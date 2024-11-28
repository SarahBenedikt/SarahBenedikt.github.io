---
layout: post
title:  "How to build the Breakout Game using Pygame"
date:   2024-10-10 20:10:57 -0600
categories: coding games
---
I rebuild a real classics of Videogames - Breakout. You can find the final version on my [GitHub](https://github.com/SarahBenedikt/Breakout). I will explain the process of building on this page.

## Final Screen Shots
![breakout image]({{ "/assets/screenshot_breakout_1.png" | relative_url }})
*Screenshot of my breakout game*

## What did I use?
- PyCharm as IDE
- Pygame library
- Bricks and Paddle from [opengameart.org](https://opengameart.org/content/breakout-set)

## How I creatd the game
First I imported all relevant modules. The sys module will be important later to close the game correctly. I used the random module to select different coloured bricks.

{% highlight ruby %}
import pygame
from sys import exit
import random
{% endhighlight %}

Then I started pygame an initiated all subparts with:

{% highlight ruby %}
pygame.init()
{% endhighlight %}

Next step is to create the game loop.
