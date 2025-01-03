<!-- Hover -->
<section
  id="hover"
  aria-labelledby="hover"
  data-item="Hover"
>
  <h2><a href="#hover">Incrementing with `:hover`</a></h2>

Your browser generates a `:hover` pseudo-class for every element that is currently under the pointer. If the pointer is a mouse, then there will always be a `:hover` pseudo-class created somewhere while the mouse is over the page.

If the pointer is a finger or a stylus on a touch screen, than a `:hover` pseudo-class is created when there is the first actual contact with the screen... and then (on Chrome for Android, at least), the `:hover` pseudo-class remains, even though no-one is touching the screen.

Here's the simplest "game" I could think of that illustrates my point, inspired by "The Floor is Lava". On a computer screen, you have to move your mouse as the green safe space gets smaller and floats away. I haven't found any way to check that touchscreen players doesn't just simply lift their fingers and uncheck the checkbox. And yes: I've _tried_. If you can find a solution, please, [send me a link to _your_ articles](https://github.com/MERNCraft/Pure-CSS-Games/issues/new) so that I can learn from you.

<iframe
  id="iframe-lava"
  title="Lava"
  width="300"
  height="150"
  src="https://merncraft.github.io/lava">
</iframe>

In other words: if your game is intended for playing on touchscreens, using `:hover` as a major feature of your game is likely to cause you headaches. If you use it for inessential features, then you can have fun with it.

Also, even in a game with a mouse, a custom `:hover` feature will stop working as soon as the mouse moves over a button or other element that is not a child of the element whose `:hover` you are tracking. It can be tricky to get buttons and `:hover` to work together... but it can be _tricky_ in a good way.

So, with those warnings out of the way, would you like to have some fun with `:hover`... and with counters?

For the last time (in this article at least), I'll ask you to create a new HTML file with CSS file linked to it. Here's what you'll be making (except that yours will have a white background.):


<iframe
  id="iframe-hover"
  title="Hover"
  width="300"
  height="300"
  src="https://merncraft.github.io/hover">
</iframe>

Here's some HTML...
```html
<div title="one">
  <div title="two">
    <div title="three">
      <div title="four"></div>
    </div>
  </div>
</div>
```
... and some CSS:
```css
div {
  --size: 15vmin;
  --line: 1vmin;
  --delta: calc(var(--size) + var(--line) * 2);

  position: relative;
  top: var(--delta);
  left: var(--delta);
  width: var(--size);
  height: var(--size);
  border: var(--line) solid grey;

  &:hover {
    color: red;
    border-color: orange;
    counter-increment: divs;
  }

  &::after {
    content: attr(title) " " counter(divs);
  }
}
```
Open your page in your browser and move your mouse over the different `<div>`s:

![Hovering over nested elements](images/nestedHover.webp)

The nested `<div>` elements are clearly not overlapping. In my screenshot above, the mouse is clearly over `div.three`. And yet three of the `<div>` elements have an orange border. This must have been caused by the rule:

```css-#13
  &:hover {
    color: red;
    border-color: orange;
    counter-increment: divs;
  }
  ```

And the text of _all_ of the elements is red. And yes, the CSS elves are busy with some `counter-increment` activity as well. There is no `counter: divs 0` declaration, but they have understood that they need to behave as if the declaration were there.

As you move your mouse around, the elements which are given a `:hover` pseudo-class will change. On a touchscreen, you can tap different parts of the screen and see how the `:hover` effect remains even after you remove your finger.

<details class="note" open>
<summary>Where does ::after go?</summary>
Notice that the `::after` pseudo-element for the first three `<div>`s is shown _below_ the `<div>`, but the `::after` pseudo-element for the fourth `<div>` appears _inside_ it. That's because the first three have children. The `::after` pseudo-element is shown _after_ the children... or rather, after where the children would be if they had not been given a different `relative` `position`.

</details>

The border of the `<div>` under the mouse and all its parents goes orange, because hovering, like the credit for a child's achievements, is claimed by its parents, all the way back to the first generation.

The text of all the elements goes red when any one of them is under the mouse, because `color`, like eye-colour and debt for humans, is inherited from an element's parents.

</section>