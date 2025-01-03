<!-- Final Tweaks -->
<!-- Final Tweaks -->
<section
  id="final-tweaks"
  aria-labelledby="final-tweaks"
  data-item="Final Tweaks"
>
  <h2><a href="#Final Tweaks">Final Tweaks</a></h2>

The [online version](https://merncraft.github.io/countdown)of this mini story game contains some cosmetic improvements. In particular, if you let the countdown reach one second, your version of the game will say "We have only 1 *seconds* left!", with "seconds" in the plural even though there is only one.

[![1 second](images/second.webp)](https://merncraft.github.io/countdown/)


<details class="challenge" open>
<summary>Just 1 second</summary>
In the [online version](https://merncraft.github.io/countdown), this infelicity has gone. How do you think I fixed it?

Hint: [counters can count](https://merncraft.github.io/counter-styles/).

Also, if the text wraps, then the line break will not occur between the number and the word "second". For this I've used a non-breaking space, which for CSS needs to be written as `"\00a0"`. You can click on GitHub's Octocat logo to visit the repository where you can find the complete source. Or you can look at the solution below.

<details class="solution">
<summary>Solution</summary>
```css
<i>body {
  --display: none;
  </i><b>counter-reset:
    countdown 10
    second 2 /* used with the seconds counter-style */
  ;</b><i>
  animation: timer 10s step-end forwards paused;
}

</i><b>/* Create a counter-style to use "2 seconds" and "1 second"
 * correctly. Use a non-breaking space between the number
 * and "seconds" so that the whole chunk "X seconds" will 
 * wrap to the next line together.
 */
@counter-style seconds {
  system: cyclic;
  symbols: "\00A0second" "\00A0seconds";
}</b>
```
```css-s
/* lines skipped */
```
```css-#67
<i>span::before {
  content: "My hero!";
  display: block;
}

span::after {
  content: "You saved us </i><b>all... with only " counter(countdown) counter(second, seconds) " to go!"</b><i>
}

input:not(:checked) {
  & ~ span::before {
    content: "Click me! Before it's too late...";
  }

  & ~ span::after {
    content: "We have only " counter(countdown) </i><b>counter(second, seconds)</b><i> " left!";
  }
}</i>
```

</details>
</details>

</section>