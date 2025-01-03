<section
  id="seeing-how-css-works"
  aria-labelledby="seeing-how-css-works"
  data-item="How CSS Works"
>
  <h2><a href="#seeing-how-css-works">Seeing How CSS Works</a></h2>

<details class="alert" open>
<summary>Warning</summary>
What I show below is _not good HTML_. You are not supposed to use `<b>` tags inside a `<ul>` list, and there's not a real-life case for leaving them empty. But this makeshift HTML is good enough to show you how the CSS elves work.

</details>

```html
&lt;b&gt;&lt;/b&gt;
<ul>
  &lt;b&gt;<&lt;b&gt;
  <li>For the money</li>
  &lt;b&gt;&lt;/b&gt;
  <li>For the show</li>
  &lt;b&gt;&lt;/b&gt;
  <li>To get ready and go cat go</li>
  &lt;b&gt;&lt;/b&gt;
</ul>
```
In my first example, I gave no initial value for the `item` counter, so it started with the default value of `0`. The CSS elves then found the first list item ("For the money"), and incremented the `item` counter by the default amount: `1`. So when the first list item was shown, the `content` of its `::before` pseudo-element was "Item 1."

In the CSS below, I create a custom `counter` called `item`, with an initial value of `10`. I also use `counter-increment: item 5;` each time an `<li>` item is treated, so the first item starts with an `item` value of 15.

```css
ul {
  list-style-type: none;
  counter-set: item 10;

  li {
    counter-increment: item 5;
  }

  li::before {
    content: "Item " counter(item) ". ";
  }
}

b::before {
  content: "—[" counter(item) "]—";
}
```
Here's what this looks like:

![How CSS increments items](images/counters.webp)


Notice the values of `counter(item)` that are shown in the `<b>` elements.

- The `item` counter is not available to the first `<b>` element (outside the `<ul>` element where `item` is declared, so it shows the default value of `0`.
- The `<b>` element that appears in the HTML page before the first `<li>` item shows the initial value of `10`.
- The other `<b>` elements show the value for `item` that was accumulated by all the `<list>` items that came before it.

</section>