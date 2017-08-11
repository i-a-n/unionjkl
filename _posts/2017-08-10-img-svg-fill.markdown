---
layout:          post
title:           "Swapping Fill Color on Image Tag SVGs"
subtitle:        "A Side Quest in Optimizing Performance for React"
date:            2017-08-10 12:00:00
header-img:      "img/post-bg-svgs-react-1.jpg"
thumbnail-img:   "img/post-thumb-svgs-react-1.jpg"
published:       true
category:        Code
readtime:        "4 minutes"
includeSyntax:   true
includeLightbox: false
---

Of all the wonderfully useful things the SVG image format allows us to do on the web, perhaps the most useful is exposing shapes to the web browser, so we can manipulate them powerfully with JavaScript and lighting-quick with CSS. Want to add a stroke on hover? <a href="https://codepen.io/ianm/pen/PKjeXG" target="blank">Super easy</a>. Or change the fill? <a href="https://codepen.io/ianm/pen/brRMOW" target="blank">That’s three lines of CSS</a>.

<img src="https://union.io/images/repo/20170811-13--c1c131.png" alt="Change SVG fill" class="full">
<span class="caption text-muted">From black to blue... Look at how easy this is.</span>

But SVGs on the web are far from perfect. One problem—not a fatal one, but still an issue with any virtual DOM—is that embedding SVGs directly into your app can be a resource hog. No matter how much you compress, no matter how logical and streamlined your components, if you need to load up hundreds of very-complex SVGs, React will need to track all of their nodes, and updating them becomes a chore. Changing properties on thousands of these nodes in real-time becomes noticeably laggy, mostly due to React having to continually calculate and batch-update so much material. This is especially pronounced in Safari 9.x and 10.x.

One way around this is simply linking to each SVG with an <code>&lt;img></code> tag, instead of embedding the actual SVG in the DOM. This way, the virtual DOM only needs to track one node per image, instead of hundreds for each SVG.

<img src="https://union.io/images/repo/20170811-10--c2b89a.png" alt="Inline SVG" class="full">
<img src="https://union.io/images/repo/20170811-11--4dc36c.png" alt="Linked SVG" class="full">
<span class="caption text-muted">Inline SVG [above] vs linked SVG.</span>


But in doing so we've crippled our ability to manipulate our SVGs. No longer can we add stroke, move shapes, remove nodes or change fill. In short, if you want <code>:hover</code> to change the fill color, you’re back in the stone age. On first blush the only solution would seem to be to load up a different color SVG! This is downright primitive. What are we? Cavemen??

The answer, and the reason I wrote this article, is that no, you don’t have to go back to the neolithic, because our forebears invented CSS <code>filter</code>.

Although mostly used for <a href="https://css-tricks.com/almanac/properties/f/filter/" target="blank">gaudy blurs and overworked contrast levels</a>, we can use these filter rules to—in effect—manipulate the SVG’s fill. All it takes is a bit of patience to get the properties just right, but it’s entirely possible.

Let’s say you want to change the fill color on a transparent-background SVG from black to blue on hover.

<img src="https://union.io/images/repo/20170811-12--26cdfd.png" alt="From black to blue SVG" class="full">

First, let’s target the image with a CSS rule and invert the color, from black to white, using `invert()`:

<pre class='brush: css'>
.svg {
	filter: invert(.5);
}
</pre>
<img src="https://union.io/images/repo/20170811-06--78ac75.png" alt="Inverted SVG" class="full">

The amount you invert will be the lightness of the final color. For this shade of blue we're inverting 50%, giving us a medium-gray base to work with.

Now, the crux of the whole trick: If `filter` provided us with some kind of `coloration()` or `hue()` property, this would have been much simpler. But no, as of 2017 this doesn't exist, so we have to hack it. Instead, we can use `sepia()` to turn our gray into a brown:

<pre class='brush: css'>
.svg {
	filter: invert(.5) sepia(1);
}
</pre>
<img src="https://union.io/images/repo/20170811-07--1c7b57.png" alt="Sepia SVG" class="full">


So here we are, finally with some color we can manipulate. Using `saturate()` and `hue-rotate()`, we can fiddle with these values until we arrive at the desired color. These can be visually adjusted until you get the right shade, or inspected in software like Photoshop and precisely reverse-engineered. To get a nice bright blue, I used these values:

<pre class='brush: css'>
.svg {
	filter: invert(.5) sepia(1) saturate(5) hue-rotate(175deg);
}
</pre>

<img src="https://union.io/images/repo/20170811-08--62fa2d.png" alt="Blue SVG" class="full">


And that's it! <a href="https://codepen.io/ianm/pen/QMgrzq" target="blank">Check my CodePen example</a>, and play around with it to see how you can manipulate the fill color. You now have a super-fast, CSS-only way to change the fill of an SVG, even in an <code>&lt;img></code> tag, supported by every major browser (except IE). Enjoy!
