<!-- Interacting with the User -->
<section
  id="interacting-with-the-user"
  aria-labelledby="interacting-with-the-user"
  data-item="User Interactions "
>
  <h2><a href="#interacting-with-the-user">Interacting with the User</a></h2>
  
A web experience cannot be considered to be a game if it has no user interaction. In this section, you'll be seeing how to use checkboxes, radio buttons and the sibling combinators ( [`~`](https://developer.mozilla.org/en-US/docs/Web/CSS/Subsequent-sibling_combinator) and [`+`](https://developer.mozilla.org/en-US/docs/Web/CSS/Next-sibling_combinator) ) to change what the CSS is counting, depending on what the user clicks on.

### Not on display

The CSS elves will only count what they can see. You can try to trick them with another sloppy line of HTML:
```html
<ul>
  &lt;b&gt;&lt;/b&gt;
  <li>For the money</li>
  &lt;b&gt;&lt;/b&gt;
  <input type="checkbox"> <!-- Linters don't like this in a <ul> -->
  <li>For the show</li>
  &lt;b&gt;&lt;/b&gt;
  <li>To get ready and go cat go</li>
  &lt;b&gt;&lt;/b&gt;
</ul>
```

And you can add a new rule that will hide the `<li>` item immediately after the checkbox when you check it.

(Note that I've also removed the `counter-increment: item -1;` from the `b::before` ruleset, to keep things simple.)
```css
<i>ul {
  list-style-type: none;
  counter-set: item 10;

  li {
    counter-increment: item 5;
  }

  li::before {
    content: "Item " counter(item) ". ";
  }

  </i><b>input:checked + li {
    display: none;
  }</b><i>
}

b::before {
  content: "—[" counter(item) "]—";
}</i>
```

What do you think will happen when you click on the checkbox?

![CSS doesn't count elements that are not displayed](images/checked-counter.webp)

If an element is not displayed, then no counter will count it.

However, if you simply hide a list item, like this...

```css-#13
<i>  input:checked + li {
    visibility: </i><b>hidden</b><i>;
  }</i>
```

... then the CSS elves _do_ count it:

![CSS does count hidden items](images/hidden-item.webp)


So here's a trick that you can use: You can set the `display` value of certain HTML elements to `none` if particular checkboxes or radio buttons are `checked`. The CSS elves will not count the elements with `display: none`, so you can display the number of such elements that are visible.

</section>