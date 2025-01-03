<!-- Custom CSS Properties -->
<section
  id="custom-css-properties"
  aria-labelledby="custom-css-properties"
  data-item="Custom Properties"
>
  <h2><a href="#custom-css-properties">Custom CSS Properties</a></h2>

You can also use [custom CSS properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)  to hold numbers. To create a custom CSS property, you use a property name that starts with `--x`, where "x" is any letter.

I've already used a custom CSS property to set the diameter of the circles in the last example:
```css-#
label span {
  --size: 20vh;
  display: block;
  width: var(--size);
  height: var(--size);
  border-radius: var(--size);
  /* all other lines skipped */
}
```
A custom property lets you define a value once, and use it in many places. It helps you follow the DRY principle: Don't Repeat Yourself. If you decided that you wanted circles of a different size, you could simply change the value of `--size`, in just one place, and the `width`, `height` and `border-radius` properties would all adjust their values.


<details class="note" open>
<summary>My Opinion on the Term "~~CSS Variables~~"</summary>
Some people use the term `CSS variables` as a synonym for custom properties. But I don't.

In a programming language, a _variable_ can have various values at different times. And so can custom properties. But:

- A custom CSS property is often reset to its initial value, as you will see in a moment
- You can't display the value of a custom CSS property in the `content` property of a `::before` or `::after` element
- A custom CSS property cannot be used recursively, to reset its value to a value calculated from itself, as the next demonstration shows.

In JavaScript, you can do this, and the JavaScript elves know how to handle it:
```javascript-#
var x = 1
x = x * 2
```
After these two lines of code have been executed, `x` will have the value `2`.

In CSS, you can set a custom property to a different value. This works fine:
```css-#
label span {
  --size: 25vh;
  --size: 15vh;
  display: block;
  width: var(--size);
  height: var(--size);
  border-radius: var(--size);
  /* more lines skipped */
}
```
But in the snippet below, the second rule causes the CSS elves to panic, as if they see themselves in an [infinity mirror](https://en.wikipedia.org/wiki/Infinity_mirror). They simply stop working for you.
```css-#
<i>label span {
  --size: 25vh;
  --size: </i><b>calc(0.6 * var(--size))</b><i>;
  display: block;
  width: var(--size);
  height: var(--size);
  border-radius: var(--size);
  /* more lines skipped */
}</i>
```
Try both of these changes in the clicking-on-circles exercise that you have just done. 

Custom CSS properties do not behave like variables do in other languages. So _I_ always say "custom CSS ***properties***", to make this distinction clear. But if you call them "CSS variables", if you want to. I won't say anything. I'll just sigh.

Here is the official explanation of this, without any reference to CSS elves: [Resolving Dependency Cycles](https://www.w3.org/TR/css-variables-1/#cycles)

</details>

</section>