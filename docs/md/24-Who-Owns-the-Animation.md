<!-- Who Owns the Animation -->
<section
  id="who-owns-the-animation"
  aria-labelledby="who-owns-the-animation"
  data-item="Owning the Animation"
>
  <h2><a href="#who-owns-the-animation">Who Cares Who Owns the Animation</a></h2>
  
What happens if you comment out the line that makes the `#paused` play the animation?

```css-#19
<i>body:has(input#pause:checked) div::after {
  </i><b>/*</b><i> animation: timer 10s forwards step-end; </i><b>*/</b><i>
  animation-play-state: paused;
}</i>
```
If you start the animation with the first button and then click on the Pause button, the animation reverts to its initial state, just as if you had clicked on the Reset button. The `animation-play-state` no longer knows whose animation it refers to.

Here is a more elegant version of the working CSS:
```css-#15
body:has(input#play:checked) div::after,
body:has(input#pause:checked) div::after {
  animation: timer 10s forwards step-end;
}

body:has(input#pause:checked) div::after {
  animation-play-state: paused;
}
```
Why is this more elegant? DRY! (Don't Repeat Yourself)

The duration of `10s` is defined in only one place. In the earlier version, you could set a different duration in each of the rulesets, and unexpected things could happen. (I'm guessing that they did, and you had to puzzle about what had gone wrong for a while. I did warn you, but I've also suggested that you should be disruptive. I can't have it both ways, can I?)

The selector that you use for the different rules must apply to exactly the same element. You can say that the animation "belongs" to that element. The selectors used can look very different, so long as they refer to the same animated element. These rules would also work:
```css-#15
label:has(input#play:checked) ~ div::after,
body:has(input#pause:checked) div::after{
  animation-name: timer;
  animation-duration: 10s;
  animation-fill-mode: forwards;
  animation-timing-function: step-end;
}

label:has(input#pause:checked) ~ div::after {
  animation-play-state: paused;
}
```

</section>