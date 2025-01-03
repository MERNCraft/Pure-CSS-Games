<!-- Counting Clicks 2 -->
<section
  id="counting-clicks"
  aria-labelledby="counting-clicks"
  data-item="Counting Clicks"
>
  <h2><a href="#counting-clicks-fail">Counting Clicks: Take 2</a></h2>
  
At the beginning, I hope you played with the [Arithmetic in Pure CSS](http://MERNCraft.github.io/calc) calculator. Amongst other things, this allows you to cycle through the digits from `0` to `9` and then round to `0` again.

One of the questions that I suggested you ask yourself was: "How do I cycle through all the numbers, using a single button?" Well, now it's time to give you an answer.

In the last exercise, you saw how to use just two radio buttons to cycle through just two different states (Well and Good). Can you imagine how you could extend this technique to cycle through all the numbers from `0` to `9` and then start again from `0`?

<details class="note" open>
<summary>Not with animations</summary>
OK, so technically, this exercise should not be in the Animations section, because it doesn't involve any animations, so it won't help you to think of a solution that uses animations.

But I did. I went down the wrong path. I went a long way down the wrong path before I gave up. Only Firefox stayed with me all the way.

If you're interested, you can read below the story of my failed attempt to use animations to solve this problem.

</details>

<details class="tldr">
<summary>A failed attempt</summary>
When I first planned this part, I had imagined that I would be able to use animation and two radio buttons, one on top of the other. My plan was to start with an animation which would repeatedly cycle through the digits `0` to `9`, but which started off `paused` at `0`.

The animation would start `running` as soon as the top radio button was checked. When the animation reached the next keyframe, it would move the label for the other radio button in front of the `:checked` button, so the label for the `:checked` button would no longer generate a `:hover` pseudo-class. I would have a rule that would pause the animation if there was no `:hover` pseudo-class on the `:checked` button. My plan was that the animation would stop at the current number, and stay there until the radio button which was _now_ at the front was clicked...

Fiendishly clever, I thought. But only Firefox agrees with me. Safari doesn't update the `:hover` class until you move the mouse, which leads to chaos. And the Chrome CSS elves just shake their heads and say: "Whaaat!?"

[![fail](images/fail.webp)](https://merncraft.github.io/stop-motion/)

If you feel so inclined, you can [try it for yourself](https://merncraft.github.io/stop-motion/) in different browsers.

I have included this failed attempt for a good reason, and not just because it took a lot of effort to get it to work at all. All progress takes effort. The article you are reading now and the demos that accompany it took many days to write. As soon as you start writing articles to share _your_ knowledge, you will know that it's worth it. When you decide to explain something in detail, you discover that there are still many details that you are unsure of, and you have to make the effort to understand them before you can continue.

One of the lessons that I learned from this failure was that Safari, Chrome and Firefox all treat `:hover` in subtly different ways. It's not good enough to have a good idea. You have to test early, test often, and test on all target platforms (Thank for that mantra, John Dowdell!)

</details>

To repeat my earlier question: **Can you imagine how you could extend the label-and-radio-button technique that you have just seen, to cycle through all the numbers from `0` to `9` and then start again from `0`?**

It's time for new HTML and CSS files. Perhaps you'd like to call this project "Counting to 9".

## Counting without counters

Here's the HTML for the first solution that I succeeded with: 

```html
<input type="radio" name="d" id="d0" checked>
<input type="radio" name="d" id="d1">
<input type="radio" name="d" id="d2">
<input type="radio" name="d" id="d3">
<input type="radio" name="d" id="d4">
<input type="radio" name="d" id="d5">
<input type="radio" name="d" id="d6">
<input type="radio" name="d" id="d7">
<input type="radio" name="d" id="d8">
<input type="radio" name="d" id="d9">
<label for="d1">1</label>
<label for="d2">2</label>
<label for="d3">3</label>
<label for="d4">4</label>
<label for="d5">5</label>
<label for="d6">6</label>
<label for="d7">7</label>
<label for="d8">8</label>
<label for="d9">9</label>
<label for="d0">0</label>
```

With no CSS, this creates a line of 10 checkboxes, followed by the digits `1234567890` in the same order as on the keyboard.

![A row of radio buttons followed by digits](images/radioNumbers.webp)

Note, though that the _first_ input is checked, and this is the input with`id="d0"`. The input for `0` is at the beginning, but the `<label for="d0">` is at the end. Try clicking on the _numbers_ to see which radio button becomes selected.

## Only two labels at a time

I want to show only two labels at any one time:

- The label which is `for` the `:checked` input. This should be visible.
- The label which is `for` the input with the next number in the cycle. This should be:
	- Invisible
	- In front of the label `for` the `:checked` input.

If I use `position: absolute` for all the labels, they will all appear one on top of each other, with the `<label for="d0">` at the top of the pile, immediately under the mouse. I'll make everything really big, so it's easy to click on the numbers:

```css
label {
  /* Cosmetic */
  --size: 100vmin;
  width: var(--size);
  height: var(--size);
  font-size: var(--size);
  text-align: center;

  /* Logical */
  position: absolute;
}
```
![Absolutely positioned labels](images/absolute.webp)

I won't show the `/* Cosmetic */` CSS any more, but you might like to keep it in your project anyway.

I need to put the `<label for="d1">` in front of the `<label for="d0">`. My trick is to:

* Set the `z-index` for all the labels _except for `<label for="d0">`_ to `1`
* Hide all the labels _except `<label for="d0">` and `<label for="d1">`
* The label for `<label for="d1">` (almost) transparent. (I'll leave just a little opacity for now, so you can see that the number is there.)

Now, a click on what seems to be the `0` will in fact be a click on the`1`. 

```css
<i>label {</i>
```
```css-s
<!-- Cosmetic lines skipped -->
```
```css-#10
 <i> position: absolute;</i><b>
  z-index: 1;
  display: none;
}

#d0:checked ~ [for=d0] {
  display: block;
  opacity: 1;
}

#d0:checked ~ [for=d1] {
  display: block;
  opacity: 0;
}

[for=d0] {
  z-index: 0;
}

#d9:checked ~ [for=d0] {
  z-index: 1
}</b>
```
<details class="note" open>
<summary>Troubleshooting</summary>
If you don't see any numbers on your page, check that the first radio button on the left i selected.

</details>

With the CSS shown above, if you click on the `0`, `<input id="d0">` will no longer be checked, but `<input id="d1">` will be checked instead. And the rest of the page will go blank.

I now want `<label for="d1">` to be visible, with `<label for="d2">` in front of it, but invisible. I can do this by adding an additional selector to each of the rulesets that set both `display` and `opacity`.

```css-#15
#d1:checked ~ [for=d1],
#d0:checked ~ [for=d0] {
  display: block;
  opacity: 1;
}
#d1:checked ~ [for=d2],
#d0:checked ~ [for=d1] {
  display: block;
  opacity: 0;
}
```

Indeed, I can apply the same logic all the way up to 9.

```css-#15
label {
  position: absolute;
  z-index: 1;
  display: none;
}

#d9:checked ~ [for=d9],
#d8:checked ~ [for=d8],
#d7:checked ~ [for=d7],
#d6:checked ~ [for=d6],
#d5:checked ~ [for=d5],
#d4:checked ~ [for=d4],
#d3:checked ~ [for=d3],
#d2:checked ~ [for=d2],
#d1:checked ~ [for=d1], 
#d0:checked ~ [for=d0] {
  display: block;
  opacity: 1;
}
#d9:checked ~ [for=d0],
#d8:checked ~ [for=d9],
#d7:checked ~ [for=d8],
#d6:checked ~ [for=d7],
#d5:checked ~ [for=d6],
#d4:checked ~ [for=d5],
#d3:checked ~ [for=d4],
#d2:checked ~ [for=d3],
#d1:checked ~ [for=d2], 
#d0:checked ~ [for=d1] {
  display: block;
  opacity: 0.1;
}

[for=d0] {
  z-index: 0;
}
```

When I click on a digit, the next digit becomes fully opaque, and shows the label for _its_ next digit very transparently in front of it.

This works until I click on the `8` and the label for `9` becomes fully opaque. But there is no sign of a semi-transparent `0`.

I can follow what is happening in the Developer Tools Inspector:

![Using the browser's Inspector](images/inspector.webp)

When I get to `9`, I want the next click to apply to the `<label for="d0">`. In the Inspector, this label _appears_ to be in a higher layer than  the `<label for="d9">`, but just now, I set the `z-index` of every label _except_  the `<label for="d0">` to `1`, so that I could click on  the `<label for="d1">` instead.  Now I'll need one last rule to fix this for this one specific case:

```css-#46
#d9:checked ~ [for=d0] {
  z-index: 1
}
```
Try it! You should be able to cycle through all the numbers.

## Detecting which number is currently checkd

This system has some advantages. At any time, I can use a selector which contains (say) `#d3:checked`, to check if the player is currently looking at a `3`. This makes it easy to apply other rules to other elements when you select the answer that I want you to select.

<details class="pivot" open>
<summary>Plus and minus</summary>
A major disadvantage is that you must click on the current number itself if you want it to increase. This is not an intuitive action.

It would be better to have a specific button that says `+`. And if you add a `+` button, why not add a `–` button, too?

**But, wait a minute... How can you make two buttons that work in opposite directions?**

</details>
</section>