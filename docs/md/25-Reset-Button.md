<!-- Reset Button -->
<section
  id="reset-button"
  aria-labelledby="reset-button"
  data-item="A Reset Button"
>
  <h2><a href="#reset-button">A Reset Button</a></h2>
  
Now that you have buttons to control the animation, you can use a `<button type="reset">` inside a `<form>` element to reset the buttons to their initial states. A `<button type="reset">` on its own won't work: it has to be inside a `<form>` element before it has any effect. 

Here's what your HTML might look like with a form reset button:

```html
<form>
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

  <button type="reset">Reset Form</button>
</form>
```

<details class="note" open>
<summary>Edge case</summary>
This only works because the animation is triggered by buttons. That's why I did not suggest it from the beginning. An animation that is triggered automatically after the page has loaded will continue to play, no matter how hard you press a `<button type="reset">`.

</details>

</section>