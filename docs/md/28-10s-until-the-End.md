<!-- s until the End -->
<section
  id="the-end-is-near"
  aria-labelledby="the-end-is-near"
  data-item="The End is Near"
>
  <h2><a href="#the-end-is-near">Ten Seconds until the End</a></h2>
  
Actually, so far you have created the exact opposite of the story I want to tell. I want to create a countdown where clicking this button will _stop_ the red message from appearing. This is the ending I want your triumphant player to see:
```css-#32
span::before {
  content: "My hero!";
  display: block;
}
span::after {
  content: "You saved us!"
}
```
You can use the same countdown timer that you used in the last exercise, with one little difference...
```css-#39
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
}
```
Instead of making the little harmless `0` turn red, this will turn the whole page red, as `--display` is set to `--flex` on the last keyframe.

If you add this to your CSS file, nothing will happen... yet. First you have to start the animation.

<details class="challenge" open>
<summary>Where to add an `animation` rule</summary>
Here's a question for you. The following rule will start the animation. Which element should it be applied to?

```css-#
animation: timer 1s step-end forwards;
```
I've used a very short duration (`1s`) for now, so that you will see immediately if the animation is working or not. Remember, the final value of `--display` needs to be applied to the `<div>`.  Would this work?

```css-#18
<i>div {
  </i><b>animation: timer 1s step-end forwards;</b><i>
  background-color: #900;
  display: var(--display);
}</i>
```
You can try it. You can try putting the new `animation` rule at the end of the ruleset. But, no, it doesn't work.

It's not crystal clear why not. The official documentation talks about  ["animation-tainted" custom properties](https://www.w3.org/TR/css-variables-1/#animation-tainted), and discussions on the [W3C GitHub Issues pages](https://github.com/w3c/csswg-drafts/issues/411#issuecomment-890081098) show just how complex the interaction of custom variables and keyframe animations is. I use the principle of [Occam's Razor](https://www.newscientist.com/definition/occams-razor/) here. To paraphrase: if it doesn't work, don't look for anything more complex. Find a simple solution that does work.

<details class="solution" >
<summary>Solution</summary>
What happens if you apply the animation to the `<body>`instead?
```css
<i>body {
  --display: none;
  </i><b>animation: timer 1s step-end forwards;</b><i>
}</i>
```
Now the animation works. Now that you know that, you can set its duration to `10s` to give yourself time to stop the animation before it ends in tragedy.

</details>
</details>

</section>