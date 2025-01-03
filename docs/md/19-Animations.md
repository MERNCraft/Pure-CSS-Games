<!-- Animations -->
<section
  id="animations"
  aria-labelledby="animations"
  data-item="Animations"
>
  <h2><a href="#animations">Animations</a></h2>

The easiest project for exploring how CSS animations work with CSS counters is a countdown timer. Here's the kind of thing you'll be creating in this exercise (with some extra contral buttons):


<iframe
  id="iframe-countdown"
  title="Countdown"
  width="300"
  height="300"
  src="https://merncraft.github.io/10s-timer">
</iframe>


For this new topic, you can create a new folder with the name "Countdown" and create inside it an HTML file and a linked CSS file. Here's enough HTML to get started:
```html
<div></div>
```
Here is some equally minimal CSS:
```css
body {
  counter-set: countdown 10;
}

div::after {
  content: counter(countdown);
  font-size: 256px;
}
```
<details class="note" open>
<summary>Connecting HTML and CSS</summary>
I'm assuming that you know how to create an HTML page with a linked CSS file, so that you can get this to work for you. If not, click on the GitHub octocat logo in the demo above, and check out how it works.

</details>

The `font-size` is not strictly necessary, but it makes the display more dramatic. Your page should now show a big number `10`.

## The `@keyframes` at-rule

CSS Animations are defined by a [`@keyframes`](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes) at-rule. Here is a rule that creates an animation with the name `timer`:
```css-#10
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
 100% { counter-increment: countdown -10; }
}
```
You can add this at the end of your CSS file.

<details class="tip" open>
<summary>Hacking with Emmet</summary>
Note that I did not type all of this out by hand. I used a hack. My code editor is VS Code, and this comes with a built-in plug-in called Emmet. ([Emmet](https://www.etymonline.com/search?q=emmet) is an old or dialectical word for [ant](https://www.etymonline.com/word/ant).) Emmet provides shortcuts for HTML and CSS code that you might need to type regularly. As of the time of writing, it does not provide shortcuts for generating CSS keyframe animations. So I cheated. I used a shortcut for creating a series of HTML elements with incrementing values. I typed this in my HTML page...

```html
div{ $% counter-increment: countdown -$ }*10
```
... and then pressed Enter. (Tab also works.) This produced the following output:
```html
<div> 1% counter-increment: countdown -1 </div>
<div> 2% counter-increment: countdown -2 </div>
<div> 3% counter-increment: countdown -3 </div>
<div> 4% counter-increment: countdown -4 </div>
<div> 5% counter-increment: countdown -5 </div>
<div> 6% counter-increment: countdown -6 </div>
<div> 7% counter-increment: countdown -7 </div>
<div> 8% counter-increment: countdown -8 </div>
<div> 9% counter-increment: countdown -9 </div>
<div> 10% counter-increment: countdown -10 </div>
```
The [curly `{}` brackets](https://docs.emmet.io/abbreviations/syntax/#text) define the text that I want to appear inside the HTML element, [the dollar `$` sign](https://docs.emmet.io/abbreviations/syntax/#item-numbering) is replaced by a line number and the [multiplication `*` sign](https://docs.emmet.io/abbreviations/syntax/#multiplication) tells Emmet how many elements I want.

The output is not exactly what I want, but I then used VS Code's built-in [multi-cursor selection](https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_multi-cursor-selection) to quickly remove the parts that I did not want, to add curly `{}` brackets where I did want them, and to add a `0` between the numbers on the left and the following percentage `%` sign.

</details>

<details class="note" open>
<summary>Absolutely not a loop</summary>
Notice that each keyframe deducts a bigger number from `countdown` than the previous keyframe. This reveals a critical difference between the way CSS applies a variety of rules to a static page, compared with the way JavaScript can apply loops and variables to create an endless range of possibilities.

In JavaScript, you could reduce the value of a variable by `1` on each iteration through a loop. In CSS, each time a new keyframe uses `counter-increment` to change the value of the `countdown` counter, it does this with reference to the initial value of `10` that is set by this rule for the `<body>` element:
```css
body {
  counter-set: countdown 10;
}
```
Or to put it another way, CSS starts from the original static HTML page each time, and applies its rules in the appropriate order. There is never any question of looping. 

</details>

## The independence of `@keyframes`

An `@keyframes` rule simply gives instructions on what should change at what point in the animation. It does not give any information on which element this animation should be applied to, or how fast it should run or whether it should repeat, or a number of other things.

## Playing an animation

To get the countdown timer to work, you can add a single line to your CSS. This provides details that are not included in the `@keyframes` at-rule itself:
```css-#5
<i>div::after {
  content: counter(countdown);
  font-size: 256px;
  </i><b>animation: timer 10s forwards;</b><i>
}</i>
```

This new line says:

- Apply the animation named `timer` to the element identified by `div::after`
- Play the animation over the span of [`10s`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-duration)
- When the animation reaches the end, don't rewind. Just play it [`forwards`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode).

The animation should start as soon as you load the page, and continue until the counter shows a big `0`. The word `forwards` is one of the values of the [`animation-fill-mode`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode) property. It tells the CSS elves to leave everything the way they were told to by the last keyframe they read.

## Transition between frames

Reload the page to restart your animation. 

<details class="env" open>
<summary>Hard refresh in Firefox </summary>
In Firefox, when you simply refresh a page, Firefox remembers the state of all your checkboxes, radio buttons, details elements and so on, and restores their state after refreshing the page. To clear all these states, you need to use a _hard refresh_, which also clears the cache.

The keyboard shortcut for this, for all common browsers, is `Ctrl-Shift-R` (or `Command-Shift-R` if you're working on a Mac.)

</details>

Do you notice that the step from `10` to `9` plays faster than the following steps? This is because, by default, CSS applies a _transition_ between each keyframe. If the property that the animation changes can have intermediate values, then the animation will move it smoothly from one keyframe to the next.

However, the value of your `counter` changes by a whole integer at each step. There are no intermediate values. With the default settings, the CSS elves get half-way towards the next keyframe and they think: "We're closer to next waypoint now. Let's change already!" As a result, with your counter, the changes happen after 0.5s, 1.5s, 2.5s, and so on. That's why the change from `10` to `9` happens faster than you would expect.

You will see how to fix this in the coming sections.

<details class="note" open>
<summary>What's key about a keyframe?</summary>
The word _keyframe_ is used to refer the precise values to use at precise times. The browser will interpolate other (non-key) frames between each keyframe. 

</details>

</section>