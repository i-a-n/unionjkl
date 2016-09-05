---
layout:         post
eyebrow:        "Front-End Dev Thought #0000001:"
title:          "Managing inline SVGs with React/Webpack"
date:           2016-07-22 12:00:00
header-img:     "img/post-bg-svgs-react-1.jpg"
thumbnail-img:  "img/post-thumb-svgs-react-1.jpg"
published:      true
category:       Code
readtime:       "8 minutes"
includeSyntax:	true
---

<p><span class='illuminated-letter'>A</span> t work this week, I found myself tasked with developing something that sounded fairly simple: A React web component that accepts the name of an icon, and returns an inline SVG of that icon. Such that I could write this:</p>

<pre class="brush:xml">

&lt;Icon name="exampleIcon" /&gt;

</pre>

<p>And it would return this:</pre>

<pre class="brush:js">
<svg viewport="0 0 72 72">
	<d path=/*** actual "exampleIcon" SVG data here ***/ />
</svg>
</pre>

<p>As is the case with, oh I don&rsquo;t know, say, ⅔ of all simple-sounding dev tasks, it turned out to be not a simple dev task at all. Maybe even the opposite of a simple dev task. And it took me enough Googling and gnashing of teeth that I feel compelled to document the solution I developed, so that if I ever need to do it again I&rsquo;ll have a handy reference, and also in the event someone else finds their way to this post under similar circumstances they might get a few questions answered.</pre>

<h3 class="section-heading">1. The Setup</h3>

<p>The setup is pretty standard React-web-app-in-2016 fare. We&rsquo;re using React, and Webpack, and all the typical Node, ES6, and JSX hipster stuff that comes with it. Our icon component, aptly named <i>Icon</i>, is boiler plated like so:</p>

<pre class="brush:js">
const Icon = (props) => (
	<svg
		className={ props.className }
		viewBox="0 0 72 72"
		width={ props.width }
		height={ props.height }
	>
		{ props.title && <title id="title">{ props.title }</title> }

		/*** Inline SVG data should go here ***/

	&lt;/svg&gt;
);
</pre>

<p>Yes, we could&rsquo;ve simply used <code>&lt;img src="exampleIcon.svg"&gt;</code> and inserted the SVG that way, but we wanted inline SVGs for a number of (quite valid) reasons.
Yes, we could&rsquo;ve imported an object with SVG data, or a bunch of modules that exported SVG data, but we wanted to be able to simply drop in raw SVG data to a folder somewhere and not worry about writing any code or running any generators.
And before you ask, no, we didn&rsquo;t want to give up the boiler plate <code>&lt;svg&gt;</code> tag attributes, we wanted those four big beautiful attributes (<code>className</code>,<code>viewBox</code>,<code>width</code>,<code>height</code>) to be applied just like that, to all SVGs coming through this pipeline.</p>

<p>Okay, so what&rsquo;s our first step here?</p>

<h3 class="section-heading">2. The Wrong Approach</h3>
<p>My initial line of thought was <i>let&rsquo;s just do some kind of <code>import *.svg</code> or something! That&rsquo;ll import all the SVGs we dropped into the icon directory</i>. But of course it isn&rsquo;t that easy. Here are a few things that absolutely don&rsquo;t work:</p>

<pre class="brush:js">
/*** Doesn't work, because ES6 won't batch-import .svg ***/
import * as iconObject from './icons';
import * as iconObject from './icons/*';
import * as iconObject from './icons/*.svg';

//** Doesn't work, because import has to come first **/
$listOfSVGs.forEach(svg => import svg)

/*** Also doesn't work, don't ask me why ***/
const icons = require('./icons')
const icons = require('./icons/*.svg')
</pre>

<p>My next big stupid idea was to use NodeJS, or some other Node plugin, to do the filesystem magic, and return that precious list of SVGs in the icon directory. Then maybe we could <code>require()</code> them one at a time. &ldquo;Now I got you, suckers!&rdquo; I stupidly said to myself, to the SVGs.</p>

<p>First up was my attempt to use the "fs" filesystem plugin that comes standard with Node:</p>

<pre class="brush:js">

const fs = require('fs');
iconData = fs.readFileSync("icons/*.svg", "utf8")
</pre>

<p>This fails miserably: <code>"Module not found: Error: Can't resolve 'fs' in '/app/icons'"</code>. Well, okay, turns out you need to make a space for the "fs" module in your Webpack config. So I did that, and it led me to maybe the most frustrating, misleading error I&rsquo;ve seen in my life:</p>

<pre class="brush:js">

Uncaught TypeError: fs.readFileSync is not a function

</pre>

<p><code>Uncaught TypeError: fs.readFileSync is not a function</code>. Read over those words and seethe. Why is <code>readFileSync</code> in all of the fs documentation if it doesn't actually exist? Why doesn&rsquo;t this fail until I run it in a browser, and not at a build level? Why?? This is hell, my friends. This is hell.</p>

<p>I&rsquo;ll spare you the dramatics and cut to the chase. It turns out I had an understanding of the entire concept of React, Node and Webpack that I&rsquo;d now categorize as "deeply flawed" in this regard. I was treating these tools, the very things stitching together my files to display in a browser, as if they were exclusively back-end tools. They aren&rsquo;t. Node, and my "fs" function, will only have access to the filesystem when the <i>server</i> is running it. When the browser is running it (or, more precisely, when the browser is running what Webpack has stitched together), it has no such filesystem access (for fairly obvious reasons). In some respects, what I was trying to do is the whole <i>point</i> of Webpack, or Browserify, or any of those kinds of tools. You can&rsquo;t use Node to do filesystem work for your browser in this fashion.</p>

