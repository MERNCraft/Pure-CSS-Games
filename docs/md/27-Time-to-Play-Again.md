<!-- Time to Play Again -->
<section
  id="time-to-play-again"
  aria-labelledby="time-to-play-again"
  data-item="Time To Play Again"
>
  <h2><a href="#time-to-play">Time to play:  A Race Against Time</a></h2>
  
I want to use CSS to tell a story of how one person can save the whole ~~world as we know it~~  browser from a ~~terrible~~ simulated threat, by clicking on a button, in a race against time.

You can play this mini game below. The chances are that it's already game over for you by the time you have read this far, but you can simply click on the Replay link:

<iframe
  id="iframe-countdown"
  title="Countdown"
  width="300"
  height="150"
  src="https://merncraft.github.io/countdown">
</iframe>

## Creating your own version of the game

Create a new HTML file with a linked CSS file. Here's the HTML that you can use:
```html
  <form>
    <label>
      <input type="checkbox">
      <span></span>
    </label>
    <div>It was always too late.</div>
    <button type="reset">Reset</button>
  </form>
```
You can make both the `label` and the `div` fill the entire browser viewport, with the `div` in front:
```css
label,
div {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 7vmin;
}

div {
  background-color: #900;
}
```
The text "It was always too late" should now appear in dramatic black characters on an ominous red background. The mini-game that you can create will give the player the chance to prevent this terrible news from appearing.

The `<label>` with a transparent background is hidden behind this. However  Reset button is also hidden behind the `<div>`, because of the use of `position: fixed`, which creates a new [stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context). To raise the button above the `fixed` elements, you have to give it a `position` other than `relative` or `static`:
```css-#19
button {
  position: absolute;
}
```
#### Hiding and showing the message of doom

To hide the red `<div>` you can set its `display` to `none`. But you don't need to do this directly. You can use a custom CSS property with the value of `none`. Add a new rule, and a new line to the ruleset for the `div`:
```css
<b>body {
  --display: none;
}</b><i>

label,
div {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 7vmin;
}

div {
  background-color: #900;
  </i><b>display: var(--display);</b><i>
}

button {
  position: absolute;
}</i>
```
You should now see a little lonely checkbox in the centre of your page. If you click on it, it becomes selected but nothing else happens. You can add a rule to change the value of the `--display` custom property. **This is not the rule that you are looking for**:
```css-#27
input:checked {
  --display: flex;
}
```
You can try it anyway, but it won't work. Why not?

Which element is this custom property applied to? Which element _should_ it be applied to, so that the `div` rule can use it?

Try this instead:
```css-#27
<b>body:has(input:checked)</b><i> {
  --display: flex;
}</i>
```
Do you see the difference? In the first rule, `--display` was set for the `<input>` element. The `<div>` is not a child of the `<input>` element, so it cannot inherit the value of `--display`.

In fact, `<input>` elements cannot have any children. They are written with a single self-closing tag, so there is nowhere for a child to be added. And for this reason, they cannot have `::before` or `::after` pseudo-elements either. That's why I added an empty `<span></span>` element inside the label. A `<span>` _can_ have children —and `::before` and `::after` pseudo-elements— and that's good because that's what I'll use for the storytelling.

The second rule, which uses the [`:has()`](https://developer.mozilla.org/en-US/docs/Web/CSS/:has) pseudo-class, allows me to select the `<body>` element, only if there is an `<input>` which is `:checked` as one of its children. When you check the checkbox, the _`<body>`_ gives its `--display` custom property the new value of `flex`, and the `<div>` is a child of the `<body>`, so it inherits this new value. And the red message fills the screen.

You can click on the Reset button to make it disappear again.

</section>