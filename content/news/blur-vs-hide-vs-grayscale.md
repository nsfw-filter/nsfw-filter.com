---
title: "Blur, grayscale, or hide? Choosing NSFW filter effects"
date: 2026-06-02T09:00:00+05:30
image: "images/news/blur-vs-hide-vs-grayscale/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "NSFW Filter lets you blur, grayscale, or hide detected images and adjust strictness. Which effect fits work, home, and shared screens, and how to tune it."
draft: false
faq:
  - question: "What is the difference between blur, grayscale, and hide?"
    answer: "Blur keeps the image in place but unreadable, so the layout stays intact. Grayscale desaturates it, a lighter touch. Hide removes the image entirely. NSFW Filter lets you pick whichever fits, where most competitors only offer one behavior."
  - question: "How do I make NSFW Filter stricter or less strict?"
    answer: "Adjust the sensitivity setting in the popup. A stricter setting flags more images, which catches more explicit content but raises false positives on borderline-safe images. A looser setting does the reverse. Tune it to your tolerance."
  - question: "Can I turn off NSFW Filter on sites I trust?"
    answer: "Yes. Allow-list any site you trust and NSFW Filter skips filtering there, while still working everywhere else."
---

NSFW Filter can blur, grayscale, or hide the images it flags, and let you tune how strict it is. Most competitors only do one of those. Blur is the default and the right pick for most people; grayscale is a lighter touch; hide removes the image entirely. Which one you want depends on where you are browsing and who might see the screen.

## The three effects

**Blur** leaves the image in place but unreadable. The page layout does not shift, so nothing looks broken, and you can tell an image is there without seeing it. This is the default, and it is the best fit for shared or work screens where a sudden blank gap would draw more attention than a blurred box.

**Grayscale** strips the color out of the image. It is the lightest touch of the three. Detail is still visible, so it is less about hiding and more about taking the edge off. Useful if you find full blur too aggressive for everyday browsing.

**Hide** removes the flagged image completely. Pick this when you would rather the content simply not be there, and you do not mind the occasional gap in a page's layout.

{{< chrome-cta >}}

## Tuning strictness

The strictness setting decides how confident the model has to be before it flags an image. This is a genuine trade-off, not a "more is better" dial.

Turn it up and the filter catches more, including borderline images, at the cost of occasionally blurring a perfectly safe photo, a portrait or a beach shot. Turn it down and you get fewer false positives but a higher chance something explicit slips through. There is no universally right setting. Set it to your own tolerance for each kind of mistake.

If you are curious why some safe images get flagged at all, it comes down to the model, and [how on-device NSFW image filtering works](/news/how-on-device-nsfw-image-filtering-works/) explains what the classifier is actually judging.

## Allow-listing sites you trust

Some sites you already know are safe, and running the filter on them is just overhead. Allow-list those, and NSFW Filter skips them while staying on everywhere else. It is the cleanest way to cut false positives on sites you visit constantly without weakening the filter where it matters.

## Suggested settings

- **At work or on a shared screen:** blur, with strictness a notch high. Discretion matters more than the odd false positive here.
- **On your own machine at home:** blur or grayscale at the default strictness. Comfortable for daily browsing.
- **On public or borrowed screens:** hide, strictness high. When you cannot control who glances over, remove flagged images outright.

Whichever you choose, the classification runs on your device and nothing you browse is uploaded. If you have not installed it yet, [the Chrome setup takes about two minutes](/news/blur-nsfw-images-chrome/), and it works the same on [Edge, Brave, Opera, and Vivaldi](/news/nsfw-image-filter-edge-brave-opera/).

{{< chrome-cta label="Set up NSFW Filter" >}}

## Frequently asked questions

### What is the difference between blur, grayscale, and hide?

Blur keeps the image in place but unreadable, so the layout stays intact. Grayscale desaturates it, a lighter touch. Hide removes the image entirely. NSFW Filter lets you pick whichever fits, where most competitors only offer one behavior.

### How do I make NSFW Filter stricter or less strict?

Adjust the sensitivity setting in the popup. A stricter setting flags more images, which catches more explicit content but raises false positives on borderline-safe images. A looser setting does the reverse. Tune it to your tolerance.

### Can I turn off NSFW Filter on sites I trust?

Yes. Allow-list any site you trust and NSFW Filter skips filtering there, while still working everywhere else.
