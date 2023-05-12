---
layout: post
title: "The “Next-Minor” Versioning Strategy"
subtitle: "My first-hand account of a popular git branching & releasing methodology"
date: 2023-05-11
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-nmvs.png"
published: true
category: Code
includeSyntax: true
includeLightbox: true
---

<span class='illuminated-letter'>I</span>’ve had some trouble researching “git versioning strategies” in the past. Part of the trouble is searching Google, whose current search algorithms so ruthlessly optimize for “most people search THIS, so that’s what you must’ve meant” and “here is the one-sentence result that our Google Assistant can read to you from your smart microwave” that finding blog posts on abstract versioning-releasing strategies is nearly impossible. But part of the trouble I think is that people don’t generally write too many articles about something as “internal” as software versioning best practices. Instead, those articles are generally found in README files in their private github repos.

So here’s my accounting of my team’s “Next-Minor” versioning strategy, which dictates the structure of our git repositories’ branches, tags and releases. This post might serve no purpose other than to remind me how we did all this stuff the next time I need to set up a new large project.

This strategy is a very common one, in use across all kinds of software products. I don’t know if it has an official inventor or even a commonly-accepted name; if it does, I can’t find it. So I’m going with Next-Minor Versioning Strategy (NMVS). Because, as the strategy goes, your code on <code>main</code> will always be the _next minor_ release.

## Terminology

