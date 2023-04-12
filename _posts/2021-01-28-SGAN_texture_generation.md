---
title: "Texture Generation with Spatial GANs"
excerpt: "Replicating Jetchev, Bergmann & Vollgraf (2016)."
header:
  teaser: "/assets/images/posts/new_york_SGAN.png"
  overlay_image: "/assets/images/posts/new_york_SGAN.png"
  #caption: "Photo credit: [**Wikimedia Commons**](https://commons.wikimedia.org/wiki/)"
  #actions:
  #  - label: "Learn more"
  #    url: "https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg"
tags:
  - Neural Networks
last_modified_at: 2020-08-01T10:22:00-04:00
---

Last year, I teamed up with Lucas Feldmann and Josefine Zerbe to replicate the SGAN network 
designed by Jetchev, Bergmann & Vollgraf (2016) from Zalando Research. Their SGAN model 
provides a nice way to generate non-repeating patterns of any texture. In the following 
ipynb notebook, we describe the model and training results on different textures. After 
that, we provide another notebook including a Tensorflow implementation of the original 
SGAN architecture as well as the training procedure that we used to generate our textures.
See for yourself and feel free trying out to train the network on your own texture images:


<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2FDiGyt%2Fsnippets%2Fblob%2Fmaster%2FSGAN_BlogPost_group_21.ipynb&style=default&type=ipynb&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2FDiGyt%2Fsnippets%2Fblob%2Fmaster%2FSGAN_SourceCode_group_21.ipynb&style=default&type=ipynb&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>

