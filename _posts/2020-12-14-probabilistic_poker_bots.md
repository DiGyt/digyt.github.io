---
title: "Probabilistic Poker Bots"
excerpt: "Define automated Poker playing algorithms and play against them."
header:
  teaser: "/assets/images/posts/poker_wikimedia.jpg"
  overlay_image: "/assets/images/posts/poker_wikimedia.jpg"
  caption: "Photo credit: [**Wikimedia Commons**](https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg)"
  #actions:
  #  - label: "Learn more"
  #    url: "https://commons.wikimedia.org/wiki/File:Card_games_and_game_tokens_01.jpg"
tags:
  - Probability Theory
  - Statistics
last_modified_at: 2020-12-14T10:22:00-04:00
---

Now we can look at a specific hand, e.g. [(4, 'clubs'), (8, 'hearts'), (10, 'spades'), (9, 'diamonds'), ('J', 'spades'), ('Q', 'spades'), ('Q', 'hearts')] and check it for specific combinations. We can for example look if there is a pair or a straight in our hand, our simply print out the best combination in our hand.

In contrast to most of the Poker evaluation functions I found on the web, these functions are not restricted to a specific hand size, but work correctly with any given card number, which especially helps us when not all game are known yet.


<iframe src="https://colab.research.google.com/gist/DiGyt/8fc610f08a8fe677b2d8e59c914a4226/probabilistic_poker_bots_i.ipynb#scrollTo=oigci7Edre1E&line=6&uniqifier=1
"></iframe>
<!---
<style>
iframe{height:20000px !important;}
</style>
<div style="margin-right:-30%;">
  <script src="https://gist.github.com/DiGyt/8fc610f08a8fe677b2d8e59c914a4226.js"></script>
</div>
-->
