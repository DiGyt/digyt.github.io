---
title: "Introducing: ASRpy"
excerpt: Artifact Subspace Reconstruction in Python.
header:
  teaser: "/assets/images/posts/asrpy_clean_evoked.png"
  overlay_image: "/assets/images/posts/asrpy_clean_evoked.png"
  overlay_filter: rgba(150, 150, 150, 0.5)
  #caption: "Photo credit: [**Wikimedia Commons**](https://commons.wikimedia.org/wiki/)"
  #actions:
  #  - label: "Learn more"
  #    url: "https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg"
tags:
  - Neuroscience
  - Data Processing
last_modified_at: 2022-02-02T10:22:00-04:00
---


Last Year, when I started comparing different EEG cleaning algorithms (see [this blog post](https://digyt.github.io/automated_EEG_cleaning_comparison/)),
I was looking for a valid and trustworthy Python implementation of the original algorithm for Artifact Subspace Reconstruction.

Artifact Subspace Reconstruction is a promising EEG cleaning algorithm, which is gaining more and more popularity due to its convincing cleaning results.
It was originally developed for an EEGLAB extension in MATLAB, but there was no perfectly equivalent version in Python. Following preceding work done by 
[Nicholas Barascud](https://nbara.github.io/python-meegkit/modules/meegkit.asr.html), and the original implementation by 
[Christian Kothe and Scott Makeig](https://github.com/sccn/clean_rawdata), I started to create a Python version of Artifact Subspace Reconstruction that 
would be perfectly equivalent with the original MATLAB implementation. After a lot of work and comparisons I succeded in doing so, producing an Artifact 
Subspace Reconstruction which was only differing from the MATLAB version by external factors, such as slightly differing Eigenspace solver algorithms used
in numpy and MATLAB. However, all other operations were perfectly replicating the MATLAB code.

The result can be found in my [ASRpy repository](https://github.com/DiGyt/asrpy). Information on the algorithm, installation and examples can be found 
there.

IF you want to know how to apply ASRpy to your own Python EEG data (either with MNE-Python or with numpy arrays), you can go through this quick tutorial:
<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2FDiGyt%2Fasrpy%2Fblob%2Fmain%2Fexample.ipynb&style=default&type=ipynb&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>


<!--   style="width:100%; height:300px;"   https://github.com/yusanshi/embed-like-gist This is a beautiful way of embedding stuff directly from github
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2FDiGyt%2Fcateye%2Fblob%2Fmain%2Fexample_minimal_use.ipynb&style=github&showBorder=on&showLineNumbers=on&showFileMeta=on&showCopy=on"></script>-->
