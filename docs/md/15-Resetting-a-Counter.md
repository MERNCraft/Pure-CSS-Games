<!-- Resetting a Counter -->
<section
  id="resetting-a-counter"
  aria-labelledby="resetting-a-counter"
  data-item="Resetting A Counter"
>
  <h2><a href="#resetting-a-counter">Resetting A Counter</a></h2>

As you have just seen, you can set a `counter` to a value given by a custom CSS property. If you change the value of the custom CSS property, the values of all the counters will be recalculated.

But you can also use `counter-set` explicitly anywhere in your CSS. Will there be a conflict of interests? Who will win? The custom CSS property or the value given by `counter-set`?

Here's how you could test this.

1. Add a new line to your HTML:

```html
  <p>Tinker</p>
  <p>Tailor</p>
  <b class="resetter"></b> <!-- new line -->
  <p>Soldier</p>
  <p>Sailor</p>
```

2. Replace your current rule for `body` with these two rules... which may or may not be in a logical order. (That's what we want to find out.)
```css
<b>b.resetter {
  counter-reset: item 9999;
}</b>

<i>body {
  counter-reset: item var(--start);
  --start: 0;
}</i>
```
```css-s
/* The following lines do not change */
```

3. Refresh your page. You should see something like this.

<iframe
  id="iframe-reset-counter"
  title="Reset Counter"
  width="150"
  height="300"
  src="https://merncraft.github.io/reset_counter/">
</iframe>

4. Notice that the item number for `Soldier` is `10000` (`9999 + 1`), and that this value does not change when you check any of the checkboxes, although the numbers for the paragraphs before the `b.resetter` element do change.

![counter-reset takes priority over custom properties](images/counter-set.webp)

In the screenshot above, the custom CSS property `--start` is set to `100`, and this determines what value the `item` counter has, until the `<b class=resetter>` element is displayed. At this point, the rule...
```css-#
b.resetter {
  counter-set: item 9999;
}
```
... is applied, and the initial value set by the custom CSS property `--start` is forgotten. Once again, it is the order of elements _in the HTML source_ that decides what value a `counter` will have at any particular point.

To summarize:

- When you use CSS to alter the value of a custom CSS property, it is the precedence in the CSS which determines the value
- When you use CSS to alter the value of a CSS counter, it is the order of elements in the HTML file which determines the value.

This is, in fact, logical, but it can be confusing.

</section>