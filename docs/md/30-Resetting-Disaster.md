<!-- Resetting Disaster -->
<section
  id="resetting-disaster"
  aria-labelledby="resetting-disaster"
  data-item="Reset Spells Disaster"
>
  <h2><a href="#resetting-disaster">But... Reset Spells Disaster!</a></h2>
  
Ha! Your non-evil twin has missed a trick! Press the Reset button, and the countdown timer continues!

This is because resetting the form resets the state of the `input` elements inside the `<form>`, and this unchecks the radio button, just as if it were a checkbox.

You need something more radical than simply resetting the form. The simplest solution is to reload the whole page, using a link whose `href` is `/`.  Notice that you don't need the `<form>` element any more. Here's the final HTML:

```html
<i><label>
  <input type="radio">
  <span></span>
</label>
<div>It was always too late.</div>
</i><b><<a href="/" draggable="false">Replay</a>
</b>
```

To prevent the link from moving when dragged, just like a button, I've added `draggable="false"`.

Here's the final CSS, where I've replaced the ruleset for `button` with a nested ruleset for `a`, to make the link look as much like a standard button as possible.

```css
<i>body {
  --display: none;
  counter-reset: countdown 10;
  animation: timer 10s step-end forwards paused;
}

body:has(input:not(:checked)) {
  animation-play-state: running;
}

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
  display: var(--display);
}

</i><b>a {
  position: absolute;
  padding: 0.1em 0.2em;
  background-color: #eee;
  border: 1px outset #999;
  border-radius: 0.25em;
  text-decoration: none;
  color: #000;

  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -o-user-select: none;
  user-select: none;

  &:hover {
    background-color: #ddd;

    &:active {
      background-color: #ccc;
      border-style: inset;
    }
  }
}</b><i>

span::before {
  content: "My hero!";
  display: block;
}
span::after {
  content: "You saved us!"
}

input:not(:checked) {
  & ~ span::before {
    content: "Click me! Before it's too late...";
  }

  & ~ span::after {
    content: "We have only " counter(countdown) " seconds left!";
  }
}

@keyframes timer {
   0% { counter-increment: countdown   0; }
  10% { counter-increment: countdown  -1; }
  20% { counter-increment: countdown  -2; }
  30% { counter-increment: countdown  -3; }
  40% { counter-increment: countdown  -4; }
  50% { counter-increment: countdown  -5; }
  60% { counter-increment: countdown  -6; }
  70% { counter-increment: countdown  -7; }
  80% { counter-increment: countdown  -8; }
  90% { counter-increment: countdown  -9; }
 100% { counter-increment: countdown -10;
        --display: flex;
      }
}</i>
```

</section>