---
title: "Introducing: CatEyes"
excerpt: Unified Gaze Classification for Eye Tracking.
header:
  teaser: "https://raw.githubusercontent.com/DiGyt/cateyes/main/docs/files/imgs/cateye_header.png"
  overlay_image: "https://raw.githubusercontent.com/DiGyt/cateyes/main/docs/files/imgs/cateye_header.png"
  overlay_filter: rgba(150, 150, 150, 0.5)
  #caption: "Photo credit: [**Wikimedia Commons**](https://commons.wikimedia.org/wiki/)"
  #actions:
  #  - label: "Learn more"
  #    url: "https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg"
tags:
  - Neuroscience
  - Data Processing
last_modified_at: 2021-11-18T10:22:00-04:00
---

<style>
iframe{height:2500px !important;}
</style>

Over the last years, I have been working a lot with classification of eye tracking data.

I found that there are tons of different gaze classification available out there, but many of them took a terrible amount of installation, implementation, and data wrangling work until ready for application. If you had to apply gaze classification at one point in your career, you might know what I'm talking about. As this problem deterred me and many of my lab members from actually using these algorithms, I decided to unite all these different algorithms in one toolbox, and unite all their functionality into one simple and easily applicable workflow.

The result of this work is the [CatEyes](https://github.com/DiGyt/cateyes) Toolbox. It does not allow you to test different gaze classification algorithms with very simple and standardized functions, it also provides some tools to easily handle and visualize eye tracking data, especially with respect to classification.

If this idea caught your attention, feel free to check out the repository, where you can find everything you need to know about application, installation, as well as practical examples on how to directly apply gaze classification to your specific eye tracking project. Probably the best way to get an idea of how CatEyes works, is by using our CatEyes minimal example. You can inspect the intrdocutory example below, or click on the "Open in Colab" button, to run it in Google Colab's hosted runtime.

<script src="https://gist.github.com/DiGyt/65d8e15964b7ec144dd2ecf298f5bdc2.js"></script>

Of course this is by far not everything you can do with CatEyes. If you wonder what other functionality CatEyes provides, you can check out the repository, or have a look at the [CatEyes documentation](https://digyt.github.io/cateye/cateyes/index.html).




<!--   style="width:100%; height:300px;"   https://github.com/yusanshi/embed-like-gist This is a beautiful way of embedding stuff directly from github
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2FDiGyt%2Fcateye%2Fblob%2Fmain%2Fexample_minimal_use.ipynb&style=github&showBorder=on&showLineNumbers=on&showFileMeta=on&showCopy=on"></script>-->
