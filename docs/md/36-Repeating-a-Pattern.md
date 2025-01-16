<!-- Repeating a Pattern -->
<section
  id="repeating-a-pattern"
  aria-labelledby="repeating-a-pattern"
  data-item="Repeating a Pattern"
>
  <h2><a href="#repeating-a-pattern">Repeating a Pattern</a></h2>
  
You want to be able to cycle through the numbers `0` to `9`, but for now, you can only show the number `1` (if the right radio button is checked). You need more labels with spans and radio buttons in your HTML page.

<details class="note" open>
<summary>Apply the pattern</summary>
For brevity, I'm not going to list them all. You should be able to see the pattern and the missing labels.

</details>

```html-
<i>  <label class="d0">
    <span class="minus">–</span>
    <input type="radio" name="d" id="d0" checked>
    <span class="plus">+</span>
  </label>
  <label class="d1">
    <span class="minus">–</span>
    <input type="radio" name="d" id="d1">
    <span class="plus">+</span>
  </label>
 <label class="d2">
    <span class="minus">–</span>
    <input type="radio" name="d" id="d2">
    <span class="plus">+</span>
  </label>
  </i><b><!-- Add a label for 3 with the appropriate class and id -->
  <label class="d3">
    <span class="minus">–</span>
    <input type="radio" name="d" id="d3">
    <span class="plus">+</span>
  </label>
  <!-- Continue the sequence up to 9 (4-8 are skipped here) -->
  <label class="d9">
    <span class="minus">–</span>
    <input type="radio" name="d" id="d9">
    <span class="plus">+</span>
  </label></b><i>
  <span class="display"></span></i>
```

## More CSS

You'l also need more CSS rules, each with a similar pattern.

<details class="note" open>
<summary>Cheating</summary>
In the CSS below, I've cheated to make the `.d3` label jump directly to `.d9`, to match the HTML entries above and to keep the code short.

</details>

```css
<i>body {
  --counter: 0;
  counter-set: digit var(--counter);
}

label span {
  display: none;
}

</i><b>body:has(#d0:checked) {
  --counter: 0;
  .d9 span.minus { display: block }
  /* Notice that the "minus" span belongs to 9 */
  .d1 span.plus  { display: block }
}</b><i>
body:has(#d1:checked) {
  --counter: 1;
  .d0 span.minus { display: block }
  .d2 span.plus  { display: block }
}
</i><b>body:has(#d2:checked) {
  --counter: 2;
  .d1 span.minus { display: block }
  .d3 span.plus  { display: block }
}
body:has(#d3:checked) {
  --counter: 3;
  .d2 span.minus { display: block }
  /* I've cheated: I used .d9 instead of .d4 */
  .d9 span.plus  { display: block }
}
/* And so on, up to 9 ... */
body:has(#d9:checked) {
  --counter: 9;
  .d3 span.minus { display: block } /* <<< .d3/.d8 cheat */
  /* Notice that the "plus" span belongs to 0 */
  .d0 span.plus  { display: block }
}</b></i>

span {
  --size: 64px;
  font-size: var(--size);
}

span.display::after {
  content: counter(digit);
}</i>
```

I suggest that you add the following cosmetic rulesets, so the `-` and `+` spans don't keep changing places.

```css
span {
  position: absolute;
  top: 30px;
}
span:first-child {
  left: 10px;
}
span:last-child {
  left: 60px;
}
```
Make these changes to your project, and then check if the plus and minus buttons work as expected.

<details class="question" open>
<summary>Cycling from 9 to 0</summary>
Did you notice that the "plus" for 9 and the "minus" for 0 are different? That's what makes the system cycle.

</details>

<details class="note" open>
<summary>No repeat loops</summary>
This exercise demonstrates one of the frustrations of writing CSS-only activities. There are no repeat loops or Boolean logic in CSS. As a result, every pattern has to be written out methodically, chunk by chunk, and every variant on the pattern needs to be manually edited.

If you are familiar with [SASS](https://sass-lang.com/), you can use its [flow control features](https://sass-lang.com/documentation/at-rules/control/) to generate patterns in CSS. You can use JavaScript in NodeJS to generate corresponding patterns for HTML.

Nonetheless, in many cases, your CSS-only activities will require many many lines of code, most of which you will have to write by hand.

</details>

## Next step: making a calculator?

The technique that I have described here is exactly the same as the one I used to create the [Arithmetic in Pure CSS](https://merncraft.github.io/calc/) activity that you tried out at the beginning.

<iframe
  id="iframe-arithmetic"
  title="Arithmetic"
  width="300"
  height="150"
  src="https://merncraft.github.io/calc">
</iframe>

It's true that the span "buttons" are a little more discreet there. There's also a little calculation that is done with the values of the custom CSS properties that hold the digit values, and a little trick to show `NaN` if you try to divide by `0`. But you should be able to reverse engineer everything that I did there... and if you get stuck you can always visit the GitHub repo and see all the CSS for yourself.

</section>