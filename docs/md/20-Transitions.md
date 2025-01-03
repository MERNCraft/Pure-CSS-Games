<!-- Transitions -->
<section
  id="transitions"
  aria-labelledby="transitions"
  data-item="Transitions"
>
  <h2><a href="#transitions">Transitions</a></h2>

You can observe this interpolation process by adding a second `@keyframes timer` at-rule after the first:
```css
@keyframes timer {
  0% { background-color: #f00; }
 10% { background-color: #f80; }
 20% { background-color: #ff0; }
 30% { background-color: #0f0; }
 40% { background-color: #0cf; }
 50% { background-color: #06f; }
 60% { background-color: #33f; }
 70% { background-color: #00f; }
 80% { background-color: #80f; }
 90% { background-color: #f0f; }
100% { background-color: #f00; }
}
```
<details class="note" open>
<summary>Only the last timer animation is applied</summary>
Because this second at-rule appears later in the CSS file than the other, the CSS elves will ignore the first  `@keyframes timer`. They won't increment the countdown counter any more, they will only change the `background-color`.

</details>

Now when you refresh your page, you should see the `background-color` moving smoothly  from one colour to the next. The effect should be similar to what you see in the animation below. (My animation has more bells and whistles than yours will have, to illustrate the various points I'll be mentioning).

<iframe
  id="iframe-colour-countdown"
  title="Colour Countdown"
  width="300"
  height="300"
  src="https://merncraft.github.io/colour-countdown">
</iframe>

## `animation-timing-function`

Actually, the default [`animation-timing-function`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function) is `ease-in-out`, so there it slows down as it reaches each intermediate `background-color` then speeds up again If you replace your `animation` rule with this...

```css-#8
  <i>animation: timer 10s forwards </i><b>linear</b><i>;</i>
```
... then the changes become even smoother.

</section>