---
layout: post
title: "Introducing ASTRA"
subtitle: "The Aggressively Simple Template for React Apps"
date: 2023-10-29
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-bitwise.png"
published: true
category: Code
includeSyntax: false
includeLightbox: true
---

<span class='illuminated-letter'>A</span>lmost everyone who makes web apps seems to hate web apps, I've noticed. And, more specifically, they hate the complexity that manages to find its way into doing anything, no matter how simple. A modern web app that just says "Hello world!" requires like five thousand times more computing power to render than the entire Apollo space program used to put humans on the moon. The size of the web app itself, counting its dependencies, is probably more than any single consumer computer could store before the 1990s. There has to be a better way.

There are a million "better ways", of course. Every major front end template out there claims to have finally simplified the process of creating a web app, keeping you the developer from any unnecessary complexity or hoop-jumping with their ruthlessly optimized, strongly-opinionated boilerplates.

But this isn't really true. They may have kept complexity away from the developer, but it was just by stashing that complexity elsewhere temporarily. `create-react-app`, the one-time defacto React templating library, essentially just developed a ferociously complicated front end application, packaged all of the configs and scripts up into their own little dependencies—dependlets if you will—and gave you a `package.json` wrapper around them with which to run two or three commmon build-and-serve commands. The _dependlets_ option proved to be a popular one, probably because it meant your top-level template could just import one single depdendlet! Wow, so “““simple”””! Unfortunately, the actual truth is not so simple.

They still configure webpack using voodoo magic. They still have to deal with upgrades to babel and jest and enzyme and whatever the hell else. It's all still there. They still firebomb your hard drive with 300+ `node_modules` packages just to serve "Hello world". And if you want to do something differently than the way they planned ("eject", in `create-react-app` language), you better pray there's a tutorial or accurate Stack Overflow answer, and the walkthrough you're currently on step 16/22 of wasn't made obsolete when the React team bumped their dependlet from version `3.4.2` to `3.5.0`.

"This sucks", I thought to myself for the ten billionth time last week, as I wanted to stand up a super quick React app to display a few cooking recipes my wife sent me. "I just want a 'Hello World' React app I can build and send to my web server to host as HTML/JS/CSS. I just want a codesandbox I can control."

### Enter bun.sh

The ten billionth complaint proved to be the magic number, since I remembered that [bun](https://bun.sh), a new Node replacement ecosystem, had just released their big `1.0.0` version last month. They made big promises about rewriting all of the Node stuff that was too complex, and using it to do all the basic stuff that Node and JavaScript apps currently needed colossal, inscrutable libraries to accomplish.

I decided to see how far I could ride the bun train. The list of things it purported to be able to replace in my React ecosystem was astounding. It claimed it could replace:

- webpack (or any bundler at all)
- babel
- standalone typescript compilers
- jest/enzyme/mocha
- expressjs

I'll cut to the big reveal a little early: I was indeed able to replace every single one of those things with a nearly-no-code `bun` version.

I finished [my recipes app](https://github.com/i-a-n/basic-recipes-app) in just a few days, and it was a pleasure to develop. Just a handful of React components compiled into a single `.js` file, linked from an `index.html` I could look at in my browser locally. Yes friends, I could just visit a `file:///` URL in Chrome to see my web app. No web server, no CSS-loaders or whatever, no weird army of `chunk-main-abcdef123467890.js` files getting cached who-knows-where and injected who-knows-how. So pleasant. So quaint.

"I should make this a template so I can do it again next time I want to make a quick app", I thought.

### The end result

And so a few days later I finished developing [ASTRA](https://github.com/i-a-n/astra), the aggressively simple template for react apps. I thought about naming it something cooler like Astroturf, but decided against it, because it is not a cool library. It's just, essentially, three `bun` commands that you can run using `npm`, and two directories: one to make your app, and one for the build output. It really can't get much simpler than this.

<a href="/img/astra/number-of-packages.png" onclick="microLite(this); return false;"><img src="/img/astra/number-of-packages.png" width="100%" class="inline" /></a>

<a href="/img/astra/time-to-build.png" onclick="microLite(this); return false;"><img src="/img/astra/time-to-build.png" width="100%" class="inline" /></a>

But within this simplicity is power. When I thought about how to best add routing to my recipes app, I felt something strange, something I hadn't felt in a while when working in the Node/React ecosystem: excitement. My options were endless! I could use _any router I wanted_, and not only that, I didn't have to worry about it being compatible with Babel-TypeScript-React-JSX-ECMAScript2016 or whatever. It was just going to work because I am using nothing except React. Instead of being bound by whatever "super fast! super opinionated!" router Next.js or whoever chose for me, I was liberated to do absolutely anything.

In fact, it occurred to me, I'm not even bound to make my recipes app a single-page-app. I could just, you know, copy `index.html` into `add-recipe.html` and then target that file with a different React `createRoot` render! This multi-page pattern, once the normal way to make web pages by the way, has been entirely abandoned by a generation of web developers, so much so it is seemingly _impossible to do_ with any other front end framework... But how many small-app developers could have saved a ton of agony by just making another `.html` file? How many small projects should have at least had the freedom to _consider_ that as an option??

ASTRA reintroduces that little spark of possibility.

And all because it's just aggressively simple.

---

### Postscript

I want to end on a philosophical note, and this is probably all a bunch of privileged navel-gazing, but it's how I genuinely feel. Often times we find cures for awful things and the cures are so good they seem to eradicate the Awful Thing entirely. And then the generation of people who experienced that Awful Thing die and the next generation of people are left wondering why we have to keep doing this whole Cure thing, because the Cure itself takes some work to maintain and hey, we can just stop doing this slightly difficult Cure thing.

Sometimes the new generation is right, and we really _can_ stop doing the Cure Thing. Sometimes a colony no longer needs to send money to the metropole; the things they were "curing" have disappeared or changed and the colony can now maintain independence. Wipe the slate clean folks, let's start over.

But other times the new generation doesn't realize the Awful Thing is still there, and the Cure really is worth the trouble. Like with NATO or the measles vaccine—the cost of the Cure is actually tiny compared to the thing it's preventing (world war and children dying, respectively). But sometimes it's harder to see the Awful Thing lurking in the shadows, and just wiping everything off the table and starting clean feels like the easier answer.

I'm hopeful my React template is closer to the former situation, where the overwrought complexity of modern web apps has simply gotten so bad it no longer is preferable to the stuff it was trying to "cure" for most use cases. However, I do want to assert that there is a good chance I'm doing something closer to the latter situation, where I'm throwing 10+ years of good ideas into the trash just because I don't know how Awful it really is out there. There's a chance someone using my template will encounter just as much pain in the long-run because of the things I foolheartedly left out than the simplicity I introduced.

But sometimes the only way to know is to wipe away the Cure for a while, and see how it all shakes out.

Good luck out there.