<p>Anyway, it took me much longer than this one paragraph to understand that, and I tried browserify-fs and rbfs and a few other things to try and get around it, but they were either too much overhead or just the wrong tool for the job. The correct tool for the job is going to be Webpack&rsquo;s implementation of dynamic requiring. <i>Because Webpack is what&rsquo;s doing the filesystem work for the browser, dummy!</i> I finally realized to myself.</p>

<h3 class="section-heading">3. Setbacks and Common Errors</h3>

<p>The first problem you&rsquo;ll run into is that Webpack just chokes real hard on the whole concept of an .svg file. An error like this will pop up: <code>"Module parse failed: /app/icons/svg/icon.svg Unexpected token (1:0) ... You may need an appropriate loader to handle this file type."</code> That&rsquo;s because if we&rsquo;re going to handle a bunch of SVGs like raw data, we&rsquo;ll need to parse them like raw data. In your Webpack config, add this in the appropriate place:</p>

<pre class="brush:json">
module: {
	loaders: [{
		{
			test: /\.svg$/,
			loader: 'raw'
		}
	}]
}
</pre>

<p>Of course, since nothing is free, you&rsquo;ll need to use NPM or similar to install the "raw-loader" part. For most setups it&rsquo;s as simple as:</p>

<pre class="brush:shell">

$ npm install raw-loader --save

</pre>

<p>I also spent too long attempting to do all of the looping, parsing, and logic in the React component code itself. There&rsquo;s no need to do that, and JSX is actually really awful for that (likely by design), so I&rsquo;d recommend just offloading all the hard work to a new file, and using a conventional <code>require()</code> to import it. You&rsquo;ll see what I mean in the next bit.</pre>

<h3 class="section-heading">4. The Solution</h3>

<p>Here&rsquo;s what I came up with, and, against all odds, it actually works. I&rsquo;ll explain line-by-line after the jump:</p>

<pre class="brush:js">
/** `Icon.component.js` **/
const iconSVGData = require('../icons/index.js');

const Icon = (props) => (
	<svg
		className={ props.className }
		viewBox="0 0 72 72"
		width={ props.width }
		height={ props.height }
	>
		{ props.title && <title id="title">{ props.title }</title> }
		<g dangerouslySetInnerHTML={ { __html: iconSVGData[props.name] } } /> // This is the important bit

	</svg>
);
</pre>
<pre class="brush:js">
/** `icons/index.js` **/

const iconRequireObject = require.context('./svg', true, /.*\.svg$/); // require all .svgs in the ./svg folder
const exports = module.exports = {};
const iconList = [];

iconRequireObject.keys().forEach(path => {
	const iconName = path.substring(path.lastIndexOf('/') + 1, path.lastIndexOf('.')); // find the bare name of the icon
	exports[iconName] = iconRequireObject(path);
	iconList.push(iconName);
});

exports.iconList = iconList;
</pre>
<pre class="brush:xml">
&lt;!-- icons/svg/exampleIcon.svg (example SVG path) --&gt;
&lt;d path="1a,2b,3c,[...],1a,2b,3c"&gt;
</pre>

<p>So there you have it. What does it all mean? Here&rsquo;s a line-by-line breakdown:</p>

<h4>Icon.component.js</h4>
<p>In the first file, we simply <code>require()</code> the second file (line 2), and, within the component, add a <code>&lt;g&gt;</code> tag with the raw SVG data (line 12). Notice the <code>dangerouslySetInnerHTML</code> feature, which the React developers purposely crafted to sound scary. Mainlining raw code into your component&rsquo;s veins is generally frowned upon but in this instance, it&rsquo;s totally fine. I threw it into a <code>&lt;g&gt;</code> tag, just because it was simpler than factoring in the <code>&lt;title&gt;</code> tag to live as its sibling (if you inject innerHTML there can&rsquo;t be anything else living there already). You&rsquo;ll notice I used <code>iconSVGData[props.name]</code> to retrieve the raw data. So that means our second file will have to export that data in that format.</p>

<h4>icons/index.js</h4>
<p>In the second file, line 3, we use "<a href="https://webpack.github.io/docs/context.html" target="_new">require.context()</a>" to get a list of SVG files sitting on the filesystem. It also does the actual importing of those files, but we&rsquo;ll have to use it like a function to return that data (see line 9). Lines 4 and 5 are just setting variables, and line 7 just loops over the names of the files. So all we have to do is get the raw icon name (line 8), make sure we&rsquo;re exporting it properly (line 9), and then add it to a list (lines 10 and 13). Adding it to the list is actually optional, but I needed it for a style guide app we run (long story), so you can safely ignore that.</p>

<h4>icons/svg/exampleIcon.svg</h4>
<p>This is just any ol&rsquo; SVG, but without the <code>&lt;svg&gt;</code> tag. Path info only! Therefore, the final Icon component just needs to be built like this:</p>

<pre class="brush:xml">
&lt;Icon name="exampleIcon"&gt;
</pre>

<p>And we&rsquo;re done! The component uses the name we supply to get the icon data of the same name from the <code>icons.index.js</code> exports! It&rsquo;s front-end magic.</p>

<h3 class="section-heading">5. Conclusion</h3>
<p>Now, with this setup, all we have to do is drop any number of SVG paths into the <code>icons/svg</code> directory, and our app will instantly know about it and be able to inject it, based on its filename, into the Icon component. I understand this isn&rsquo;t a very advanced solution, or a particularly elegant one, but I wasn&rsquo;t able to find a good example of this on any of my normal channels, so hopefully this will be helpful to someone else trying to do the same thing.</p>

<p>Good luck out there, kids. You&rsquo;ll need it.</p>
