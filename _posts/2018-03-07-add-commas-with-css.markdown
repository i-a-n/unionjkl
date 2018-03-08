---
layout:          post
title:           "A Pure CSS Solution for Adding Commas Between List Items"
subtitle:        "...With an ‘and’ at the end, for good measure"
date:            2018-03-07 12:00:00
header-img:      "img/post-bg-svgs-react-1.jpg"
thumbnail-img:   "img/post-thumb-svgs-react-1.jpg"
published:       true
category:        Code
readtime:        "4 minutes"
includeSyntax:   true
includeLightbox: false
---

<span class='illuminated-letter'>O</span>ne thing I love doing, and probably spend too much time doing, is finding ways to use pure CSS to solve problems you might think only JavaScript would be able to solve. Animations, <a href='/code/2017/08/10/img-svg-fill/' target='blank'>image manipulation</a>, that sort of thing. Using CSS instead of JavaScript (or server-side rendering) offers a few unique advantages: It's usually faster for the user to load and execute, it can take advantage of hardware acceleration and, in many cases, it can be more browser-agnostic. Also, if you want to test out some wacky CSS idea, all you have to do is fire up a <a href='https://codepen.io/' target='new'>CodePen</a> and you’re looking at pretty much the most advanced CSS IDE available. No builds, no NPM packages, just code and go.

So, a coworker asked my web team for a new feature this week: On our website, where the authors of an article are listed, they wanted the authors’ names to be separated by commas—except the last author, whose name should be preceded by _and_. So a list of four authors with markup like this:

<pre class='brush: js'>
<span>Author1</span>
<span>Author2</span>
<span>Author3</span>
<span>Author4</span>
</pre>

... Should look like this:

<pre class='brush: js'>
Author1, Author2, Author3 and Author4
</pre>

For any number of authors.

I immediately wondered whether we could do this with CSS. Sure, we could do it with Rails or JavaScript in like five minutes, but hey, I had fifteen minutes free and a CodePen editor already up and running. Why not give it a try?

I came up with something simple enough to code with only two CSS blocks, but complex enough to be a lot of fun to try and decipher. I’ll explain it below, but first, If you’re just reading this post for the solution, well, here it is:

## The solution

<p data-height="265" data-theme-id="0" data-slug-hash="zRgNWy" data-default-tab="result" data-user="ianm" data-embed-version="2" data-pen-title="Insert commas & 'and' with CSS only" class="codepen">See the Pen <a href="https://codepen.io/ianm/pen/zRgNWy/">Insert commas & 'and' with CSS only</a> by Ian M (<a href="https://codepen.io/ianm">@ianm</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## The explanation

Let’s take it line-by-line, with the important bits written in SCSS. Assuming each list item is wrapped in a <code>span</code> tag:

<pre class='brush: sass'>
span + span:last-child {
	&::before {
		content: " and ";
	}
}

span:nth-of-type(n + 2):not(:last-child) {
	&::before {
		content: ", ";
	}
}
</pre>

The first line, <code>span + span:last-child</code>, means this: Select every <code>span</code> that is 1) the _last child_ in the series, and 2) is also the _next-sibling_ of another <code>span</code>. This ensures that you’re only grabbing the final item of a list if that list has more than one item! We don’t want to select an item in a list that only has one thing in it.

The second line, <code>&::before</code> in SCSS, just creates a pseudo-element before that final item, and injects <code>" and "</code>. These are the blue items in the example above. Note the spacing! (Also note if you aren’t using SCSS, you can do this in plain CSS by making that first line <code>span + span:last-child::before</code>.)

The second block, <code>span:nth-of-type(n + 2):not(:last-child)</code>, is the business end of this trick. Let’s break it down:

### <code>span:nth-of-type(n + 2)</code>
This selects every item in the list that is _at least the second item_ of its type. Basically, everything but the first one.

### <code>:not(:last-child)</code>
And this ensures we are _not_ selecting the final item in the list. We’re already selecting that with the first rule!

So after selecting them (they’re the red items in my example), we add a <code>::before</code> pseudo-element to inject a comma and a space before the item. Simple!


## Conclusion

That’s it! Just a fun, simple way to insert smart delimiters into list items using CSS. Give it a try. And the next time you’re given some relatively small front end task, ask yourself: “Can I spend slightly too much time engineering a way to solve this with CSS?” And then, later, “should I really write a blog post about this dumb thing I did?” If you’re like me, you’ll answer yes to both of them. For better or for worse.
