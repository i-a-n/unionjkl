---
layout:         post
title:          "Can You Tell the Difference Between Finnegans Wake and Total Nonsense?"
date:           2016-11-30 12:00:00
header-img:     "img/post-bg-finnegan-1.jpg"
thumbnail-img:  "img/post-thumb-finnegan-1.jpg"
published:      true
category:       Thoughts
readtime:       "5 minutes"
includeSyntax:	true
---

<p><span class='illuminated-letter'>I</span>f you aren’t familiar with Markov chains, well, don’t beat yourself up over it. Their simplest summary is way too simple (“a state that can be immediately deduced from an earlier state”, thanks <a href="https://en.wikipedia.org/wiki/Markov_chain" target="new">Wikipedia</a>!) and yet their real-world applications are ferociously complicated. There’s not much in-between. They’ve been around for a while but have found mainstream recognition only recently, as computing power is finally becoming cheap enough to calculate some huge, truly interesting states from “stateless” data.</p>

<p>One fairly mind-blowing use of Markov state computation is the <a href="https://erikbern.com/2014/11/29/deep-learning-for-chess/" target="new">Deep Pink chess engine</a>: It was trained purely by “observing” billions of chess moves. By using these to predict a strong “next state” of a chess game, it became a very good chess player without ever being programmed to understand how any single piece moves. It technically doesn’t know what chess is, it’s just really good at predicting what the next state of a chess board should look like.</p>

<p>Another neat use of Markov chains is in natural language generation. You can feed a Markov-inspired language generator a bunch of text (the more the better) and it’ll “predict” any amount of words, sentences, and paragraphs that might be “coming up next.” Now, it really doesn’t <i>predict</i> anything, because text generators can currently only analyze syntax, grammar, and vocabulary; meaning is entirely lost to the computer, so it comes up with text that <i>kinda sounds like</i> human language, but is basically gibberish. Which leads me to <i>Finnegans Wake</i>&hellip;</p>

<p>If you aren’t familiar with <a href="https://en.wikipedia.org/wiki/Finnegans_Wake" target="new">Finnegans Wake</a>, don’t beat yourself up over it. It was written by world-famous novelist James Joyce between 1922 and 1939, and English majors are still losing nights of sleep trying to figure out whether it actually means anything. And I don’t mean that in a sort of subjectivist, <i>“Does anything really mean anything?”</i> kind of way, brought up in passing by elbow-patched University professors over steeping teabags in dusty lounges on the edge of campus; I mean there still is literally no consensus—academic or otherwise—on whether it is <i>600 pages of entirely made-up nonsense</i>.</p>

<img src="https://union.io/images/repo/20161205-02--f031de.jpg" class="full" alt="A passage from Wake">
<span class="caption text-muted">A typical passage from Finnegans Wake</span>

<p>Joyce may have been playing a joke on the literary community, or, he might have changed the very definition of the novel. We don’t know. And barring any new personal revelation, we might never. I was leaning, personally, toward believing Joyce: Reading a few passages from <i>Wake</i> always overwhelms me, but there is an undeniable, unmistakable thread of constancy running through it, I find. It might be as little as two separate words a paragraph apart, but something always seemed to tell me that each page meant something deeper, and I was willing to give the author the benefit of the doubt.</p>

<p>Until I ran it through a Markov text generator.</p>

<p>When I found <a href="https://github.com/jsvine/markovify" target="new">this simple Markov text generator</a> a few days ago, I almost immediately knew I had to train it on <i>Finnegans Wake</i>. While analyzing <i>Wake</i>, humans get stuck on things like trying to decipher the meaning behind one of Joyce’s forty-five letter words with eighteen Zs in it. But a Markov text generator would just note it and move right along, using it only to inform its memory store that long words with lots of Zs are slightly more likely to occur. I coded the Markov program to read <i>Wake</i>, parse the results, and then begin predicting more of its text, based on its entire grammar, syntax, and vocabulary at once. This type of analysis, once nearly impossible, now takes only minutes.</p>

<p>And when I saw the results, I almost didn’t believe it. Feel free to <a href="https://union.io/wake" target="new">try telling the difference yourself</a>.</p>

<img src="https://union.io/images/repo/20161205-08--bb0d1a.jpg" class="full" alt="Wake vs a Markov generator">
<span class="caption text-muted">A passage from Wake on the left, and a Markov generator on the right.</span>

<p>In many cases, the language generator actually <i>makes more sense</i> than the original text. The output, entirely devoid-of-meaning, seems to equal the original text in substance as well as style. I watched the results coming in, generating more and more text, in a state of disbelief. You could easily insert the computer’s output anywhere within <i>Wake</i>’s 600 pages and practically no one, no one in the world, would be able to tell.</p>

<img src="https://union.io/images/repo/20161205-07--27bcfa.jpg" class="full" alt="Wake vs a Markov generator">
<span class="caption text-muted">Can you tell which passage is from Wake, and which is computer-generated?</span>

<p>So does that settle it? Was Joyce a fraud? Is his text, <i>now verifiably nearly-indistinguishable from gibberish</i>, as devoid of narrative as my program’s code? Not so fast.</p>

<p>I’m no English major, but I can recognize a few things we can’t take away from <i>Wake</i>. Firstly, the magnificently inventive vocabulary was entirely Joyce’s own. Sure, my program might be able to <i>reproduce</i> it, but it would never have been able to <i>invent</i> it. Even if the novel itself were meaningless, if you find meaning within a word, that honor belongs entirely to Joyce.</p>

<p>Secondly, even if the artist’s intent could somehow be proven machine-replicable, that doesn’t make it less valid. We could build a machine to paint like Van Gogh (or certainly Pollock), but this wouldn’t diminish the impact any individual work of art had on its observers. Perhaps part of the artist’s intent is to convey chaos, or even machine-replicability! For all I know, if Joyce were to rise from the grave and see the output from my Markov app, he might have a good laugh, lightly edit for theme, and happily publish it as <i>Finnegans Wake Part 2: Even Wakier</i>. And would that surprise anyone??</p>

<img src="https://union.io/images/repo/20161205-06--6cc65e.jpg" class="full" alt="Wake vs a Markov generator">
<span class="caption text-muted">I have honestly lost my note on which passage is which; I really don’t know which is Joyce and which is Markov-generated.</span>

<p>In the end, I have to admit my opinion on <i>Wake</i> has changed because of this. I’m willing to accept now, fully, that its internal cohesiveness is no more difficult to generate than nonsense. But, my admiration for it, and certainly for Joyce, has actually appreciated.</p>

<p>If nothing else, he was a Markov language generator 80 years before they were invented.</p>
