<!-- Set Starting Value -->
<section
  id="set-starting-value"
  aria-labelledby="set-starting-value"
  data-item="Set Starting Value"
>
  <h2><a href="#set-starting-value">Setting a starting value for a counter with a custom property</a></h2>

To explore how custom CSS properties can interact with counters, create a new HTML file with the following body:
```html-#
  &lt;b&gt;&lt;/b&gt;
  <p>Tinker</p>
  <p>Tailor</p>
  <p>Soldier</p>
  <p>Sailor</p>
  <hr>
  <label>
    Add 10: <input id="add10" type="checkbox">
  </label>
  <label>
    Add 100: <input id="add100" type="checkbox">
  </label>
  <label>
    Add 1000: <input id="add1000" type="checkbox">
  </label>
```

<details class="challenge" open>
<summary>Write your own CSS</summary>
Here's a challenge: Before you read on, can you use everything you have learnt so far about CSS counters to write the CSS that will make your page look like this?

![What your page should look like](images/property-layout.webp)

<details class="solution">
<summary>Solution</summary>
Are you ready now? Or are you being disruptive, like I suggested you should be?

Did you write something like this?
```css
body {
  counter-reset: item 
}

b::before {
  content: "—[" counter(item) "]—";
}

p {
  counter-increment: item;
}

p::before {
  content: counter(item) ": ";
}

label {
  display: block;
}
```
I imagine that:

- You chose a different name for your counter
- You might have given it an initial value and an explicit increment value
- Your rules might be in a different order.

That's good. It means that you won't be able to simply copy and paste the CSS that I provide below. You'll have to adapt it to work with your property names. You'll have to make an effort. 😈

</details>
</details>

### Activating the inputs

To activate the checkboxes, can you do these three steps?

1. Add a custom CSS property to the ruleset for the `body` selector, and set its value to `0`. Below, I've used the name `--start`, but you can use whatever name you like.
2. Use your custom CSS property as the initial value for your counter.
```css-#
/* Create a CSS property and use it to initialize the counter */
body {
  --start: 0;
  counter-reset: item var(--start);
}
```
3. Add three new rules that will change the value of your custom CSS property.
  **Note that I have placed the rule for the  `#add1000` input first. Please do the same, even if you are feeling disruptive. You'll see why in a moment.**
```css-#
/* Use the checkboxes to change the value of --start */
body:has(#add1000:checked)  {
  --start: 1000
}

body:has(#add10:checked)  {
  --start: 10
}

body:has(#add100:checked)  {
  --start: 100
}
```
Notice that I have wrapped  the reference to the `<input>` elements with the new [`:has(...)` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:has). Basically, this says: "if the `body` has a checked input, then set the value of `--start` for the `body` and all its children". 

<details class="question" open>
<summary>Why use `:has()?`</summary>
What would happen if you don't use the `:has()` pseudo-class, like this?
```css-#
#add100:checked  {
  --start: 100
}
```

The rule above would say: "Set the value of `--start` for `input#add100` and all its children." But `<input>` elements don't have any children, so the value of `--start` would change only for the `<input>` itself, and the `<input>` itself ignores it. So nothing would happen.

</details>

## Testing what the checkboxes do

Refresh your page, and then click on each of the checkboxes in turn. You should see the numbers change. Do they change the way you would expect them to?


<iframe
  id="iframe-custom-properties"
  title="Custom Properties"
  width="150"
  height="300"
  src="https://merncraft.github.io/CSS_properties/">
</iframe>

When you check Add 10, you should see `——[10]——`.
If you check both Add 10 and Add 100, you should see `——[100]——`, not `110`
And if you check Add 1000 _on its own_, you should see `——[1000]——`.

But if you check Add 1000 _and one of the other checkboxes_, you do **not** see `——[1000]——`. You see `——[100]——` or `——[10]——` instead.

![Setting --start with a checkbox](images/add-to-start.webp)  

If you see something different, then check that your rule for `#add1000` does indeed appear first in your CSS file, as it does in my code listing above.

## Order _does_ matter in CSS

I deliberately placed the rule for `#add1000` first, so that you can see that the order in which the CSS rules are written **does** matter when you set the value of custom CSS property. Even if you change the order of the `<input>` elements in the HTML file, as shown below, **the order of the CSS rules still takes priority**.
```html-#
  <label>
    Add 1000: <input id="add1000" type="checkbox">
  </label>
  <label>
    Add 100: <input id="add100" type="checkbox">
  </label>
  <label>
    Add 10: <input id="add10" type="checkbox">
  </label>
```
Try it and see.

</section>