---
title: "NSFW image filter for Edge, Brave, Opera and Vivaldi"
date: 2026-06-25T12:00:00+05:30
image: "images/news/nsfw-image-filter-edge-brave-opera/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "NSFW Filter is a Chromium extension, so it works on Edge, Brave, Opera, and Vivaldi from the Chrome Web Store, with the same on-device image filtering."
draft: false
faq:
  - question: "Does NSFW Filter work on Microsoft Edge?"
    answer: "Yes. Edge is built on Chromium and supports Chrome Web Store extensions. Install NSFW Filter from the Chrome Web Store and it works the same as it does on Chrome, with the same on-device image filtering."
  - question: "Can I use NSFW Filter on Brave, Opera, or Vivaldi?"
    answer: "Yes. Brave, Opera, and Vivaldi are all Chromium browsers that support Chrome Web Store extensions. The same install and the same settings work on all of them."
  - question: "Does NSFW Filter work on Firefox?"
    answer: "Not currently. NSFW Filter is a Chromium Manifest V3 extension, so it runs on Chrome, Edge, Brave, Opera, and Vivaldi. Firefox uses a different extension format and is not supported today."
---

NSFW Filter runs on Microsoft Edge, Brave, Opera, and Vivaldi, not just Chrome. All of them are built on Chromium and support Chrome Web Store extensions, so the same install and the same on-device image filtering work across all of them. You install it once from the Chrome Web Store and it behaves the same everywhere.

## Why one extension covers all of them

Edge, Brave, Opera, and Vivaldi are different browsers on the surface, but underneath they share the same engine: Chromium. Extensions are written against Chromium's APIs, so a single Manifest V3 extension runs on all of them without a separate build.

NSFW Filter is exactly that: one Chromium MV3 extension. There is no Edge version and Brave version to keep track of. There is one extension, and each browser installs it from the same [Chrome Web Store listing](https://chromewebstore.google.com/detail/nsfw-filter/kmgagnlkckiamnenbpigfaljmanlbbhh).

{{< chrome-cta >}}

## Installing on each browser

**Microsoft Edge.** Edge can install from the Chrome Web Store directly. Open the listing in Edge, and if it prompts you to allow extensions from other stores, allow it, then click Add.

**Brave.** Brave installs Chrome Web Store extensions with no extra steps. Open the listing and add it.

**Opera and Vivaldi.** Both support Chrome Web Store extensions. On Opera you may need the "Install Chrome Extensions" helper the first time; after that it is the same as Chrome.

Whichever browser you use, what you get is identical: images hidden until an on-device model checks them, explicit ones blurred, and nothing you browse leaving your machine. [Here is how that classification works](/news/how-on-device-nsfw-image-filtering-works/).

## What stays the same across browsers

The model, the effects (blur, grayscale, hide), the strictness setting, and the site allow-list all behave the same on every Chromium browser. Your settings are stored locally in whichever browser you installed it on. If you compare tools before settling in, [the free, open source comparison](/news/free-open-source-nsfw-blocker-comparison/) is the place to start.

**Firefox** is the one exception. It uses a different extension format, so NSFW Filter does not run there today. If you need a Firefox option specifically, look for a Gecko-compatible image filter; this is not one yet.

{{< chrome-cta label="Add NSFW Filter to your browser" >}}

## Frequently asked questions

### Does NSFW Filter work on Microsoft Edge?

Yes. Edge is built on Chromium and supports Chrome Web Store extensions. Install NSFW Filter from the Chrome Web Store and it works the same as it does on Chrome, with the same on-device image filtering.

### Can I use NSFW Filter on Brave, Opera, or Vivaldi?

Yes. Brave, Opera, and Vivaldi are all Chromium browsers that support Chrome Web Store extensions. The same install and the same settings work on all of them.

### Does NSFW Filter work on Firefox?

Not currently. NSFW Filter is a Chromium Manifest V3 extension, so it runs on Chrome, Edge, Brave, Opera, and Vivaldi. Firefox uses a different extension format and is not supported today.
