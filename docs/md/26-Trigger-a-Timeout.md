<!-- Trigger a Timeout -->
<section
  id="trigger-a-timeout"
  aria-labelledby="trigger-a-timeout"
  data-item="Trigger a Timeout"
>
  <h2><a href="#trigger-a-timeout">Triggering a Timeout</a></h2>
  
Now that you can create a countdown timer, the next step is to do something when the player's time runs out. If CSS were a programming language, you might do something when the value of the `counter` reaches `0`. But CSS is a styling language. It simply applies a series of rules to a basically static page. It _uses_ counters but it does not give you any way to _read the value_ of a counter, and certainly no way to compare one value with another.

<details class="note" open>
<summary>Off at a tangent</summary>
One main focus of this article is counters, but to bring this part of the story of a countdown to its logical conclusion, I'm going to have to leave counters aside for a moment, and talk about animations and other CSS properties, including custom properties that do not have a numerical value. 

</details>

You've used the `forwards` value of the `animation-fill-mode` property, so whatever CSS rules are given by the last keyframe will persist after the animation has finished. To see this, add a new rule at the end of the `@keyframes timer`:
```css-#27
<i>@keyframes timer {
  /* 10 lines skipped */
  100% { counter-increment: countdown -10;</i><b>
         color: red;
       }</b><i>
}</i>
```
Click on the Reset radio button and then on the Play button. Wait 10 seconds, and watch how the number `0` is now shown in red when the animation ends.

Can you see where this is going? Instead of simply changing the `color` of the animated element itself on the last keyframe, you can change something more radical which will affect other elements. It would be best to start a new project for this.

</section>