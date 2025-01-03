<!-- One way Clicking -->
<section
  id="one-way-clicking"
  aria-labelledby="one-way-clicking"
  data-item="One-way Clicking"
>
  <h2><a href="#one-way-clicking">One-way Clicking</a></h2>
  
If you click on the same gold circle a second time, the checkbox will be deselected, and the number of "clicked" circles will go down. What is the simplest way to ignore any subsequent clicks?

In a group of radio buttons, only one radio button can be checked at any given time. Clicking on that button again does not uncheck it. If you have a group with only one radio button in it, then you can switch it from unchecked to checked, but you can't toggle it back. Initially, a group of radio buttons does not need to have any buttons checked. This means that when you use radio buttons, the initial state can have all the buttons unchecked, just like you can do with checkboxes.

To test this, change the `type` of each `input` from `checkbox` to `radio` and refresh your page.
```html
  <i><label>
    <input type="</i><b>radio</b><i>">
    <span></span>
  </label>
  <label>
    <input type="</i><b>radio</b><i>">
    <span></span>
  </label>
  <label>
    <input type="</i><b>radio</b><i>">
    <span></span>
  </label>
  
  <p>You have clicked on <span>/</span> circles.</p></i>
```
Now only the first click on a gold circle will have any effect, and the number of "clicked" circles cannot decrease.

<details class="question" open>
<summary>Not following orders</summary>
If you follow my instructions perfectly, your web page should work. But if it works, what exactly have you learnt? You have definitely learnt to follow instructions, but you probably knew how to do that already.

So what if you deliberately do something different, something disruptive, something that I didn't ask you to do? For example: what would happen if you put the "You have clicked on ... circles" message at the _beginning_ of your HTML page?

And just as a double-check, you can add a new line between the second and the third label, like this:

```html
  <b><p>You have clicked on <span>/</span> circles.</p></b>
  <i><label>
    <input type="radio">
    <span></span>
  </label>
  <label>
    <input type="radio">
    <span></span>
  </label>
  </i><b><p><span>/</span> so far</p></b><i>
  <label>
    <input type="radio">
    <span></span>
  </label></i>
```

Suddenly, your first message insists "You have clicked on 0/0 circles", no matter how hard you click. The new line that you have inserted fails to count the circle in the layer above it, or any clicks on that circle.

![The order of the HTML elements matters](images/1-circle.webp)

But were you really being disruptive? Or were you just following instructions again? I wasn't watching.

</details>

<details class="note" open>
<summary>Above or below?</summary>
Notice how I use the word "above" in the question block above.

> The new line that you have inserted fails to count the circle in the layer <b><i>above</i></b> it

The third circle is shown on the screen _below_ the other two, and lower down in the HTML file. However, it is _drawn_ in a layer that covers the elements that appear earlier in the HTML file. In the _z-direction_ —from the screen to your eye— it is _above_ the `<p>` element and the other circles, even if in the y-direction, it is closer to the bottom of your screen.

You can see what I mean if you add this rule at the end of your file:
```css-#31
label:last-of-type span {
  position: relative;
  top: -30vh;
  left: 10vh;
  border: 10px solid red
}
```
![Elements _lower_ in the HTML page are rendered _above_ those higher in the page](images/above.webp)

So yes, in one sense, the bottom circle is "above" the others.

</details>

</section>