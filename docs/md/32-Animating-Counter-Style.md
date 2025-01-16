<!-- Animating Counter Style -->
<section
  id="animating-counter-style"
  aria-labelledby="animating-counter-style"
  data-item="@counter-style"
>
  <h2><a href="#animating-counter-style">Animating a counter-style</a></h2>
  
Now you are ready to combine animating a counter and using a custom `@counter-style` at-rule. Here's a little puzzle where the challenge is not finding the combination of letters that opens the lock, but finding the order in which you need to change the letters. If you get the right word but don't get the right order, the CSS equivalent of an alarm goes off when you press Enter.

But you should know a little about me by now. I do like words to be spelt correctly, and I do like to move the shortest distance between points. Of the 24 possible orders in which you can change each letter only once, only one meets my high standards.

<iframe
  id="iframe-lock"
  title="Lock"
  width="300"
  height="150"
  src="https://merncraft.github.io/lock">
</iframe>

This article is about counters, so I won't show you how to create the entire puzzle. I'll just show you how to animate the way the letters change. I'll get you to make a much simpler activity that uses this technique. If want to see how the order-of-execution logic was done, you can check out the [GitHub repository](https://github.com/MERNCraft/lock).

## Another new project

It's time to start a new project with a basic HTML page linked to a CSS file, just like you've done before. Create a new folder called `Animated Counters`, with and `index.html` file linked to a `styles.css` file, And then put on your [Thinking Cap](https://en.wiktionary.org/wiki/thinking_cap).

<details class="challenge" open>
<summary>A checkbox and a span (or two)...</summary>
You're going to be animating two counters, using letters instead of numbers. The animation will start when you check a checkbox input. The image below shows what I want your page to look like in a browser. Do you think you can create this on your own, without looking at the HTML and CSS below?

![Before the animation: Hi](images/check-hi.webp)

As a clue, here's how your page will will look like after the animation (but you don't have to think about the animation yet):

![After the animation: By](images/check-by.webp)

> OK, I do not normally spell "Bye" this way, and if _you_ do you might accuse me of cultural appropriation, but please forgive me. Animating just two letters is all you need to understand the techniques.

"H" is the eighth letter in the alphabet, and "i" is the ninth. Later (but not yet), you'll create one `@keyframes` animation to count from 8 to 2 (to replace "H" with "B"), and another`@keyframes` animation to count from 9 to 25 (to replace "i" with "y").

Do your best with creating the "Well Hi! page! You can compare your version with mine later, and see if yours was in fact more elegant : )

<details class="hint">
<summary>Hints</summary>
Here are some things to think about:

- How to show the value of a counter
- How to set the initial value of a counter
- How to display a counter using upper-case letters
- How to display a counter using lower-case letters
- How you will (eventually) hide the checkbox input
- How you can make a label look like a button
- The final exclamation mark is not going to change. It's not part of either animation.
- 
</details>

<details class="solution">
<summary>Solution</summary>
Here's the HTML that I used:

```html
<label>
  <input type="checkbox">
  Well
</label>
<span></span>!
```
And you'll see below the CSS that I started with. Note that the names for built-in counter styles is case-insensitive. I could use `upper-alpha` or `Upper-Alpha` and it would work just as well.
```css
body {
  counter-set:
    letter-one 8
    letter-two 9
  ; 
}

label {
  padding: 8px 16px;
  border: 1px outset #888;
  border-radius: 8px;
  display: inline-block;
}

input {
  position: absolute;
  left: 0vw;
}

span::before {
  content: counter(letter-one, UPPER-ALPHA);
}

span::after {
  content: counter(letter-two, lower-alpha)
}
```
I imagine that you will have used different names for your classes and counters. You might have used a different selector to hold the `counter-set` rule. You might have used two elements to show the letters `Hi`, each with its own `::before` or `::after` pseudo-element.

That's good. If your CSS creates a similar effect to mine, don't change it at all. If your CSS is different now, that means that you will have to adapt the CSS that I provide below so that it works with yours. And that means that you might make mistakes which you will have to correct. And each mistake that requires effort to correct helps you to remember what you have learnt.

I've used `left: 0vw` for the absolute position of the input element. That means that it remains visible on the page for now. In production, I would set it to `-999vw` which will move it far off-screen to the left. The value I use is arbitrary; all that matters is that it is greater than the screen width of a checkbox.

