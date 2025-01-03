<!-- Running Backwards -->
<section
  id="running-backwards"
  aria-labelledby="running-backwards"
  data-item="Running Backwards"
>
  <h2><a href="#running-backwards">Running an Animation Backwards</a></h2>

If you've got to this sections, I'll assume that you have solved the challenges in the last section, or have worked through the solutions that I proposed.

So now, if you deselect the checkbox, the display jumps back immediately to showing `Hi`. There's no reverse animation.

<details class="tip" open>
<summary>Playing animations smoothly in reverse</summary>
[Nikola Đuza at Pragmatic Pineapple](https://pragmaticpineapple.com/smoothly-reverting-css-animations/) has some good suggestions on how to make animations play smoothly in reverse, but none of them are helpful here.

</details>

If you look at the documentation for [`animation-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-direction), you'll see that one of the options for the value is `reverse`. You might think, like I did, that it would be easy to use this value with the `@keyframe` animations that you have already created. After trying, trying and trying this again and again, it seems that I can't force browsers to change the `animation-direction` of an animation that has already been applied. I have had to use a more brute-force solution. (If you find a better one, [let me know](https://github.com/MERNCraft/css-only-games-1/issues/new).

My solution was to make an exact copy of  my `@keyframes letter-1` and  `@keyframes letter-2` animations. I called them  `@keyframes letter-3` and  `@keyframes letter-4`. (I won't show them here, because they are exactly the same as the animations you can find in the solution to the last challenge, just with different names.)

I added the rule below to my CSS. Notice the word `reverse` used to set the `animation-direction`.
```css-#95
body:has(input:not(:checked)) {
  span::before {
    animation: letter-3 2.0s linear reverse forwards;
  }
  span::after {
    animation: letter-4 1.6s linear reverse forwards;
  }
}
```
You can restore the original values for `counter-set` (`8` and `9`), and try this for yourself.

## An unwanted side effect

You'll see that it has an unwanted side effect. Because the checkbox `<input>` starts off unchecked, this `reverse` animation _plays immediately after the page is loaded_.

What you need is a third state, which will not trigger any animations at the start.

<details class="question" open>
<summary>body:has(input...)</summary>
Did you notice that my earlier selector was simply `body:has(:checked)`, but this selector includes `input`?

```css
body:has(input:not(:checked))
```

If you don't include `input`, the animation triggered by the first selector you added will not run.

You might think that adding `input` increases the [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) of this second selector, but that's not the reason. The selector `body:has(:not(:checked))` means that if _any_ element does not have a `:checked` pseudo-class (**even elements that do not ever receive a `:checked` pseudo-class**), then this selector will apply to the `<body>` element.

If you place this rule after the previous one, it will take precedence because it is read later from the CSS file. You _could_ use this less specific selector and put it _before_ the one you added first, but a co-worker might think that logically it should be placed after, and move it, and break your CSS.

By adding the `input` element into the selector, you tell CSS to ignore any other kind of elements that have no `:checked` pseudo-class. Now your co-worker can reorder your rules in the CSS file and they will still work.

An alternative would be to add `input` only to your _first_ selector . Try this:
```css
body:has(input:checked) {
  span::before {
    animation: letter-a 0.6s linear forwards;
  }
  span::after {
    animation: letter-b 1.0s 0.6s linear forwards;
  }
}

body:has(:not(:checked)) {
  span::before {
    animation: letter-3 2.0s linear reverse forwards;
  }
  span::after {
    animation: letter-4 1.6s linear reverse forwards;
  }
}
```

You see? This also works, and this time [it _is_ because of specificity](https://specificity.keegan.st/). Perhaps the best solution is to use `input` in both selectors, so that your co-workers can't complain of you taking confusing shortcuts.

</details>

## Preventing the unwanted animation on page load

So back to the question: How can you stop the reverse animation from playing automatically when the page is loaded? Can you think of any three-state solutions? There's a hint in the subtitle below.

See if you can find a solution for yourself before you read on.

### Radio buttons are off by default

In your HTML file, replace the single checkbox with these two radio button:

```html
  <b>label>
    <input type="radio" name="play" id="well">
    Well
  </label>
  <label>
    <input type="radio" name="play" id="good">
    Good
  </label></b>
  <i><span></span>!</i>
```

Both buttons share the same `name` property, so only one can be _on_ at any given time. Two states. But... both buttons can be _off_ when the page is first loaded. Two buttons with a third state, for free!

So what CSS would you use with this? Notice that the radio buttons have different `id` values. Comment out your existing rules for `body:has(...)` (so that they don't also get triggered) and add this new one:

```css-#130
body:has(#well:checked) {
  span::before {
    animation: letter-1 2.0s linear forwards;
  }
  span::after {
    animation: letter-2 1.6s linear forwards;
  }
}
```
This is how your page should look immediately after it's loaded. There shouldn't be any animation.

![No checked radio buttons, no animation](images/well-hi.webp)


And this is how it should look after your check the Well button, and after the animation has finished.

![The Well radio button checked, animation complete](images/well-by.webp)

<details class="question" open>
<summary>Just for fun</summary>
On my screen, the Well label is grey, which shows that its `<input>` **has** been `:checked`, but the radio button beside it appears unchecked. Can you explain why?

Hint: How many radio buttons are there? What position has each been given? Do you see just a trace of blue around the edge of the radio button that you can see?

</details>

If you click on the Good button, once again the display jumps back immediately to showing `Hi`. 

<details class="question" open>
<summary>Just a hint</summary>
And the _frontmost_ radio button beside Well appears checked. Does that help you answer the previous question?

</details>

There's still no reverse animation. You'll need to add a new rule for `#good:checked`.
```css-#139
body:has(#good:checked) {
  span::before {
    animation: letter-3 2.0s linear reverse forwards;
  } 
  span::after { 
    animation: letter-4 1.6s linear reverse forwards;
  }
}
```

The animation should play in reverse.

![The Good radio button checked, reverse animation complete](images/good-hi.webp)

#### Kill the spare

It would be nice to make this radio button pair behave like a single toggle checkbox... but with a third state. When the page is first loaded, you should see a button named "Well". When you click on it, its name should become "Good". Or rather, the Well label should be replaced by the Good label.

The new rule below will hide whichever label contains a `:checked` radio button:
```css-#148
label:has(:checked) {
  display: none;
}
```
<details class="challenge" open>
<summary>Solution</summary>
However, both buttons both appear when the page is first loaded, when neither of them has been checked yet. Can you think of a second selector for the rule above to apply to? It should say something like: "If there is a label containing an unchecked radio button followed by another label containing an unchecked radio button, hide the second label."

You'll need to use a sibling combinator, like `~` or `+` to select the second label.

<details class="solution">
<summary>Solution</summary>
Here's my solution. Can you adapt this to work with your version?
```css-w
<b>label:has(input:not(:checked)) + label:has(input:not(:checked)),</b><i>
label:has(:checked) {
  display: none;
}</i>
```
</details>
</details>
</section>