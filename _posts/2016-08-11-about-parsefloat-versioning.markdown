---
layout:         post
title:          "Front-End Dev Thought #2:"
subtitle:       "About Using parseFloat() for Versioning..."
date:           2016-08-11 12:00:00
header-img:     "img/post-bg-svgs-react-1.jpg"
thumbnail-img:  "img/post-thumb-svgs-react-1.jpg"
published:      true
category:       Code
readtime:       "4 minutes"
includeSyntax:	true
---

<p><span class='illuminated-letter'>T</span> here are a million reasons to love programming, and at least as many reasons to hate it. In programming, your grandest structures can be toppled by the tiniest mouse hole which, when you attempt to fill it, might actually lead down a winding, expanding air shaft to a fatal sinkhole gaping directly below you; one that will inevitably swallow your project whole. Time to demolish what you’ve built so far, code monkey. You’ll need to build elsewhere.</p>

<p>The abruptness of mentally gear-shifting from Grand Software Architect to Mouse Hole Filler is jarring, and leaves every ambitious developer in a chronic state of mild paranoia. Every mole hill might actually be a mountain—you just won’t know until you try to dig it up. The relationship between the enormous and the tiny is responsible for so much of what humans perceive about beauty, horror, and humor; this is also the core relationship between the programmer and the software they’re building.</p>

<p>It’s no surprise then that software bugs, the cause of so much programming grief, are also the cause of so much joy. The relief of your mouse hole being an inch deep is always a pressure release. Those daily wellsprings of hope help to punctuate the paranoia equilibrium, and that’s what leads me to believe that most software engineers, without knowing it, love being engineers <i>because</i> of bugs.</p>

<p>One bug that made me laugh until I snorted had to do with checking the version of a certain tool we use to track our front-end code packages. Using code to check the version of the tool that <i>manages</i> the code is a fairly common practice, but also varies greatly from tool to tool. Ours went something like this (this isn’t the real code):</p>

<pre class='brush: js'>
exec('npm --version', function (version) {
	if (parseFloat(version) < 3.5) {
		throw new Error('[ERROR] You need npm version >= 3.5');
		process.exit(1);
	}
});
</pre>

<p>So basically, the tool runs <code>npm --version</code> to return the version of <code>npm</code> being used, and the output, which might be something like <code>3.8.1</code>, is then compared to make sure it isn’t less than version <code>3.5</code>. If it’s less than <code>3.5</code> it throws an error, and you need to upgrade <code>npm</code>. Pretty straightforward.</p>

<p>But this stupid piece of shit kept failing on our build server. Our build server absolutely had a new enough version of <code>npm</code> (we were using <code>3.10.4</code>) and yet it kept throwing that stupid error. This script worked on all of our other servers, most with even older versions like <code>3.7</code> or <code>3.8</code>! What gives?? The mouse hole got deeper and deeper, as we were imagining all the yawning cenotes this might lead to, directly underneath the foundation of our precious new house.</p>

<p>Do you see the bug yet? If you don’t, feel free to ruminate on it for a while before I explain it.</p>

<p>The answer: It was <code>parseFloat()</code>. Parse fucking float. We were passing the version through <code>parseFloat()</code> which took the output (a string, which can’t be compared to a number), and converted it into a floating point number (which could then be compared with the number <code>3.5</code>). But in doing so, <code>parseFloat()</code> took our version of <code>3.10.4</code> <i>and turned into</i> <code>3.1</code>. It didn’t keep the trailing zero, because why would it? And, goddamnit, <code>3.1</code> is less than <code>3.5</code>. The mouse hole was only an inch deep and I felt like a complete moron. But one very relieved moron. I laughed until I snorted.</p>

<p>These kinds of bugs affirm why I both love and hate what I do. And if you ever reach the point where you stop laughing at your bugs, I don’t think you’ll be a programmer for very much longer.</p>