If you want your label to behave more like a button when you hover your mouse over it or click, you can add a couple of cosmetic rules:
```css-#28
label {
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -o-user-select: none;
  user-select: none;
}

label:has(:checked),
label:hover:active {
  border-style: inset;
  background-color: lightgrey;
}
```
With these changes, the label appears in a different state when the `<input>` that it contains is `:checked`.


</details>
</details>

## Treating the animation

Figure 14 below shows your web page should look like after you check the checkbox.

![Click the checkbox to run the animation: By](images/grey-by.webp)

So here's a second challenge.

<details class="challenge" open>
<summary>Create two `@keyframes` at-rules</summary>
Can you create two `@keyframes` at-rules, one to change the letter `H` into the letter `B`, and one to change the letter `i` into the letter `y`?

And can you find a CSS selector and ruleset that will do the following?

- Detect when the `<body>` element contains a checked input
- Tell each of the `::before` or `::after` pseudo-elements which `@keyframes` animation to use

<details class="solution">
<summary>Solution</summary>
Here are the `@keyframes` at-rules that I used in my version:
```css-#42
@keyframes letter-1 {
  0% { counter-increment: letter-one  +0 } /* H */
  5% { counter-increment: letter-one  +1 } /* I */
 10% { counter-increment: letter-one  +2 } /* J */
 15% { counter-increment: letter-one  +3 } /* K */
 20% { counter-increment: letter-one  +4 } /* L */
 25% { counter-increment: letter-one  +5 } /* M */
 30% { counter-increment: letter-one  +6 } /* N */
 35% { counter-increment: letter-one  +7 } /* O */
 40% { counter-increment: letter-one  +8 } /* P */
 45% { counter-increment: letter-one  +9 } /* Q */
 50% { counter-increment: letter-one +10 } /* R */
 55% { counter-increment: letter-one +11 } /* S */
 60% { counter-increment: letter-one +12 } /* T */
 65% { counter-increment: letter-one +13 } /* U */
 70% { counter-increment: letter-one +14 } /* V */
 75% { counter-increment: letter-one +15 } /* W */
 80% { counter-increment: letter-one +16 } /* X */
 85% { counter-increment: letter-one +17 } /* Y */
 90% { counter-increment: letter-one +18 } /* Z */
 95% { counter-increment: letter-one  -7 } /* A */
100% { counter-increment: letter-one  -6 } /* B */
}

@keyframes letter-2 {
  0% { counter-increment: letter-two  +0 } /* i */
  6% { counter-increment: letter-two  +1 } /* j */
 12% { counter-increment: letter-two  +2 } /* k */
 19% { counter-increment: letter-two  +3 } /* l */
 25% { counter-increment: letter-two  +4 } /* m */
 31% { counter-increment: letter-two  +5 } /* n */
 37% { counter-increment: letter-two  +6 } /* o */
 44% { counter-increment: letter-two  +7 } /* p */
 50% { counter-increment: letter-two  +8 } /* q */
 56% { counter-increment: letter-two  +9 } /* r */
 63% { counter-increment: letter-two +10 } /* s */
 69% { counter-increment: letter-two +11 } /* t */
 75% { counter-increment: letter-two +12 } /* u */
 82% { counter-increment: letter-two +13 } /* v */
 88% { counter-increment: letter-two +14 } /* w */
 94% { counter-increment: letter-two +15 } /* x */
100% { counter-increment: letter-two +16 } /* y */
}
```
I _could_ have used the same names for the animations as for the counters. CSS will understand that `@keyframes letter-one` refers to something different from `counter(letter-one)`, but if I give them different names then you can see that the name of the animation and the name of the counter it increments _can_ be different.

I've used intervals that are not _exactly_ the same between each frame, just because I like to keep things as simple as possible.

Also, I made both animations run forwards through the alphabet, even though running backwards would have required fewer changes. It's my homage to the pre-digital flight information display boards in airports, I suppose.

![Flight information display board](images/board.jpg)

Back to the `@keyframes` at-rules, notice how the "H to B" animation flips from positive increments to negative increments when it goes from "Z" round to "A".

