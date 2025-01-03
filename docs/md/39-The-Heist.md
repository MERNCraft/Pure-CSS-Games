<!-- The Heist -->
<section
  id="the-heist"
  aria-labelledby="the-heist"
  data-item="The Heist"
>
  <h2><a href="#the-heist">The Heist</a></h2>

So here's a challenge that I set for myself: How much can I do using just `:hover` as the trigger? How much can I do using no checkboxes, no radio buttons, no details elements.

Here's what I came up with:

<iframe
  id="iframe-heist"
  title="Heist"
  width="600"
  height="216"
  src="https://merncraft.github.io/heist/">
</iframe>

Each action is performed in a nested `<div>` and the nesting gets deeper as the story progresses. As a result, the innermost element with a `:hover `pseudo-class maintains a :hover pseudo-class on all its parents. In this way, any changes made at one level continue to apply to the inner levels.

However, if you move your mouse off the animation, it will reset and the story will start over from the beginning.

On touchscreen devices, the innermost element with a :hover pseudo-class retains this class even after the contact with the touchscreen ceases. If a child `<div>` is activated by a touch on its parent, the child `<div>` does not immediately receive a :hover pseudo-class. (With a mouse, the child `<div>` will receive its pseudo-class as soon as the mouse moves, if not sooner.)

The numbered instructions at the top are set using a `counter` for the number of `<div>` which have a `:hover` pseudo-class. The text is set by an `@counter-style` at-rule.

Click on the GitHub octocat icon to visit the GitHub repository.

***Enjoy!***

</section>