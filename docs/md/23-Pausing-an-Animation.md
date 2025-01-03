<!-- Pausing an Animation -->
<section
  id="pausing-an-animation"
  aria-labelledby="pausing-an-animation"
  data-item="Pausing an Animation"
>
  <h2><a href="#pausing-an-animation">Pausing an Animation</a></h2>
  
Instead of `:hover`, you can use the state of a checkbox or a radio button to change the state of an animation. Edit your HTML page so that it looks like this:
```html
<label>
  <input type="radio" name="play-state" id="play">
  <span>Play</span>
</label>
<label>
  <input type="radio" name="play-state" id="pause">
  <span>Pause</span>
</label>
<label>
  <input type="radio" name="play-state" id="stop">
  <span>Reset</span>
</label>

<div></div>
```
Notice that there are three radio buttons which all appear before the `<div>`. These radio buttons share the same `name` property, so only one can be on at a time, but they all have different `id` values.

In your CSS page, comment out the rule for `div:hover::after` and add a new rule for the radio buttons:
```css-#11
/* div:hover::after {
  animation: timer 1s forwards step-end;
} */

input:checked {
  animation: timer 1s forwards step-end;
}
```
There are three radio buttons. If you check any of them, the countdown animation will play. The `<div>` still has a rule that tells its `::after` pseudo-element to display the value of the `counter(countdown)`, but it no longer _owns_ the animation. The animation belongs to whichever radio button was last clicked. The `countdown` counter belongs to the `<body>` element, and the `div::after` element can listen for its current value, because it is a child of the `<body>`, which specifically _appears in the HTML **after** any of the `:checked` radio buttons_.

## Restoring ownership

To give ownership back to the  `div::after` element, you can use the selector below: 

```css-#15
<b>body:has(input:checked) div::after</b><i> {
  animation: timer 1s forwards step-end;
}</i>
```

The selector `body:has(input:checked) div::after` says: "Apply the following rule to any `div::after` element when the `<body>` contains an `<input>` that is `:checked`." All the radio buttons appear before the `<div>` element, so if any of them is checked, the `animation` rule will apply.

And now, with the `body:has(...)` function, it doesn't actually matter whether the `<div>` appears before the radio buttons or after.

Reload your page so that no radio buttons are checked, and then click any one of them. The animation plays to the end, and stops on `0`. Now click on any of the other radio buttons.

Nothing happens.

The rule says: "If any of the radio button `<input>`s  is `:checked`, play the animation. If not, stop the animation." So it doesn't matter which button is checked. They all agree with each other. The `<div>` receives the same message from each radio button: "Go on! Play your animation!" But after the first message, the `<div>` simply shrugs: "I have played it already. I'm good."

What happens if you specify that only the button with an `id` of `play` is to make the animation play? Try this:

```css-#15
<i>body:has(input</i><b>#play</b><i>:checked) div::after {
  animation: timer 1s forwards step-end;
}</i>
```

Now, if you click on the first button, the animation plays to the end. If you click on one of the other buttons, the display reverts to showing `10`.

## Activating the Pause button

Add a ruleset for the `#pause` button, as shown below. **Note that I have reset the duration for both buttons to the same value of `10`, so that you have time to click on different buttons while the animation is in progress.**
```css-#15
<i>body:has(input#play:checked) div::after {
  animation: timer </i><b>10s</b><i> forwards step-end;
}

</i><b>body:has(input#pause:checked) div::after {
  animation: timer 10s forwards step-end;
  animation-play-state: paused;
}</b>
```
The new `input#pause` selector also plays the animation when its button is selected, but it sets the [`animation-play-state`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-play-state) to `paused`. So if you refresh your page and then click the middle radio button, nothing happens.

The CSS elves are in fact busy, but they are busy doing nothing.

If you click on the Play radio button, the animation will start. If you click on the Pause button, it will ... pause. You can continue the animation from this by clicking on the Play button again. Or you can reset the counter to `10` by clicking on the Reset button.

</section>