---
layout: post
title: "Interviewing in the Age of AI"
date: 2025-02-18
header-img: "img/post-bg-phone-bonfire.jpg"
thumbnail-img: "img/post-thumb-phone-bonfire.jpg"
published: true
category: Code
includeSyntax: false
includeLightbox: false
---

<span class='illuminated-letter'>O</span>ne of the earliest and most successful applications of LLM-powered text generation was as a "coding assistant" for writing software. I wrote about an early release of Github's Copilot waaay back in <a href="https://blog.union.io/code/2021/07/14/code-robot/">July 2021</a> (!), ages before any of the modern "chatbots" were around. It was useful then, and has only become more useful since. These days, when pairing with another engineer at my company, I find it much more common to see a coding assistant installed in their code editor than not. And nearly every new feature I've seen developed over the past 18+ months in every project I'm a part of has tell-tale signs of AI or other LLM-powered code generation in it somewhere.

After some reflection on the topic, I've come to two conclusions: 1. AI coding assistants are extremely valuable, and 2. they will never go away. These two statements will disappoint a lot of people out there, but I've thought about this from every conceivable angle over the past 3+ years and I've been unable to change my own mind. This is our reality. Might as well accept it and move forward.

The consequences of this new reality are broad and deep. One place in particular has been completely disrupted: Interviews.

<div class='asterisk-spacer'> * * * </div>

I'm writing this in 2025. After the endless rounds of tech layoffs started by Musk's hostile takeover of Twitter in 2022, the industry as a whole has been much more conservative in its growth forecasting, and hiring across the board has been nearly wiped out for much of the past few years. Just now I'm starting to notice headcounts ticking up generally; I've gotten my first few unsolicited recruiter cold-calls this year for the first time in forever. And even my little team at work got approved to hire two more engineers. So it was time for me to, finally, interview some software engineers again.

But this presented a challenge I've never faced before in my career: Designing a software engineer interview in the age of AI.

There were a few ways my team and I considered approaching the design of a technical interview, which would be conducted via video call:

### 1. Hardline anti-AI, anti-Googling approach

Option 1 was to ask the interviewee to share their screen, and give them the technical challenge at the start of the interview, and ensure they did not use any AI code completion, chat bot, or search engine for the answer. This was the old-school method for conducting an interview in many traditional settings, and might still be the preferred method by more senior software engineers who were expected to just know syntax and library-specific methods by heart when they were hired ages ago, so that's what they still expect out of candidates.

### 2. Total disregard for method; results-only approach

Option 2 was to simply disregard the candidate's methods, and only concern ourselves with their result. This method, oddly, is also fairly common among software graybeards. "Take-home tests" are typically brutally difficult, but hey, if the candidate can solve it, they deserve the job, right?

### 3. "Pair-programming"/"whiteboarding" low-code or no-code approach

A third option would be a more abstract way to learn about the interviewee's abilities, and would somewhat sidestep the other two approaches entirely. Simply talking-it-out with the interviewer, possibly in a group setting that would mirror a real-life problem solving meeting, is one way to gauge someone's technical thought process without even concerning yourself with how well they can implement their ideas.

<div class='asterisk-spacer'> * * * </div>

Faced with these options, my team and I agreed on a hybrid design, combining all of the approaches above.

My thinking was this: Not letting an interviewee use a coding assistant is, in a very literal sense, purposely not testing for a skill that is a huge part of modern software engineering. Does the candidate understand how to construct a clear prompt, or write a descriptive function name or code comment for the LLM? Does the candidate understand that AI output must be thoroughly understood before being implemented? Does the candidate have the skill to _verify_, as opposed to the skill to _produce_ code? No matter your stance on AI in general, these skills are, today, vital parts of the job of software engineer. Explicitly not checking for these skills, I believe, is a bad strategy.

On the other hand, I didn't want to entirely disregard an engineer's methods for solving a problem and just give them a "take home" problem. A standard coding assistant (plus asking an advanced chatbot for help with more abstract concepts) really makes it possible for very novice engineers to "solve" very tough problems. And while leaning too heavily on AI to solve problems outside your area of competence might work for a coding interview, there will certainly come a problem in the near future that requires a more thorough understanding of the languages and libraries involved to effectively solve. I mean hey, if we just wanted a coding robot to do the work, we'd just.. use a coding robot.

So here's how we set up the interview:

— I created a [CodeSandbox](https://codesandbox.io) environment that contained a miniature web app that used the basic libraries we use on the team. In there, I put a couple of basic components together, and added a couple of tricky React lifecycle bugs, and some purposely inefficient architectural decisions.

— When the video interview started, I sent the link to the sandbox to the candidate, and asked them to share their screen

— As they prepare to solve the bugs, I reiterated multiple times:

- Please feel free to use any coding assistant, Google, AI, Stack Overflow, etc
- We don't penalize for it. I promise.
- We're evaluating your _approach_ to problem solving, and that includes the tools _you would normally use_ to do that.

— After the technical part of the interview, I blocked out 10 minutes to ask them what they thought of the mini web app, and whether they would architect it any different if they were in charge. This was more like a "whiteboarding" session, to gauge their bigger-picture thinking.

<div class='asterisk-spacer'> * * * </div>

In the end, I was surprised by the range of skills, competence and proficiency with AI the candidates demonstrated. It was really all over the map; I found it super illuminating to watch them interact with coding tools (every single one of them used at least one coding assistant), and I can truly say that watching them either "just let the assistant auto-complete all the code without checking it" vs. "provide a descriptive and performant prompt to the coding assistant and verifying the output" was an _enormously_ important difference to note! And even if the _result_ was the same, that first engineer would not succeed in the role. The latter engineer would be a huge asset to your team.

And if you didn't let them use AI in the interview, you'd never know the difference.