Here's the CSS rule that I used to trigger the animations:
```css-#86
body:has(:checked) {
  span::before {
    animation: letter-1 2.0s linear forwards;
  }
  span::after {
    animation: letter-2 1.6s linear forwards;
  }
}
```
I used `0.1s` for each letter change, because I just want to see that the animation is working without wasting precious seconds.

To be honest, if I really wanted not to waste time, I should run both animations backwards. Here is another way of achieving the same overall effect, this time with one animation finishing before the other begins:
```css-#95
@keyframes letter-a {
  0% { counter-increment: letter-one -0 } /* H */
 16% { counter-increment: letter-one -1 } /* G */
 33% { counter-increment: letter-one -2 } /* F */
 50% { counter-increment: letter-one -3 } /* E */
 67% { counter-increment: letter-one -4 } /* D */
 84% { counter-increment: letter-one -5 } /* C */
100% { counter-increment: letter-one -6 } /* B */
}

@keyframes letter-b {
  0% { counter-increment: letter-two  -0 } /* i */
 10% { counter-increment: letter-two  -1 } /* h */
 20% { counter-increment: letter-two  -2 } /* g */
 30% { counter-increment: letter-two  -3 } /* f */
 40% { counter-increment: letter-two  -4 } /* e */
 50% { counter-increment: letter-two  -5 } /* d */
 60% { counter-increment: letter-two  -6 } /* c */
 70% { counter-increment: letter-two  -7 } /* b */
 80% { counter-increment: letter-two  -8 } /* a */
 90% { counter-increment: letter-two +17 } /* z */
100% { counter-increment: letter-two +16 } /* y */
}

body:has(:checked) {
  span::before {
    animation: letter-a 0.6s linear forwards;
  }
  span::after {
    animation: letter-b 1.0s 0.6s linear forwards;
  }
}
```

<details class="note" open>
<summary>A temporary alternative</summary>
Note that if you add this alternative solution, you don't need to comment out the previous `body:has(:checked)` ruleset. CSS will apply the last rules given for this selector.

But after you've tested this alternative, delete it or comment it out. The rest of this exercise assumes that you are using the `letter-1` and `letter-2` @keyframes.
</details>

In `animation: letter-b 1.0s 0.6s`, the second time (`0.6s`) refers to the [`animation-delay` property](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-delay), which tells the animation how long it should wait before it starts. (You can even use negative values for this, and the animation will play _as if_ it had begun in the past.)

Notice that in the `@keyframes letter-1` at-rule above, the `increment` value jumps from `+18` for `Z` to `-7` for A. The same is true for the `@keyframes letter-1` rule, which flips from to `-8` for `a` to `+17` for `z`. 

<details class="note" open>
<summary>@counter-style systems</summary>
The built-in`lower-alpha` and `upper-alpha` counters uses [`system: alphabetic`](https://developer.mozilla.org/en-US/docs/Web/CSS/@counter-style/system) in their definition. This is slightly different from `system: numeric` in that there is no value for zero. If you ask use a `content` declaration to show the value `0` for an `alphabetic` counter, it fall back on the `@default counter-style` and show exactly `0`. 

Because there are 26 letters in the English/Latin alphabet, the value `27` will be represented as `AA` or `aa`. This is not what you want in this particular case, but you might find it useful in other cases.

Try it and see. Change the values that you use in your `counter-set` rule to something like this:
```css
body {
  counter-set:
    letter-one 0
    letter-two 27
  ; 
}
```
![Letter 0 is "0" and letter 27  is "aa"](images/0AA.webp)

</details>
</details>
</details>

<details class="note" open>
<summary>Fruit machine</summary>
The fruit machine animation that you saw at the beginning uses exactly the same technique, with a few extra tricks:

* I've used an `@counter-style` at-rule that shows chosen emojis
* Each reel of the fruit machine shows several numbers
* The reels themselves are animated, to rotate about the x-axis at a regular speed, then to jump backwards each time the counter animation changes its value.
* The smiley face also uses a `counter` and an `@counter-style` at-rule

<iframe
  id="iframe-fruit"
  title="Fruit"
  width="300"
  height="150"
  src="https://merncraft.github.io/spin">
</iframe>

There are also two Spin buttons for each reel. The second button is hidden until the first Spin button for two other reels has been triggered. This means that the third Spin button you press triggers a previously hidden button, which starts a different animation... which glitches.

So you can never win.

</details>

</section>