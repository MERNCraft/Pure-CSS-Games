<!-- What You Already Know -->
<section
  id="what-you-already-know"
  aria-labelledby="what-you-already-know"
  data-item="Prerequisites"
>
  <h2><a href="#what-you-already-know">What I expect you to know already</a></h2>
  

I'm assuming that you already:

* Know how to create an HTML page and link a CSS file to it
* Understand how to write CSS selectors
* Know how to structure [nested CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting).
  
<details class="tldr">
<summary>Nested CSS</summary>
Nested CSS has been [available in all major browsers since December 2023](https://caniuse.com/?search=nested%20css), and it's available to over 80% of all users, so it should work in your development browser. It allows me to write shorter CSS code.

Here's an example of how I use nested CSS to create numbered links:

```css-#
ol {
  list-style-type: none;
  counter-reset: item 0;

  li {
    margin: 0.5em;
    border: 1px solid black;
  
    a {
      color: inherit;
      text-decoration: none;
      display: inline-block;
      padding: 0.5em;
      width: 100%;
      box-sizing: border-box;

      &::before {
        counter-increment: item 1;
        content: counter(item) ". ";
      }

      &:hover {
        text-decoration: underline;
      }
    }
  }
}
```

The result would look something like this:

![An ordered list containing numbered links](images/nestedCSS.webp)

The nested CSS above will be treated exactly as if it were written in this standard expanded format:

```css-#
ol {
  list-style-type: none;
  counter-reset: item 0;
}
ol li {
  margin: 0.5em;
  border: 1px solid black;
}
ol li a {
  color: inherit;
  text-decoration: none;
  display: inline-block;
  padding: 0.5em;
  width: 100%;
  box-sizing: border-box;
}
ol li a::before {
  counter-increment: item 1;
  content: counter(item) ". ";
}
ol li a:hover {
  text-decoration: underline;
}
```



</details>

## What you might not know yet

If you don't yet know about the recently-introduced [`:has()` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:has), don't worry. You'll see plenty of examples on how to use it.

</section>