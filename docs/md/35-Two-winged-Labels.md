<!-- Two winged Labels -->
<section
  id="two-winged-labels"
  aria-labelledby="two-winged-labels"
  data-item="Two-winged Labels"
>
  <h2><a href="#two-winged-labels">A Label with Two Wings</a></h2>

<details class="tip" open>
<summary>Keeping it small</summary>
Whenever I am working in a big project and I come across a new problem, I create a new baby project to test my ideas and make all the mistakes I need to find a solution to this new problem. When I finally understand what I am doing, then I go back to the big project and apply my new solution.

Treating a new problem in isolation frees up your mind and makes it much easier to think in new ways.

</details>

So. New problem. New HTML and CSS files. You know the drill. "Plus and Minus" might be a good name for your project folder.

Here's some HTML to get you started.

```html
  <label class="d0">
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
  <!-- Something is missing here -->
  <span class="display"></span>
```

<details class="question" open>
<summary>Reading the code</summary>
Take a good look at it and see if you can make sense of all the labels, inputs and spans. Why does each label have two spans?

</details>

## Here's how the HTML looks in a browser.

![What the HTML shows](images/minusAndPlus.webp)

This short extract only gives you three labels. They have radio buttons with the `id`s `d0`, `d1` and `d9`, but this is enough for you to check if this creates some kind of cycle. You can add more labels with the same structure later.

Each label has two spans: one with the class `"minus"`, one with the class `"plus"`.

<details class="challenge" open>
<summary>Showing the right spans</summary>
Suppose `<input id="d1">` is checked.

Can you write a CSS rule that will show _only_:

* The `.minus` span for inside the `<label class="d0">`
* The `.plus` span for inside the `<label class="d2">`?

Note that if any child of `<label class="dX">` is clicked, the associated `<input id="dX">` will become checked.

<details class="solution">
<summary>Solution</summary>
Here is the strict minimum that you need:

```css
label span {
  display: none;
}
body:has(#d1:checked) {
  .d0 span.minus { display: block }
  .d2 span.plus { display: block }
}
```

**Note that I have used `label span` for the first selector, and not just `span`. because I don't want to hide `span.display`.

This is what it will look like **if you check the checkbox for `#d1`**:

![input#d1 is checked. Visible: the minus span for .d0, the plus span for .d2](images/plus-minus.webp)

If you click either the `–` or the +, a different checkbox will be checked, and the  `–` and the + will disappear.

</details>
</details>

## Not just cosmetic

I'm going to suggest, _as a hint that you can use later_, that you make the `-` and `+` elements bigger.

```css-#11
span {
  --size: 64px;
  font-size: var(--size);
}
```


## Showing the value

The HTML I gave you includes this: `<span class="display"></span>`, but nothing is displayed in this span yet. I think you can guess that it's meant to display a digit.

Perhaps, if you think about it, this digit could a `counter` used in a `content` declaration?

You could add a line to the ruleset for the `#d1:checked` button, and a new rule for the `span.display`:
```css-#5
<i>body:has(#d1:checked) {
  </i><b>counter-set: digit 1;</b><i>
  .d0 span.m { display: block }
  .d2 span.p { display: block }
}

span {
  --size: 64px;
  font-size: var(--size);
}

</i><b>span.display::after {
  content: counter(digit)
}</b>
```
This would work. It would definitely work. But there's a problem.

CSS won't let you _read_ the value of a `counter`, except to display it in a `::before` or `::after` element.

<details class="question" open>
<summary>A different solution?</summary>
Is there a different CSS property that you could set... and then display the value of this different property?

Hint: how did I set the _size_ of the spans that show the `–` and  `+` buttons?

</details>

How about this:

```css
<b>body {
  /* Declare a custom property and use it to set a counter */
  --counter: 0;
  counter-set: digit var(--counter);
}</b><i>

label span {
  display: none;
}

body:has(#d1:checked) {
  </i><b>/* Set the custom property to a new value */
  --counter: 1;</b><i>
  .d0 span.minus { display: block }
  .d2 span.plus { display: block }
}</i>
```

Custom properties have the advantage that they can be read from any child of the element in which they are declared. They can even be read by JavaScript. Try this in the Developer Console:

```javascript
getComputedStyle(document.body).getPropertyValue("--counter")
```

![getPropertyValue("--counter")](images/getPropertyValue.webp)

<details class="tip" open>
<summary>JavaScript in custom CSS properties</summary>
And if you are _really_ sneaky, you can even store JavaScript code inside a custom CSS property. The [official specifications for Custom Property Value Syntax](https://www.w3.org/TR/css-variables-1/#syntax) explicitly requires browsers to make this possible. ( See "EXAMPLE 7")

</details>

## The trick

You can't _show_ the value of a custom property directly, but if it is a number, then you can use it with `counter-set`, and then get a _`counter`_ to display it for you.

</section>