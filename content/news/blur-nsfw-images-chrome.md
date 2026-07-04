---
title: "How to automatically blur NSFW images in Chrome"
date: 2026-05-12T10:00:00+05:30
image: "images/news/blur-nsfw-images-chrome/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "Blur explicit images automatically in Chrome with NSFW Filter. It hides every image until an on-device AI checks it, then blurs anything explicit. Free."
draft: false
faq:
  - question: "How do I blur NSFW images in Chrome?"
    answer: "Install the NSFW Filter extension from the Chrome Web Store. It starts working immediately: every image is hidden until an on-device AI model checks it, then explicit images are blurred and safe ones are shown. No account or setup is required."
  - question: "Does NSFW Filter work on every website?"
    answer: "Yes. It classifies the images on whatever page you are on, so it works site-agnostically, including social feeds, forums, image search, and third-party embeds. You can allow-list sites you trust to skip filtering there."
  - question: "Do I have to maintain a blocklist?"
    answer: "No. NSFW Filter judges each image with an AI model rather than matching URLs against a list, so there is nothing to maintain. It works on sites it has never seen."
---

To blur NSFW images automatically in Chrome, install NSFW Filter. It hides every image on a page until an AI model checks it in your browser, then blurs anything explicit and shows the rest. There is no blocklist to maintain and no account to create. That is the whole setup, and the rest of this post covers the details.

## The 30-second setup

1. Open the [NSFW Filter listing on the Chrome Web Store](https://chromewebstore.google.com/detail/nsfw-filter/kmgagnlkckiamnenbpigfaljmanlbbhh).
2. Click **Add to Chrome**, then confirm.
3. That is it. It starts filtering immediately, with blur as the default effect.

No sign-up, no configuration file, no blocklist to import. The model that does the work is bundled in the extension, so there is nothing to download separately and nothing to connect to.

{{< chrome-cta >}}

## How it blurs images without a blocklist

Most blockers match URLs against a list of known adult sites. That breaks the moment an explicit image shows up somewhere the list does not cover, which is most of the internet.

NSFW Filter does not care what site you are on. When a page loads, it hides the images, hands each one to an AI model running in your browser, and blurs the ones the model marks explicit while revealing the rest. Because it reads the image itself, it catches explicit content on sites it has never seen, including images embedded from other domains. For how that classification works under the hood, see [how on-device NSFW image filtering works](/news/how-on-device-nsfw-image-filtering-works/).

Nothing you browse is uploaded. The classification runs on your device.

## Choosing your effect

Blur is the default, but you can change how detected images are handled from the extension popup:

- **Blur** keeps the layout intact and lets you tell an image is there without seeing it. Good for shared or work screens where a blank gap would look odd.
- **Grayscale** desaturates the image. Lighter touch, useful if you find blur too aggressive.
- **Hide** removes the image entirely.

You can also adjust how strict the classifier is and allow-list sites you trust so filtering is skipped there. [Blur, grayscale, or hide](/news/blur-vs-hide-vs-grayscale/) walks through when each setting fits.

## It works beyond Chrome, too

NSFW Filter is a Chromium extension, so the same install works on Microsoft Edge, Brave, Opera, and Vivaldi from the same Chrome Web Store listing. If that is your browser, see [the cross-browser guide](/news/nsfw-image-filter-edge-brave-opera/). It also works site-agnostically on social platforms; [blurring NSFW on Reddit and X](/news/blur-nsfw-reddit-twitter/) covers those specifically.

## Honest scope

NSFW Filter blurs static images. It does not filter video, and it is not a site blocker or an accountability tool. If explicit images showing up unexpectedly is the thing you want gone, this handles it. It is free, open source, and runs entirely on your machine.

{{< chrome-cta label="Add NSFW Filter to Chrome" >}}

## Frequently asked questions

### How do I blur NSFW images in Chrome?

Install the NSFW Filter extension from the Chrome Web Store. It starts working immediately: every image is hidden until an on-device AI model checks it, then explicit images are blurred and safe ones are shown. No account or setup is required.

### Does NSFW Filter work on every website?

Yes. It classifies the images on whatever page you are on, so it works site-agnostically, including social feeds, forums, image search, and third-party embeds. You can allow-list sites you trust to skip filtering there.

### Do I have to maintain a blocklist?

No. NSFW Filter judges each image with an AI model rather than matching URLs against a list, so there is nothing to maintain. It works on sites it has never seen.
