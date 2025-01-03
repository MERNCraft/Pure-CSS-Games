<!-- HTML and CSS order -->
<section
  id="html-and-css-order"
  aria-labelledby="html-and-css-order"
  data-item="HTML and CSS Order"
>
  <h2><a href="#html-and-css-order">Order in HTML and CSS</a></h2>

From the test that you did in the last section, you can deduce that **the order in which elements appear _in the HTML file_ affects the order in which they can increment a `counter`**.

But what about the order of rules in the CSS stylesheet? What happens if you change the order in which the `counter` properties are set and read, as shown below?
```css
<b>/* Read the value of the counter properties... */
p span::before {
  content: counter(clicked)
}

p span::after {
  content: counter(total)
}

/* ...before you declare the counter properties */
</b><i>body {
  background-color: #222;
  color: #ddd;</i><b>
  counter-set:
    total
    clicked;
}</b>

<i>/* The CSS below is unchanged */
label span {
  --size: 20vh;
  display: block;
  width: var(--size);
  height: var(--size);
  border-radius: var(--size);
  background-color: gold;
  opacity: 0.25;

  counter-increment: total;
}  

input:checked ~ span {
  opacity: 1;
}

input:checked {
  counter-increment: clicked;
}</i>
```

![Reordering the CSS has no effect](images/reorderd.webp)

## Does this solve the problem that you just created?

No. But if you place a copy of the  element...

```html-#
<p>You have clicked on <span>/</span> circles.</p>`
```

... back at the end (as I did for the screenshot above), then everything works fine,  at least in this final position. This _suggests_ that the order in which rules appear _in the CSS file_ **does not** affect the order in which a `counter` is incremented.

But don't let this give you a false sense of security. As Mr Weasley said: "Never trust something that can think for itself if you can't see where it keeps its brain."


<details class="tip" open>
<summary>Checking it twice</summary>
Whenever I am following a tutorial to learn a new technique, I do the tutorial twice. The first time, I follow the instructions carefully, so that I can see that the results are what the writer promised. 

Sometimes, tutorials contain errors — a missing step, a missing line, a missing semicolon — and sometimes the technology has changed since the tutorial was written, and instructions that used to work no longer do. When I encounter a tutorial like this, I find that it is often worth persisting, and searching online for solutions. The process of searching is where a lot of my learning happens.

The second time I do the tutorial, I try not to read it at all. I do as much as I can from memory, and inevitably I make mistakes because there is something that I did not understand, or did not pay attention to, or assumed that I could ignore. I don't _mean_ to be disruptive. I just allow disruption to happen.

It is the mistakes that I make the second time that show me how much I still have to learn. If I don't make these mistakes, I can deceive myself into thinking that I have understood. Solving my mistakes takes effort (especially if I don't look back at the tutorial). And something that you have made an effort to do is something that you will remember. 

An app that works perfectly the first time is less helpful than an app where I have to struggle to get it to work.

</details>

</section>