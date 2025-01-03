<!-- White Space Matters -->
<section
  id="white-space-matters"
  aria-labelledby="white-space-matters"
  data-item="White Space Matters"
>
  <h2><a href="#white-space-matters">White Space Matters</a></h2>
  
Try adding a new line to the ruleset for the `b::before` selector:
```css-#14
<i>b::before {
  </i><b>counter-increment: item+1;</b><i>
  content: "—[" counter(item) "]—";
}</i>
```

You'll see that the CSS elves also now happily add `1` for each `<b>` element they encounter. Notice that there is no space between `item` and `+1`.

![Making `<b>` elements also increment `item`](images/b-counters.webp)

But what if you change the `+` to a`-` sign?

```css-#14
<i>b::before {
  counter-increment: </i><b>item-1</b><i>;
  content: "—[" counter(item) "]—";
}</i>
  ```

The CSS elves get confused. They think that you are referring to a counter named `item-1`. If you'd used `item-one`, it would have had the same effect. You didn't declare a counter called `item-1`, so they ignore it. The result will be just the same as what you saw in Figure 4.

If you add a white space, then everything is clear again.

```css-#14
<i>b::before {
  counter-increment: item</i><b> -1</b><i>;
  content: "—[" counter(item) "]—";
}</i>
```

<details class="note" open>
<summary>No `counter-decrement`</summary>
Note that there is no ~~`counter-decrement`~~ property. You have to increment by a negative number. And a space.

</details>

Each `b` element decreases `item` by 1, in each and every case, even outside the `<ul>` where the `item` counter is declared. In effect, the CSS elves are very accommodating. You didn't declare a `counter` for this particular element before you started using it? No worries, they will create one for you implicitly. Browsers are designed to be forgiving, so you can write sloppy code.

And yes, my code here is deliberately sloppy. I find that you learn more about how to write good code if you deliberately try to break the rules, and see what the effect is. [If you always do things perfectly, you don't find out what the rules are](https://www.youtube.com/watch?v=vKA4w2O61Xo).

And, as before, each `<li>` item increases `item` by 5.

![Alternately decrementing and incrementing a counter](images/counter-1.webp)

</section>