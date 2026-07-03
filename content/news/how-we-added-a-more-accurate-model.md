---
title: "How we added a more accurate model"
date: 2026-07-02T10:07:21+05:30
image: "images/news/new-model/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "NSFW Filter can now classify images with a new Vision Transformer model. Here's how we chose it and converted it to run entirely in your browser."
draft: false
---

NSFW Filter has always classified images with one model: the gantman/nsfwjs MobileNetV2, whose weights have been frozen since 2020. It works, but the field has moved on, and we wanted to know whether a newer model could do better without breaking the one rule the extension never bends. Everything runs on your machine. Nothing is sent to a server.

v3.0.0 is the answer. It ships a second model you can switch to, and this is the story of how it got there.

## Picking a candidate

Most of the good open NSFW classifiers released since 2020 are binary Vision Transformers. Instead of the five categories the current model predicts, they output a single number: the probability that an image is NSFW. To compare them fairly we built a small benchmark harness that runs each model over the same labeled images and reports accuracy, precision and recall, ROC AUC, and how often each one false-flags a hard negative.

The test set was around 800 images: 400 NSFW from a permissively licensed Hugging Face set, and 400 safe images split across celebrity portraits, animals, and food. Portraits are the interesting slice, because skin-heavy but perfectly safe photos are where NSFW models tend to cry wolf.

We ran the shipped model against two candidates, [Marqo's nsfw-image-detection-384](https://huggingface.co/Marqo/nsfw-image-detection-384) (a ViT-Tiny) and [AdamCodd's vit-base-nsfw-detector](https://huggingface.co/AdamCodd/vit-base-nsfw-detector) (a larger ViT-base). Both beat the baseline. At our default strictness they caught roughly 96% of the NSFW images against the current model's 91%, and they did it while flagging fewer of the safe portraits. AdamCodd edged ahead on raw accuracy, but it is a ViT-base, several times heavier. Marqo's ViT-Tiny landed within a hair of it at a fraction of the size, so that is the one we picked.

Two honest caveats. One labeled set is not the open web, and this one leans toward photographic content with little drawn or borderline material, so read the numbers as directional. The NSFW images may also overlap what the current model was trained on, which quietly flatters the baseline. We treated the benchmark as a reason to try the new model, not as proof it wins everywhere.

## The constraint: it has to run in the browser

This is where most of the work went.

NSFW Filter classifies every image locally, inside the extension. Manifest V3's content security policy forbids remote code and eval, which rules out fetching a model at runtime or running anything like PyTorch. The model has to be a TensorFlow.js graph model, bundled with the extension, running on the GPU through WebGL with a single-threaded WASM fallback for when the GPU cannot.

Marqo publishes the model as PyTorch weights through timm. So before any of it could ship, the weights had to make a trip: PyTorch to ONNX to TensorFlow to TensorFlow.js.

## Converting the weights

Each step below looks like one line. Every one of them was a dead end first, so here is what actually worked.

**Export to ONNX.** From timm, export with `torch.onnx` at opset 17 and the classic exporter (`dynamo=False`). The newer dynamo exporter produced a graph the next tool could not read.

**Simplify it, separately.** Run `onnxsim` on the ONNX file as its own step before anything else touches it. Skip this and the conversion silently builds a broken attention layer, a matrix multiply with its axes swapped, that only surfaces as wrong numbers much later.

**ONNX to TensorFlow with onnx2tf.** This transposes the graph from PyTorch's channels-first layout to the channels-last (NHWC) layout the browser produces natively, so there is no pixel shuffling at runtime. Two traps here: onnx2tf bundles its own copy of onnxsim that segfaulted on this model, so disable it (`-nuo`), and it tries to download a calibration sample on first run, which fails with no network and leaves a corrupt file behind. Pre-place that sample and it skips the download.

**TensorFlow to TensorFlow.js.** Convert the saved model with `tensorflowjs_converter`. There is a version knot to untie: numpy has to stay below 2.0 for the earlier steps (numpy 2 breaks a pickle load), but that pins an old, broken tensorflowjs. The fix is to do it in two stages, build the saved model first, then upgrade tensorflowjs to 4.22 in a clean environment for the final conversion.

**Prove it survived.** Conversion across three frameworks is exactly the kind of thing that quietly changes a number. So we fed one fixed input through the original ONNX model and the final TensorFlow.js model and compared: 0.11132877 against 0.11132858, a difference of about two ten-millionths. The layout and the normalization made it through intact.

## Wiring it in

The converted model wants a `[1, 384, 384, 3]` tensor, so the extension reads an image's pixels, resizes to 384 square, scales to the 0-to-1 range, and normalizes each channel with a mean and standard deviation of 0.5. The model returns two logits; after a softmax, index 0 is the probability that the image is NSFW.

The strictness slider in the popup maps that probability to a single cutoff. (The original five-class model uses the same slider differently, tuning a threshold per category, so each model keeps its own decision logic behind one shared control.) Both models ship inside the extension, which makes the download a little larger than before, but only the model you actually select is loaded into memory.

## Try it

The new model is a choice, not a change. Open NSFW Filter's advanced settings, pick it from the "Trained model" dropdown, and the extension starts classifying with it. The original model stays the default, and as always, nothing you look at leaves your browser.

You can read the rest of what shipped in [the v3.0.0 notes](/news/v3.0.0/), or dig into the code on [GitHub](https://github.com/nsfw-filter/nsfw-filter).
