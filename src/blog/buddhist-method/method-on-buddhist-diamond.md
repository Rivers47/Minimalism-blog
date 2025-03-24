---
title:  Method on Buddhist's Diamond
description: An English translation of my original post on dodging Buddhist's Diamond
tags: ["post", "touhou"]
date: 2023-12-30
location: 迷いの竹林
layout: article.njk
permalink: "blog/{{ title | slugify }}.html"
---

<!-- <div class="lead">
Until now, trying to style an article, document, or blog post with Tailwind has been a tedious task that required a keen eye for typography and a lot of complex custom CSS.</div> -->

I don't know why translating this to English feels harder than translating to Japanese. Here I am and I updated this article with some new revelations unknown when I wrote the Chinese version, and got rid of some false conclusions.

# Introduction

BD consists of 33 familiars that fires lasers, random star bullets, and a series of aimed arrow heads from Kaguya. The interval of which the lasers are fired is actually not constant, the first two lasers are 200 frames apart, the later ones are 180 frames apart. The first aimed bullets is spawned 128 frames after the first laser, and is fired every 144 frames afterwards. The arrow heads fly very slowly, and the next wave is spawned before the previous wave leaves the screen. Similarly for lasers, the next wave start to appear before the previous wave fades off.

We can model the laser, starting from the second wave by:


$\sin(\pi180(x−200))=0\\{x>199\\}$

aimed arrow heads: $\sin(\pi144(x−128))=0\\{x\geq 0\\}$

Pardon the dumb way of formulating this on Desmos...

If we draw this on Desmos, it is clear that although the lasers and the aimed bullets are not synchronized they roughly line up every 4 waves.

The hitboxes of lasers spawn extremely late and despawn very early. I'm not sure how to test that without looking at the code directly.

Magic and Scarlet usually don't worry about this spell too much as they only have to dodge 3 waves for survival. Weak shots, and especially solo human shots suffer greatly from BD, and is one of the biggest roadblocks in LNN.

On the other hand solo shots always take exactly the same time to kill the spell, and there is no need to stay under the boss. For solo youkai shots, all shots can hit Kaguya regardless of their posistion except solo Alice. So there are also potential benefits if one can take advantage of all the horizontal screen space.

# How to dodge BD

We call each continuous space surrounded by lasers a cell. Dodging BD consists of three problems:

1. Which cell to choose for each laser wave
2. How (and whether) to misdirect the aimed bullets
3. How to dodge the random start bullets

If you vision covers half of the screen, then you can simply choose an area with the least star bullets. Unfortunately I have not evolved to process dozes of random bullets simultaneously, so I have to consider all three factors.

For each of these problems

1. Naturally the the bigger the cell the better, but in reality you only need enough space to maneuver around potential start bullet clusters, and bigger cells are not that meaningful. 
2. We don't want the arrow heads to divide a cell in half, making it even smaller, in other words we either want to be in a different cell from the arrow heads, or make them to overlap with one of the lasers. (Technically you could micro thru the arrow heads, but I have never actively practiced that).
3. There is not much to dodging random things, only thing worth mentioning is that the starts are under the arrow heads, so pay extra attention on stars coming from the same direction as the aimed arrow heads. 

Combining 2 and 3, we conclude the following:

If laser lines appear first, then arrow heads lock on you, misdirect the arrow heads towards one of the laser warning lines. If arrow heads lock at the same time, or appears earlier, then try to macro to a different cell.

One problem remains, the arrow heads are so slow such that sometimes the bullets you misdirect only arrive at the next wave of lasers, making misdirection meaningless. However, there are still sometimes this will work.

# Conclusion

Depending on your shot type, memorize the waves where it is meaningful to misdirect the arrow heads. When you can misdirect, try to enlarge your field of view and look for relatively sparse area of star bullets and big cells.

 
## Aside:

There are beliefs that dodging BD is easier at the very sides. If true then all solo human shots should employ it. However, empirically I have not found it easier at the side. Also, it might also be easier to dodge above the bottom row of familiars, since you technically deal with less lasers, but I have not practiced dodging like that. Both ideas came from/were inspired by Levea. It'd be interesting to see an LNN with either of them, especially the second strat.

## Another note (updated in 2025)
TL;DR: there are certain times during the spell where it's harder because the arrows block along with the lasers, so after palying a lot of times you can get a feeling that you need to semi-macro to avoid the arrow-laser combo



<!-- old template  -->

