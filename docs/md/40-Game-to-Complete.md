<!-- Game to Complete -->
<section
  id="Game to Complete"
  aria-labelledby="Game to Complete"
  data-item="A Game to Complete"
>
  <h2><a href="#Game to Complete">Complete a Game by Adding Counters</a></h2>

I wrote at the beginning of this article that I would not be showing you, step by step, how to build a particular game. However, I do want to give you the chance to test whether my explanations have made good sense to you.

I've created a pure CSS game that uses the techniques that I have described above. You can find the GitHub Repository [here](https://github.com/MERNCraft/path).

<iframe
  id="iframe-path"
  title="Path"
  width="300"
  height="300"
  src="https://merncraft.github.io/path">
</iframe>

<details class="challenge" open>
<summary>Adding counters</summary>
If you clone the repository and launch the game on your own computer, you will find that the scoring and timing system is missing. Using the knowledge that you have just acquired, can you get your local version of the game to behave the same as the online version?

The logic of the game (starting and stopping it, picking up the gold tokens, showing the result when you reach the end) is already written. You'll find the CSS for this in a file called `styles.css`. You should not need to change anything in this file or in the `index.html` file.

There is a second CSS file attached to the HTML page. It's called `counters.css`, and it currently contains no CSS at all. You should now be able to write CSS of your own that:

- Shows the score
- Shows an emoji that gets happier as the score increases
- Shows how many seconds have passed since the player clicked on the green Start button
- Stops the timer when the game is over.

And of course, you can use this as the starting point for your own remixed version of the game. I'm sure that, artistically, your CSS power does exceed my own...

</details>
</section>