<!-- Starting an Animation -->
<section
  id="starting-an-animation"
  aria-labelledby="starting-an-animation"
  data-item="Starting an Animation"
>
  <h2><a href="#starting-an-animation">Starting an Animation</a></h2>
  
For now, to restart your animation, you have to reload the page. Reloading the page will reset everything in your game, so you only want to do this if the player wants to start over from the beginning.

Here's a change you can make so that the animation will restart when you move your mouse over the `<div>` element. I've given the complete CSS code, so you can compare with what you have in your project, but only a small part has changed.

Note that I have reduced the duration of the animation to just `1s`, because your time is precious, and you don't want to wait ten whole seconds to see the final result.
```css
<i>body {
  counter-set: countdown 10;
}

div::after {
  content: counter(countdown);
  </i>font-size: 256px;<b>
}

/* animation rule moved to here... and made to run faster */
div:hover::after {
  animation: timer 1s forwards step-end;</b><i>
}

@keyframes timer {
  0% { counter-increment: countdown   0; }
 10% { counter-increment: countdown  -1; }
 20% { counter-increment: countdown  -2; }
 30% { counter-increment: countdown  -3; }
 40% { counter-increment: countdown  -4; }
 50% { counter-increment: countdown  -5; }
 60% { counter-increment: countdown  -6; }
 70% { counter-increment: countdown  -7; }
 80% { counter-increment: countdown  -8; }
 90% { counter-increment: countdown  -9; }
100% { counter-increment: countdown -10; }
}

/* @keyframes timer {
   0% {  background-color: #f00; }
  10% {  background-color: #f80; }
  20% {  background-color: #8f0; }
  30% {  background-color: #0f0; }
  40% {  background-color: #0f8; }
  50% {  background-color: #08f; }
  60% {  background-color: #00f; }
  70% {  background-color: #80f; }
  80% {  background-color: #f0f; }
  90% {  background-color: #f08; }
 100% {  background-color: #f00; }
} */</i>
```
Now, if you move your mouse over the text the `<div>`, the animation will start. It will stop again and revert to showing `10` as soon as you move the mouse down off the `<div>`.

## Restarting when the state changes

If you hold the mouse in a place where the animation will run to the end, you should see a big `0`. If you then move the mouse away from the link, it will revert to showing `10`.

Before, it played all the way to the end, and then stayed at `0`, regardless of where the mouse was. What has changed?

Before, the animation started as soon as the page was loaded. The page remained loaded after the animation finished, so the CSS elves left everything the way they were told to by the final `100%` keyframe of the animation. Now, when you move the mouse off the link, they consider the animation to be switched off again, and reset everything to its original state.


</section>