For simplicity’s sake, I’ll refer to the main trunk of your codebase as <code>main</code> (historically sometimes called <code>trunk</code> or <code>master</code>). All versioning schemas will be in the [semver](https://docs.npmjs.com/about-semantic-versioning) style, of <code>major.minor.patch</code>, for example, <code>4.2.13</code>. Any examples or specific version control terminology will come from git and/or GitHub. But this strategy should work with any other VCS, or could be adapted to work with other versioning schemas.

## Summary

In short: <code>main</code> always contains all the newest code, and when <code>main</code> is released, it will be the _next minor_ version. For example, if the “current release” is <code>2.3.13</code>, the _next minor_ version will be <code>2.4.0</code>.

This means the _current minor_, in the above example <code>2.3.X</code>, is maintained on its own branch—in this case a branch simply called <code>2.3</code>. That branch is where the _current release_ was cut from, and if there is a _next patch release_ (say, <code>2.3.14</code>), it would be cut from the <code>2.3</code> git branch as well.

In typical development cycles, NMVS dictates that you should always work against <code>main</code>, which means branching from <code>main</code> and merging back into <code>main</code>, and you should port only “bug fixes” to the _current minor_ branch (<code>2.3</code>).

I’m going to attempt to make a visual representation of this branching strategy. Historically, I’ve always hated these version control branching diagrams, and never really understood them, but maybe if I make one myself I’ll like it. Let’s try it out.

<a href="/img/nmvs/diagram-1.png" onclick="microLite(this); return false;"><img src="/img/nmvs/diagram-1.png" width="100%" class="inline" /></a>

Okay, this maybe works. It’s simplified, but covers the major point: the <code>main</code> branch, across the top, is where work happens. And releases from <code>main</code> are the next minor version. After a release, the version of the code on <code>main</code> is incremented (in this example, it’s the version in a <code>package.json</code> file, which gets incremented to the _next minor_, <code>2.5.0</code>).

The minor branch across the bottom, <code>2.3</code>, is where patch releases happen. After each patch release, the version of the code on the minor branch is also incremented. When the next minor is released from <code>main</code>, the old minor branch is effectively dead.

But where did that <code>2.3</code> branch come from? And what will replace it? Where does <code>2.4</code> come from? Well, I didn’t want to put all of that in the first diagram because things got too complicated. So the first diagram was a bit of a lie, and for that I apologize. But let’s look at what _actually_ happens during a release.

## Releasing code

Let’s see what the above diagram looks like when we add what actually happens for a new minor release from <code>main</code>:

<a href="/img/nmvs/diagram-2.png" onclick="microLite(this); return false;"><img src="/img/nmvs/diagram-2.png" width="100%" class="inline" /></a>

New minor branches are branched from <code>main</code> when the time comes for a new minor release, in the above example it was the <code>2.4</code> branch that was created.

All releases technically happen only from minor branches. (Even the release of a new major version, say <code>3.0</code>, is technically the patch release of <code>3.0.0</code>.)

### How-To: Patch release

So let’s say we want to do a patch release of version <code>2.3.13</code> in this example. The steps are:

1. Checkout the minor branch from which to cut the release. (Make sure it’s up to date by fetching/pulling if necessary.)

<pre class='brush: bash'>
git checkout 2.3
</pre>

2. Use <code>git tag</code> to tag the release.

<pre class='brush: bash'>
git tag 2.3.13
git push origin 2.3.13
</pre>

3. Head back to the minor branch and increment its version in the code.

<pre class='brush: bash'>
git checkout 2.3
[edit package.json files, etc, to update version to 2.3.14]
</pre>

That’s it. The version management part is done. Now all you need to do is actually build/release the code you tagged with <code>2.3.13</code>.

Typically you would check out that tag:

<pre class='brush: bash'>
git checkout 2.3.13
</pre>

Then follow release steps specific to your code base. In many cases this will involve building images or making executables... That sort of thing.

At this point I also like using GitHub’s Releases interface to create an official release for <code>2.3.13</code>, so it can be a documented artifact. See [GitHub’s docs](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release) for how to create a release in your repository.

### How-To: New minor release

If you want to release a new minor, which comes from the code on <code>main</code>, there’s really only one unique step: You need to create a branch off of <code>main</code>! First, ensure you are on <code>main</code> and have pulled in the latest code. Then, create the new minor branch. In this example, the _existing_ minor branch was <code>2.3</code>, so we will create <code>2.4</code> from <code>main</code>:

<pre class='brush: bash'>
git checkout -b 2.4
git push origin 2.4
</pre>

The version of the code in <code>main</code> should already be <code>2.4.0</code>, which means that the code in <code>main</code> needs to be incremented to <code>2.5.0</code> now:

<pre class='brush: bash'>
git checkout main
[edit package.json files, etc, to update version to 2.5.0]
</pre>

And you’re done. Now, you’ll follow the steps above for a _patch release_ from the new minor branch you just created (<code>2.4</code>). Your release will be <code>2.4.0</code>.

If this is making sense to you so far, but you feel like perhaps something’s missing, you’re right. We haven’t covered how to actually get changes INTO a minor branch. Up to this point, all of the coding and merging has happened only on <code>main</code>.

Once again I have lied to you. The above diagram was still too simplified; _backporting_ is the key feature that allows for patch releases, but I didn’t put it in the previous diagrams because, once again, they got too complicated. Please accept my apologies as we cover backporting.

## Backporting

<a href="/img/nmvs/diagram-3.png" onclick="microLite(this); return false;"><img src="/img/nmvs/diagram-3.png" width="100%" class="inline" /></a>

All code is merged into <code>main</code>, but only some code is backported to the current minor branch. Exactly what code does and does not get backported is up to you, but I like the rule that only bug fixes get backported.

As a result, all patch releases off the current minor branch will contain only relatively small bug fixes. And the next minor, from <code>main</code>, will contain all the new features.

Backporting is the process of selectively copying specific commits from one branch to another. In the context of NMVS, backporting involves cherry-picking commits from <code>main</code> to the “current minor” branch.

You can perform a backport manually after merging code into <code>main</code> using <code>git</code>. The primary command for copying individual commits is <code>git cherry-pick</code>. The command takes the commit hash or reference as an argument and applies the changes made in that commit to the current branch.

For example, to backport a single commit with the hash <code>abcdefg</code> from <code>main</code> to the current minor branch <code>2.3</code>, you would run the following commands:

<pre class='brush: bash'>
git checkout 2.3
git cherry-pick abcdefg
</pre>

It’s possible at this point you’ll encounter a code conflict, and git will prompt you to resolve it. But in my experience this is surprisingly rare, as only bug fixes were ever backported to the current minor branch _after_ already applying them to <code>main</code>, so things generally keep in sync.

But, if you do manual backporting, you’ll probably need to brush up on [some full documentation](https://www.atlassian.com/git/tutorials/cherry-pick) for the <code>cherry-pick</code> command.

To simplify the backport process, you may want to consider a backporting helper library. I recommend [backport](https://www.npmjs.com/package/backport) if you’re working with a node project. It also has extensive documentation on how to automate backporting with GitHub actions, that way PRs labeled as “bugfix”, for example, can be automatically backported when the PR to <code>main</code> is merged. It’s a huge timesaver, highly recommend.

## Releasing a Major Version

Eventually the time might come when you want to release a major version; if we keep our examples above going, this would be version <code>3.0.0</code>. What then? All you have to do is increment the version on <code>main</code> to the next major, instead of the next minor.

<img src='/img/nmvs/diagram-4.png' class="full">

And what if you want to release the next major version _now_, not after the next release? Well, folks, it’s so straightforward I can hardly stand it.

<img src='/img/nmvs/diagram-5.png' class="full">

Yep, just increment the version of the code on <code>main</code> to the next major version, then proceed as normal to a release.

## Conclusion

NMVS is currently in use all over the place, in software projects of all sizes, and works at scale well enough to support even the largest code bases.

I find it keeps releases smaller and more predictable, doesn’t burden developers with having to worry about managing tons of branches or having to know which release their code needs to target; you always work from, and to, <code>main</code>.

NMVS does have its drawbacks. I don’t find it particularly intuitive. And, although it makes developing simpler, most of that complexity has simply been stashed away in the backporting and releasing tasks. So it absolutely requires good documentation and at least one experienced developer to help keep things straight during the first few releases.

I do think, overall, NMVS is worth it. And if you think so too, maybe it’s the right system for your next project. Which means we’re finally ready for the last, final, way-too-detailed diagram of ultimate complexity. This is NMVS. I’m sorry:

<a href="/img/nmvs/diagram-complete.png" onclick="microLite(this); return false;"><img src="/img/nmvs/diagram-complete.png" width="100%" class="inline" /></a>
