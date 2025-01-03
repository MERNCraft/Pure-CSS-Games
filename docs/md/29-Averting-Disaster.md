<!-- Averting Disaster -->
<section
  id="averting-disaster"
  aria-labelledby="averting-disaster"
  data-item="Averting the Disaster"
>
  <h2><a href="#averting-disaster">Averting the Impending Disaster</a></h2>
  
My story needs two more elements to make it even a little bit interesting:

1. An indication that the end is coming
2. An action that will stop the animation.

You can use the `counter(countdown)` to indicate how much time is left:
```css-#39
input:not(:checked) {
  & ~ span::before {
    content: "Click me! Before it's too late...";
  }

  & ~ span::after {
    content: "We have only " counter(countdown) " seconds left!";
  }
}
```
The selector `input:not(:checked)` adds greater specificity to the selector that acclaims the hero (`span::before`), so the span will show this text as long as the checkbox is not clicked.

But `counter(countdown)` starts at `0` and then goes negative. How can you get it to start at `10`? You'll need to add the following rule:

```css
body {
  --display: none;
  counter-reset: countdown 10;
  animation: timer 10s step-end forwards;
}
```

With this rule the countdown will be shown, and at `0`, the "It was always too late" message will be shown.

However, if you click on the button to stop it, you just bring the end closer. That's because of the rule you added a while back. It's time to remove this:

```css-#29
/* body:has(input:checked) {
  --display: flex;
} */
```

Now, if you click (anywhere) the checkbox will be checked, and you will be praised as a hero.

<details class="challenge" open>
<summary>Unavoidable disaster?</summary>
But... wait for the 10-second countdown to end, and **the terrible red message will appear anyway**.

You need to stop the animation.

Only you can do this. _You_ are the hero.

You need to tell the `<body>` to pause the animation when the checkbox is checked.

And here comes the twist in my story. You are not the hero after all. You just set up the situation so that you can _look_ like the hero.

Does that give you a clue as to how to solve this?

You need to set the `animation-play-state` to `paused` by default, and only set it to [whatever the opposite of `paused` is](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-play-state) while the checkbox is _not_ checked. This means that you need to create a selector that selects the `<body>` only if the checkbox is not checked.

<details class="solution">
<summary>Your secret Bond-villain plan</summary>

Here's one way to _look_ like a hero:

```css
<i>body {
  --display: none;
  counter-reset: countdown 10;
  animation: timer 10s step-end forwards </i><b>paused</b><i>;
}</i>
```
You make the world safe. And _then_ you create the sense of danger with this new rule:
```css-#7
body:has(input:not(:checked)) {
  animation-play-state: running;
}
```

And since you are now the villain, you can deselect the checkbox again, and let countdown continue. You can both save the world and let the end come anyway. 

Yes, but while you were doing this, the real hero (played by your non-evil twin) crept unseen into the HTML file and changed the `type` of the `<input>` from `"checkbox"` to `"radio"`. Once a solitary radio button is checked, it cannot be unchecked. The good guys win again!

One person can save the world!

```html
<i><form>
  <label>
    <input type="</i><b>radio</b><i>">
    <span></span>
  </label>
  <div>It was always too late.</div>
  <button type="reset">Reset</button>
</form></i>
```

</details>
</details>

</section>