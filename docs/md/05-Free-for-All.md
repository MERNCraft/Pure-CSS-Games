<!-- Free for All -->
<section
  id="free-for-all"
  aria-labelledby="free-for-all"
  data-item="Free For All"
>
  <h2><a href="#free-for-all">Free For All</a></h2>

Ordered lists don't claim exclusive rights over counters. Browsers make counters available to any element. They give you full control of any kind of numbering process. Here's what an ordered list does naturally:

```html
<ol>
  <li>For the money</li>
  <li>For the show</li>
  <li>To get ready and go cat go</li>
</ol>
```

![Standard numbering with an ordered list](images/ol_go-cat-go.webp)


Here's how you could create a similar (not identical) result using a `<ul>` unordered list.
```html
<ul>
  <li>For the money</li>
  <li>For the show</li>
  <li>To get ready and go cat go</li>
</ul>
```
```css
ul {
  list-style-type: none;
  counter-set: item;

  li {
    counter-increment: item;
  }

  li::before {
    content: "Item " counter(item) ". ";
  }
}
```
Here's what happens:

* The CSS elves see that a `counter` called `item` has been set for the `<ul>` element.
* By default, they give it the value `0`.
* They apply the rule `counter-increment: item` each time they meet a new `<li>` item in the list where the `item` counter was set.
* They then read the current value of `counter(item)` and use this number as the [`content`](https://developer.mozilla.org/en-US/docs/Web/CSS/content) of the [`::before`](https://developer.mozilla.org/en-US/docs/Web/CSS/::before) pseudo-element.
* They apply the decorations `Item ` and `. ` around the counter

![numbered unordered list](images/go-cat-go.webp) 


<details class="note" open>
<summary>Summary</summary>
Note that [you can provide several items](https://developer.mozilla.org/en-US/docs/Web/CSS/content#syntax) in the value for the `content` attribute, like `"Item " counter(item) ". "`, and the CSS elves will concatenate them together for you. 

</details>

<details class="warn" open>
<summary>Summary</summary>
Note that I use [`counter-set`](https://developer.mozilla.org/en-US/docs/Web/CSS/counter-set) and not `counter-reset`, because the current version of Firefox (128.0.3) does not always handle `counter-reset` as you would expect it to.

</details>

</section>