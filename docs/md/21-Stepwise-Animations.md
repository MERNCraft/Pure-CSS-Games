<!-- Stepwise Animations -->
<section
  id="stepwise-animations"
  aria-labelledby="stepwise-animations"
  data-item="Stepwise Animations"
>
  <h2><a href="#stepwise-animations">Stepwise Animations</a></h2>
  
 As I mentioned earlier, with the default [`animation-timing-function`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function) of `ease-in-out` (and even with the value `linear`), the changes in your countdown timer happen after 0.5s, 1.5s, 2.5s, and so on. For a countdown timer, this is not what you want. Here's how to fix that.

Keep the `@keyframes timer` rule that changes the `background-color`, but change your `animation` rule to this:
```css-#8
  animation: timer 10s forwards step-end;
```

With the `step-end` timing function, you should see an abrupt change to the next `background-color`at the end of every second. Comment out the `background-color` timer, so that the original `counter-increment` plays instead. You should see that change from `10` to `9` now happens the way you would expect.

<details class="question" open>
<summary>Using other`animation-timing-function` values</summary>
What happens if you use [`jump-end`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function#jump-end), or [`end`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function#end), or [step-start](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function#step-start) as the timing function instead? Some of these have the same effect, one does something different.

Whenever you meet a new idea, it is good to try a number of variants. This helps you to remember. The human brain is very sensitive to changes. Your eyes are constantly twitching, so that the signal they send to the brain is always slightly different. [If the image on your retina does not change, your vision becomes poorer](https://www.rochester.edu/newscenter/small-eye-movements-are-critical-for-20-20-vision-415522/). When the pump on your refrigerator is running, your brain stops hearing it. When the pump motor stops, you suddenly become aware of the lack of noise.

If you give your brain the chance to compare and contrast ideas, your brain will pay more attention.

</details>

Here's another demonstration of the timing of changes of a different discrete animatable CSS property: `z-index`:

<iframe
  id="iframe-timing"
  title="Timing"
  width="300"
  height="150"
  src="https://merncraft.github.io/timing">
</iframe>

This demonstration uses the following `@keyframes` animation:
```css
@keyframes z-left {
  0%  { z-index: 0; left:  0px; }
  10% { z-index: 1; left:  0px; }
  30% { z-index: 2; left:  50px; }
  50% { z-index: 3; left: 100px; }
  70% { z-index: 4; left: 150px; }
  90% { z-index: 5; left: 200px; }
 100% { z-index: 5; left: 200px; }
}
```
When you select `step-end` as the `animation-timing-function` for this animation, the integer steps for `z-index` coincide with the stepwise change of the `left` property for the grey square. When you select `linear` as the `animation-timing-function`, the value of `left` changes at a steady pace between keyframes. The change in `z-index` occurs when the grey square is halfway between two keyframe positions.

You can find a list of all animatable CSS properties [here](https://www.quackit.com/css/css3/animations/animatable_properties/). Most properties have an animation associated with them, and code that you can copy and paste.

</section>