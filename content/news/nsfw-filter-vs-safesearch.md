---
title: "SafeSearch isn't enough: block explicit images everywhere"
date: 2026-05-28T15:00:00+05:30
image: "images/news/nsfw-filter-vs-safesearch/cover.png"
author: "Navendu Pottekkat"
type: "regular"
description: "Google SafeSearch only filters search results, not the rest of the web. Here is how to block explicit images on every site with an on-device AI filter."
draft: false
faq:
  - question: "Does SafeSearch block images on all websites?"
    answer: "No. SafeSearch only filters explicit results inside Google Search, including Google Images. It has no effect on other websites, social feeds, forums, or images embedded from third parties. For those you need a filter that checks images on every page."
  - question: "Why do I still see explicit images with SafeSearch on?"
    answer: "Because SafeSearch only covers Google's own search results. Once you leave the results page and visit a site directly, SafeSearch stops applying. An on-device image filter like NSFW Filter checks the images on every page you visit, not just search."
  - question: "Can I use SafeSearch and NSFW Filter together?"
    answer: "Yes, and it is a good combination. SafeSearch keeps explicit results out of Google Search, and NSFW Filter blurs explicit images everywhere else. They cover different gaps and do not conflict."
---

Google SafeSearch only filters images inside Google Search. It does nothing on the rest of the web. If you have SafeSearch on and still run into explicit images, that is not a bug, it is the boundary of what SafeSearch does. To filter images everywhere else, you need something that checks images on every page, not just search results. That is the gap NSFW Filter fills.

## What SafeSearch actually covers

SafeSearch is a filter on Google's search results, including Google Images. When it is on, Google tries to keep explicit results out of what it shows you. That is useful, and if you use Google Images a lot you should leave it on.

But it is scoped to Google. The instant you click through to a website, or open a social feed, or land on a page with an image embedded from somewhere else, SafeSearch is no longer in the picture. It never saw those images. It only ever filtered the search results page.

## The structural blind spot

The web is mostly not search results. Explicit images turn up in comment sections, on forums, in feeds, in ads, and embedded from image hosts onto pages about something else entirely. SafeSearch cannot touch any of that, because it is a search-results filter, not a page filter.

This is not a setting you can turn up to fix. It is what the tool is. Reddit's own NSFW blur and X's sensitive-media setting have the same shape of limit: each one only covers its own content, and only while you stay logged in with the setting on.

{{< chrome-cta >}}

## How per-page image filtering fills the gap

NSFW Filter works one level down from all of that. Instead of filtering a site's results, it looks at the images on whatever page you are on and checks each one with an AI model running in your browser. Explicit images get blurred or hidden before you see them, on any site, including images embedded from third parties.

Because it reads the pixels rather than trusting a site's own setting, it does not matter whether the site has an NSFW toggle or whether you are logged in. It catches the image either way. And because the classification runs on your device, none of your browsing is uploaded to make it work. [Here is how that on-device filtering works](/news/how-on-device-nsfw-image-filtering-works/).

## Use both

This is not SafeSearch versus NSFW Filter. Leave SafeSearch on to keep explicit results out of Google, and run NSFW Filter to blur explicit images everywhere else. Belt and suspenders. They cover different gaps and do not get in each other's way.

If the images you run into are mostly on social platforms, [blurring NSFW on Reddit and X](/news/blur-nsfw-reddit-twitter/) is worth a read. Otherwise, the two-minute install is [here](/news/blur-nsfw-images-chrome/).

{{< chrome-cta label="Filter images everywhere with NSFW Filter" >}}

## Frequently asked questions

### Does SafeSearch block images on all websites?

No. SafeSearch only filters explicit results inside Google Search, including Google Images. It has no effect on other websites, social feeds, forums, or images embedded from third parties. For those you need a filter that checks images on every page.

### Why do I still see explicit images with SafeSearch on?

Because SafeSearch only covers Google's own search results. Once you leave the results page and visit a site directly, SafeSearch stops applying. An on-device image filter like NSFW Filter checks the images on every page you visit, not just search.

### Can I use SafeSearch and NSFW Filter together?

Yes, and it is a good combination. SafeSearch keeps explicit results out of Google Search, and NSFW Filter blurs explicit images everywhere else. They cover different gaps and do not conflict.
