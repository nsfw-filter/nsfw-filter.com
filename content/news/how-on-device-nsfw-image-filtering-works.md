---
title: "How on-device NSFW image filtering works"
date: 2026-07-04T09:30:00+05:30
image: "images/news/how-on-device-nsfw-image-filtering-works/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "NSFW Filter classifies every image in your browser with a bundled AI model. Nothing you browse is uploaded. Here is exactly how that works."
draft: false
faq:
  - question: "Does NSFW Filter upload my images or browsing to a server?"
    answer: "No. The model is bundled inside the extension and runs in your browser. Classification happens on your device, and no image or page you visit is sent anywhere. You can confirm this by reading the source on GitHub or watching the network tab while it runs."
  - question: "What model does NSFW Filter use?"
    answer: "By default it uses the gantman/nsfwjs MobileNet model, a small convolutional network that runs fast on almost any machine. Since v3.0.0 you can also switch to a newer Vision Transformer model that is more accurate on hard images, at a small speed cost."
  - question: "Does it slow down my browser?"
    answer: "Classification runs on the GPU through WebGL when available, and falls back to CPU otherwise. Images load in parallel and the model checks them one at a time. On a normal page you will not notice it after the first few images warm the model up."
  - question: "Is NSFW Filter safe to install?"
    answer: "It is free, open source, and auditable on GitHub. It requests only the permissions it needs to read images on pages and store your settings locally. There is no account, no telemetry, and no remote code."
---

Short version: NSFW Filter checks every image on a page with an AI model that runs inside your browser, hides each image until the model says it is safe, and never sends anything you browse to a server. This post is the long version, because "runs locally" is a claim every clone makes and few explain.

## What "on-device" actually means

Most content filters work at the network level. You point your DNS or your router at a blocklist, and requests to known adult domains get dropped. That approach never sees the image itself. It only sees the URL, so it cannot tell a safe photo from an explicit one on a site it does not recognize, and it misses anything embedded from a third party.

NSFW Filter does the opposite. It looks at the pixels. When a page loads, the extension finds the images on it and asks a machine-learning model, "is this safe for work?" The model is a file bundled inside the extension. It runs in your browser using [TensorFlow.js](https://www.tensorflow.org/js), the same way a web app runs JavaScript. No request leaves your machine to classify anything.

That is the whole privacy story, and it is worth being precise about it: the model weights ship with the extension, the math runs on your CPU or GPU, and the only thing that ever crosses the network is the page you were already loading.

{{< chrome-cta >}}

## Hide first, reveal when safe

The order of operations matters more than people expect. If you classified an image and then hid it, there would be a window where an explicit image is on screen before the model finishes. NSFW Filter avoids that by hiding first.

The moment the page starts parsing, a small style rule hides every image that has not been checked yet. Each image is then handed to the model. If it comes back safe-for-work, the extension reveals it. If it comes back explicit, the image stays hidden, or gets blurred or grayscaled, depending on the effect you picked. Safe images appear a beat later than they would without the extension. Explicit images never get their moment on screen.

Tiny images, icons and spacers a few pixels wide, are let through without classification. Running a neural network on a 16-pixel favicon is a waste, and those images are never the problem.

## The models

The default model is the [gantman/nsfwjs](https://github.com/GantMan/nsfwjs) MobileNet, a compact convolutional network trained to sort images into categories like neutral, drawing, and explicit. It is small and fast, which is why it has been the default since the beginning. It runs comfortably on a laptop with no dedicated GPU.

Since v3.0.0 you can switch to a newer Vision Transformer model. Vision Transformers read an image as a grid of patches rather than sliding a filter across it, and the newer one is noticeably better on the hard cases, skin-heavy but safe photos that older models tend to over-flag. It is a little heavier to run. The trade is accuracy for speed, and you get to choose. We wrote up how we picked and converted it in [a separate post](/news/how-we-added-a-more-accurate-model/).

## Why it makes no network requests to classify

The extension is a Manifest V3 build, which is the current format Chrome and every other Chromium browser use. MV3 ships with a strict content security policy: an extension cannot load or run code fetched from the internet. Everything it executes has to be in the package you installed.

For a privacy tool that is a feature, not a limit. The model and the small WebAssembly runtime that backs the CPU path are both bundled. The classifier prefers your GPU through WebGL, because compiling a shader and running it on the GPU stays inside the browser's sandbox, and falls back to single-threaded WebAssembly on the CPU when WebGL cannot run the model. Either way, the computation happens on hardware you own.

If you want to check rather than take our word for it, open your browser's network tab and browse with the extension on. You will see the page's own requests and nothing from the extension calling home, because there is nothing to call.

## Where this fits

On-device image classification is the right tool when you want explicit images blurred anywhere they show up, on any site, without handing your browsing history to a filtering company. It is not a site blocker and not an accountability tool, and it reads static images rather than video. If you want the honest comparison against other approaches, we lay it out in [the best free, open source NSFW image blocker](/news/free-open-source-nsfw-blocker-comparison/). If you just want it running, [here is the two-minute setup for Chrome](/news/blur-nsfw-images-chrome/).

NSFW Filter is free and open source. You can read every line of what runs on your machine [on GitHub](https://github.com/nsfw-filter/nsfw-filter).

{{< chrome-cta label="Get NSFW Filter" >}}

## Frequently asked questions

### Does NSFW Filter upload my images or browsing to a server?

No. The model is bundled inside the extension and runs in your browser. Classification happens on your device, and no image or page you visit is sent anywhere. You can confirm this by reading the source on GitHub or watching the network tab while it runs.

### What model does NSFW Filter use?

By default it uses the gantman/nsfwjs MobileNet model, a small convolutional network that runs fast on almost any machine. Since v3.0.0 you can also switch to a newer Vision Transformer model that is more accurate on hard images, at a small speed cost.

### Does it slow down my browser?

Classification runs on the GPU through WebGL when available, and falls back to CPU otherwise. Images load in parallel and the model checks them one at a time. On a normal page you will not notice it after the first few images warm the model up.

### Is NSFW Filter safe to install?

It is free, open source, and auditable on GitHub. It requests only the permissions it needs to read images on pages and store your settings locally. There is no account, no telemetry, and no remote code.
