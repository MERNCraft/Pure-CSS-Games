---
title: Pure CSS Games 
subtitle: '1: Using CSS counters in creative ways'
month: January 2025
organization: MERNCraft
repo: Pure-CSS-Games
---

<!-- Intro -->
<section
  id="intro"
  aria-labelledby="intro"
  data-item="Introduction"
>
  <h2><a href="#intro">Introduction</a></h2>
  

CSS is not a programming language. Not _officially_. But it [is possible to create games with only HTML and CSS](https://www.youtube.com/watch?v=-e5nWsGgZXQ). And there are even some tutorials on how to make a specific game: [a click 'em all](https://medium.com/cssclass-com/how-to-create-pure-css-games-2a29c777bf4), [a jigsaw](https://css-tricks.com/how-i-made-a-pure-css-puzzle-game/), [a maze](https://scriptraccoon.dev/blog/create-css-maze), and maybe more that I have not found.

My aim here is different. In this series of articles, I want to get you to experiment with the different techniques that you can use to create your own games. By the end of each article, you won't have created a game, but you will have understood why some things work and some things don't.

In this article, you'll be looking at the following ideas:

1. Using checkboxes and radio buttons to store state
2. Using animations to change state
3. Using `::before` and `::after` pseudo-elements
4. Using `z-index` to reorder elements
5. Using the `:hover` pseudo-class to intercept the actions of the mouse
6. Writing selectors that control the logic
7. **Using custom CSS properties**
8. **Working with counters**

My main focus here will be on the last two ideas: understanding how **CSS custom properties and counters work together**. You need to use counters, after all, to number things: to show the score or to display a timer, for example. These are simple ways to add urgency and excitement to a game. And if you think laterally, you can also get counters to do some quite unexpected things for you, as you will see.

I won't treat the other seven ideas is such great depth here. I'll be writing other articles about them specifically.

</section>