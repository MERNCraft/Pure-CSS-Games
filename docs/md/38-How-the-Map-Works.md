<!-- How the Map Works -->
<section
  id="how-the-map-works"
  aria-labelledby="how-the-map-works"
  data-item="How The Map Works"
>
  <h2><a href="#how-the-map-works">How The Map Works</a></h2>
  


You've already seen the Map activity. Now that you have an understanding of how CSS counters and `@counter-style` works, you can make sense of the tricks I have used.

<iframe
  id="iframe-map-2"
  title="Map"
  width="500"
  height="150"
  src="https://merncraft.github.io/map">
</iframe>

## Counting nesting depth

The Map uses counters to detect how deeply nested the element immediately under the touch point is. 

The relief pattern for the hill and the sea is created by nested `<div>` elements:

```html-#21
      <div class="hill-1 contour">
        <div class="hill-2">
          <div class="hill-3">
            <div class="hill-4">
              <div class="hill-5"></div>
            </div>
          </div>
        </div>
      </div>

      <div class="sea-1 contour">
        <div class="sea-2">
          <div class="sea-3">
            <div class="sea-4">
              <div class="sea-5"></div>
            </div>
          </div>
        </div>
      </div>
```

Suppose the mouse is over `<div class="hill-4">`. As you saw in the last section, four of the `div`s with a class whose name begins with `hill` will have a `:hover` pseudo-class: `div class="hill-4">` itself and all its parents.

## @counter-style for height or depth

I've created an `@counter-style` at-rule to display a string that represents a height or a depth for each of its values:

```css
@counter-style relief {
  symbols: "100m" "200m" "300m" "400m" "500m";
}
```

I increment a `relief` counter, for each `div`s with a class whose name begins with `hill` which has a `:hover` class.

```css-#130
div[class|=hill]:hover {
  counter-increment: relief;
}
```

<details class="note" open>
<summary>counter and @counter-style with the same name</summary>
The CSS elves are smart enough to distinguish between a `counter` and an `@counter-style` that have the same name, so it makes sense to use the same name for both, to indicate that they work together.

</details>

And I use a `::before` pseudo-element on the `<p>` element centred at the top of the page to show the height. But I hide this `::before` element...

```css-#168
p.relief::before {
  content: "Height: " counter(relief, relief);
  display: none;
}
```
...unless the lowest `div.hill-1` element has `:hover` applied to it:

```css-#176
.hill-1:hover ~ p.relief::before {
  display: inline;
}
```

## Dealing with the grid

The grid pattern is even more complex: ten vertical rectangular `<div>`s, one for each of the columns, all nested inside each other, and inside each column.

In this composite image below, you'll see how the mouse is hovering over a `<div class="row-3">`, which is a child of all the following:

* `<div class="row-2">`
* `<div class="row-1">`
* `<div class="col-2">`
* `<div class="col-1">`

![Hovering over cell B3](images/hoverB3.webp)

In the CSS, a counter called `col` is incremented for each `div` whose class name begins with `col`...

```css-#193
div[class^=col]:hover {
  counter-increment: col;
}
```
... and a counter called `row` is incremented for each `div` whose class name begins with `row`...

```css-#212
div[class^=row]:hover {
  counter-increment: row;
}
```

Each `div` whose class name begins with `row` also has its own `::before` element, whose `content` is determined by the `col` and `row` counters. However, these `::before` elements acquired not shown...

```css-#218
div[class^=row]::before {
  content: counter(col, upper-alpha) counter(row);
  position: absolute;
  width: 30px;
  line-height: 30px;
  text-align: center;
  display: none;
}
```
... except for the `div` which is _immediately_ under the mouse:

```css-#227
/* Show a label for the hovered cell... */
div[class^=row]:hover::before {
  display: inline-block;
}
/* ...but not for all the cells in the parent rows */
div[class^=row]:has(:hover)::before {
  display: none;
}
```

</section>