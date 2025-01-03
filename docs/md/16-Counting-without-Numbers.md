<!-- Counting without Numbers -->
<section
  id="counting-without-numbers"
  aria-labelledby="counting-without-numbers"
  data-item="No-number Counters"
>
  <h2><a href="#counting-without-numbers">Counting Without Numbers</a></h2>

So far, every time you've seen a counter, it's looked like a number. Well... that's not quite true. Right at the beginning, in the little sneak-peek demos, you saw counters that look like letters and emojis. You may not even have realized they were counter tokens, although I did give a big hint.

Here's a CSS-only presentation of how the [`@counter-style` at-rule](https://developer.mozilla.org/en-US/docs/Web/CSS/@counter-style) can be used to change the tokens that are used to number items in an `<ol>` list. Click on the style names on the right to see how it changes the counter tokens on the left.

The `<ol>` list on the left contains only empty `<li>` items, so all you see are the `::marker` tokens.


<iframe
  id="iframe-counter-styles"
  title="Counter Styles"
  width="300"
  height="230"
  src="https://MERNCraft.github.io/counter-styles">
</iframe>

The default value for `list-style-type` is decimal. Your browser has [over 100 built-in alternatives](https://w3c.github.io/predefined-counter-styles/), to cater to writing systems all around the world. You can see them in action [here](https://mdn.github.io/css-examples/counter-style-demo/). In order to create so many styles, the [`@counter-style`](https://developer.mozilla.org/en-US/docs/Web/CSS/@counter-style) at-rule became [available in all major browsers since September 2023](https://caniuse.com/?search=%40counter-style). 

Here, for example, is the built-in `@counter-style` at-rule for Thai numeric symbols. This gives the Unicode code points for each numeral:
```css-#
@counter-style thai { 
  system: numeric;
  symbols: '\E50' '\E51' '\E52' '\E53' '\E54' '\E55' '\E56' '\E57' '\E58' '\E59';
}
```
The `@counter-style` below has exactly the same effect. It uses the actual [Thai characters](https://compart.com/en/unicode/search?q=thai#characters) instead of their code points.
```css-#
@counter-style thai { 
  system: numeric;
  symbols: '๐' '๑' '๒' '๓' '๔' '๕' '๖' '๗' '๘' '๙';
}
```
And just like the `counter` property has been made generic so that all HTML elements have access to it, so the `@counter-style` has been made generic, so that you can create your own styles. Here's my rule for English weekday abbreviations:

```css
@counter-style weekdays {
  system: cyclic;
  symbols: "Mon" "Tue" "Wed" "Thu" "Fri" "Sat" "Sun";
  suffix: "";
}
```
By default, each `counter-style` has `"."` as its suffix. If you want to remove this (as I did for the weekdays), or change it to something else (like `")"`), you can use the `suffix` property.

Because you can use _any text_, you can also use emojis. Or [mathematical symbols](https://www.compart.com/en/unicode/category/Sm). Or Unicode [shapes](https://www.compart.com/en/unicode/block/U+25A0) and [arrows](https://www.compart.com/en/unicode/block/U+2190). The W3C specifications also describe the use of images, but at the time of writing, the major browsers have not implemented this for counters yet. (You can set the `list-style-image` as bullet points for a whole list or for an individual list item, though, but this is outside the current topic of counters.)

</section>