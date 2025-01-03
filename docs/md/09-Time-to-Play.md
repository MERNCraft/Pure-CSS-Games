<!-- Time to Play -->
<section
  id="time-to-play"
  aria-labelledby="time-to-play"
  data-item="Time To Play"
>
  <h2><a href="#time-to-play">Time to play: counting clicks</a></h2>

If all this makes sense to you, the perhaps you'd like to create a really simple activity. (If it doesn't make sense, then you can go back and read the links that I provided for each new concept, and you try to make different mistakes to irritate your browser, until you can work out what rules it really wants you to follow.)

This time, you can leave lists behind, and count checkboxes directly.

You can create an new HTML file and give it these elements:
```html
  <label>
    <input type="checkbox">
    <span></span>
  </label>
  <label>
    <input type="checkbox">
    <span></span>
  </label>
  <label>
    <input type="checkbox">
    <span></span>
  </label>
  
  <p>You have clicked on <span>/</span> circles.</p>
```

Attach a CSS stylesheet with the following rules:

```css
body {
  background-color: #222;
  color: #ddd;
  counter-set: total;
}

label span {
  --size: 20vh;
  display: block;
  width: var(--size);
  height: var(--size);
  border-radius: var(--size);
  background-color: gold;
  opacity: 0.25;

  counter-increment: total;
}  

input:checked ~ span {
  opacity: 1;
}

p span::before {
  content: "0"
}

p span::after {
  content: counter(total)
}
```

## Make a prediction

Before you launch your new web page, do your best to predict what you will see:

- Each `<label>` contains both a checkbox and a `<span>`. This means that the `<span>` is part of the  `<label>`, and a click on this `<span>` inside the  `<label>` will toggle the checkbox.
- The [`~` sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Subsequent-sibling_combinator) in the selector `input:checked ~ span` selects a span only when a preceding `<input>` sibling has been checked. When a checkbox is checked, the `opacity` of the associated gold circle will be set to `1`. When the checkbox is not checked, the gold circle will appear dim.
- There are different rulesets for the  `<span>` elements inside a `<label>` and for  the `<span>` inside the  `<p>` element. This is because they are used for different purposes.
* The [custom CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties) `--size` allows you to set one value that is used for the `width`, `height` and `border-radius` of all the `<span>` elements which are inside `<label>` elements. This means that the `<span>`s will be round. 
* There is a `counter` called `total` which starts with a default value of `0`. Each `<label>` element increments this value by the default increment of `1`. There are three `<label>` elements, so the final value of `total` should be 3.
* The `<span>` inside the `<p>` element contains only a `/` slash, but the CSS adds both `::before`  and `::after` pseudo-elements to it.

You should see three pale gold circles, each with a checkbox at its top left, and text at the bottom of your page should say: "You have clicked on 0/3 circles." You can click on the checkboxes and circles as much as you like. After the first click on any of the circles, it will become brighter, but the final sentence will not change.

![Two circles clicked... but the text doesn't update](images/0-circles.webp)

The value `3` appears because of this rule:
```css-#27
p span::after {
  content: counter(total)
}
```

<details class="challenge" open>
<summary>Add another counter</summary>
Can you imagine how to add another `counter` that will count how many `<input>` elements have been checked? Can you imagine how to display  the value of this new `counter` in the `::before` pseudo-element of the `<p>` element?

Can you do it on your own, without reading the solution below?

<details class="solution">
<summary>Solution</summary>

Here are the lines of CSS that I changed or added in my version, in order to make this feature work:

```css
<i>body {
  background-color: #222;
  color: #ddd;
  counter-set: total </i><b>clicked</b><i>;
}</i>
```
```css-s
<!-- lines skipped -->
```
```css-#23
<i>p span::before {
  content: </i><b>counter(clicked)</b><i>
}

p span::after {
  content: counter(total)
}
</i><b>
input:checked {
  counter-increment: clicked;
}</b>
```
![Detecting how many circles were clicked](images/2-circles.webp)  


Now when you click on a gold circle, or on its checkbox, the number shown in the `::before` pseudo-element changes.

</details>
</details>

<details class="note" open>
<summary>More than one counter declaration?</summary>
You might think that declaring each `counter` on a different line might be valid CSS...
```css-#
body {
  counter-set: total;
  counter-set: clicked;
}
```
... and it _is_ valid, but it doesn't behave the way you might expect. The second `counter-set` property overwrites the first, so `counter-set: total;` will be ignored.

This is the way CSS works for all other properties. In this ruleset...
```css-#
label span {
  background-color: gold;
  background-color: silver;
}
```
... the `silver` background will overwrite the `gold`, just as you would expect.

If you want to declare different `counter` properties on different lines, just use a single semicolon at the end of the multi-line rule:
```css-#
body {
  counter-set:
    total
    clicked;
}
```

</details>
</section>