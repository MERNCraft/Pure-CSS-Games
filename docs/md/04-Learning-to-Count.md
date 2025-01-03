<!-- Learning to Count -->
<section
  id="learning-to-count"
  aria-labelledby="learning-to-count"
  data-item="Learning To Count"
>
  <h2><a href="#learning-to-count">Learning To Count</a></h2>
  
### The Origin Story: ordered lists

If you create an `<ol>` ordered list, your browser will automatically number the lines. Try it:
```html
<h1>TO DO LIST</h1>
<ol>
  <li>Buy a tortoise</li>
  <li>Call it 'The Speed of Light'</li>
  <li>Tell people I can run faster than The Speed of Light</li>
</ol>
```
You can change the number that the list starts with by using the `start` attribute in your HTML:
```html
<ol start="10">
  <li>Buy a tortoise</li>
  <li>Call it 'The Speed of Light'</li>
  <li>Tell people I can run faster than The Speed of Light</li>
</ol>
```

![using `<ol start="10">`](images/ol.webp)

This works because under the hood, the browser uses a  [counter](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_counter_styles/Using_CSS_counters) called `list-item`. You can control this counter through CSS. With the following rule, all your `<ol>` elements will start from `101`... even those where you set the `start` property in your HTML file. The `counter` property takes precedence...
```css
ol {
  counter-set: list-item 101;
}
```
<details class="warn" open>
<summary>or rather: "_should_ take precedence"</summary>
... except that since Google released Chromium 126 on 11 June 2024, this use of `list-item` is broken in Webkit browsers such as Google Chrome, Opera and Microsoft Edge. It still works in Firefox and Safari, so you can test it there. It's not a big deal, because you won't need to use exactly this feature for anything in your CSS-only games. It's just nice to know that ordered `<ol>` lists were where the `counter` feature came from.

</details>
</section>