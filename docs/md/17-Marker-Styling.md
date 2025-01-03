<!-- Marker Styling -->
<section
  id="marker-styling"
  aria-labelledby="marker-styling"
  data-item="::marker Styling"
>
  <h2><a href="#marker-styling">`::marker Styling`</a></h2>

In the example in the previous section, all the Thai list-items appear in red, and the weekday abbreviations "Sat" and "Sun" appear in gold. This is not an effect of the `@counter-style` that is used. This is achieved by [styling the `::marker` pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/::marker).

You can only change a few properties of the `::marker` pseudo-element. You can't change its alignment or position, for instance, but you can change the `color` and even the `content`. Here's the CSS that I've used to make weekends stand out, and react to being rolled over by the mouse:

```css-#
#weekdays:checked {
  & ~ ol {
    list-style-type: weekdays;

    li:nth-child(7n + 6)::marker,
    li:nth-child(7n)::marker {
      color: gold;
    }

    li:nth-child(7n + 6):hover::marker,
    li:nth-child(7n):hover::marker {
      content: "Weekend!";
    }
  }
}
```

Note that the `:hover` pseudo-class applies to the list item itself; it cannot be applied to the `::marker` pseudo-element.

![Hovering over Saturday](images/hover-sat.webp)

The `::marker` pseudo-element only applies to list elements (`<ul>`, `<ul>` and `<dl>`). You can provide CSS rulesets for the  `::before` and `::after` pseudo-elements of any visible element, and these can be styled in many more ways than the `::marker` pseudo-element.

</section>