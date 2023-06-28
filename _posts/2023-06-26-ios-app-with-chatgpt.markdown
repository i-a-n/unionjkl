---
layout: post
title: "I used ChatGPT to help me write my first iOS app. Here’s how."
subtitle: "An overview of 598 chat messages that built an open-source iOS app"
date: 2023-06-26
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-chatgpt.png"
published: true
category: Code
includeSyntax: false
includeLightbox: true
---

<span class='illuminated-letter'>T</span>he “app ecosystem”, as it exists today, is hopelessly broken.

Around the start of the pandemic I started cooking more, and shortly thereafter decided I wanted a recipe app. This idea immediately made me cringe. Just thinking about having to search “best recipe apps” on Google, getting 200 identical clickbait-and-popups-website results, going to the App Store and getting essentially three relevant results, all of which would inundate you with notifications, try to steal your contact list, block off key functionality to get you to subscribe, and on and on... What a fucking nightmare. Our entire modern app universe seems to be hopelessly, pitifully broken.

A year later my wife brought up essentially the same point when talking about trying to find a period-tracking app. It’s an absolute farce. The two or three major period-trackers in the App Store are patronizing, dark-pattern monstrosities, so manipulative and invasive they would probably be considered abusive if they weren’t all bathed in the same light pink pastel color swatches. “Can’t someone just make an app where you enter your period and then that’s it?” she said.

Finally, this year, I decided it was time to start writing down my friends’ birthdays somewhere. I always forget birthdays. I didn’t want to use any of my Google or Apple calendars. I didn’t want to sync it to my phone contacts. I just wanted to write down birthdays in an app and then maybe once a week get a notification if any birthdays were coming up. That’s it. Thinking about searching “best birthday app” made me want to jump off a cliff. Why is this so difficult? If only I were an iOS developer, I thought. If only I could make my own apps. I would make the simplest, easiest apps of all time. No bullshit, no clutter, nothing. You’d just anonymously sign in via text message so you could keep your data across devices, you wouldn’t have to pay or share your location or see ads. You’d just use an app.

But I’m a web developer, I said to myself, and I know absolutely nothing about app development. It was hopeless.

Until ChatGPT came along.

<div class='asterisk-spacer'> * * * </div>

<a href="/img/chatgpt/ss-0.png" onclick="microLite(this); return false;"><img src="/img/chatgpt/ss-0.png" width="100%" class="inline" /></a>

I use ChatGPT daily for my job. I mainly write TypeScript/Node apps, with a few other web-friendly languages thrown in there. And ChatGPT has saved me literally hours every single week, writing up utility functions (“how does <code>filter().reduce()</code> syntax go again? Oh yeah, ChatGPT can just write this for me.”) and finding lower-order bugs in code snippets I didn’t want to spend time debugging if I can help it.

I’ve gotten really familiar with using ChatGPT for JavaScript (a language I know well). I’ve seen its shortcomings and have been, generally, quite impressed with its knowledge. So one day, while using ChatGPT to help me with my code, it occurred on me: Could I use this chat robot to teach me how to make an iOS app? I started a new chat:

<blockquote>in this exercise I will be creating a simple application to store my friends’ birthdays, first as a web app, then as an iOS app, and you will be acting as an app developer who assists and consults on each step of the process.</blockquote>

This was the first of 598 messages shared between me and the chat robot over the course of three weeks. It was truly fascinating, equal parts frustrating and enlightening. At times the robot gave insightful, nearly impossible-to-find advice that proved crucial to my app working. Other times it wrote entire functions and classes for me, easy for me to verify their correctness but impossible for me to have written. Other times it confidently gave wrong answers, apologized for giving wrong answers, then confidently gave the same wrong answer over and over again.

Here’s the link to the full chat: [https://chat.openai.com/share/dccd5c9a-7898-4cef-8fef-2547d0be84db](https://chat.openai.com/share/dccd5c9a-7898-4cef-8fef-2547d0be84db)

Along the way the robot helped me build out a Firebase backend for my app, start an iOS project in XCode, build my first SwiftUI views, find and import a calendar library, make an iOS icon and so much more. Time and time again I’d ask the robot how to do something that I could only describe in web development terms, or just in plain English, and I’d get back a thoughtful and accurate answer within milliseconds. This example question, where I needed to “listen” for a change in a parameter passed to a child class, perfectly encapsulates the type of “hard-to-search-for” question that ChatGPT masterfully answers for me over 200 times in the conversation:

<a href="/img/chatgpt/ss-1.png" onclick="microLite(this); return false;"><img src="/img/chatgpt/ss-1.png" width="100%" class="inline" /></a>

I felt I was truly probing the limit of ChatGPT’s intelligence only a few times. Although I got the sense that I was bumping up some kind of artificial wall; maybe the algorithm’s memory or CPU could only hold or process so much data, and my question required holding or processing more information than it was allotted for our conversation:

<a href="/img/chatgpt/ss-2.png" onclick="microLite(this); return false;"><img src="/img/chatgpt/ss-2.png" width="100%" class="inline" /></a>

<a href="/img/chatgpt/ss-3.png" onclick="microLite(this); return false;"><img src="/img/chatgpt/ss-3.png" width="100%" class="inline" /></a>

Pretty quickly I grew more attuned to the robot’s conversational style and what types of questions it excelled at answering. Eventually I found myself thinking about ChatGPT not as a programmer, nor as a search engine, but something a bit more nuanced: I was using ChatGPT as a hyper-personalized bootcamp course & instructor, teaching me exactly what I needed to know in order to implement a real-world iOS application. A six-week iOS bootcamp would have been much more cumbersome, at times no doubt feeling too abstract or too technical. On the other hand, a running conversation with ChatGPT taught me exactly what I needed to know, using a perfectly personalized, hands-on curriculum, at exactly the pace and direction I needed so I could learn how I learn best.

<div class='asterisk-spacer'> * * * </div>

People who write about chat robots like ChatGPT seem to polarize into two camps: One camp writes about it as if it’s a true technological revolution, and will make all of us rich by doing our jobs for us. Another camp seems to prefer downplaying its abilities, calling it a forgery machine, little more than a Google search bar that’s developed a few parlor tricks to sound like it can speak English.

In the realm of software & engineering, the truth is closer to the former than the latter. The robot can absolutely synthesize, organize and explain novel ideas at near-human levels, and at super-human speeds. It passes the Turing test, a concept many of my fellow software engineers have conveniently tossed aside as soon as they didn’t like the machine that passed it. ChatGPT is truly intelligent. Generative AI is, in my opinion, the most important invention since the Internet.

But for me its current usefulness seems to really shine in the area between “generalist” and “specialist”. The area where, until now, you needed to learn and memorize lots of routine, repeatable things: language syntax, best practices, usage of common tools. A human acting as a good software generalist can use ChatGPT to implement ideas and answer questions the generalist does not have time to learn, like me with iOS development. A human acting as a good software specialist can use it to implement routine functions and rote documentation that would otherwise take them too long to do themselves, like me with JavaScript development. AI robots dominating this “middle area” will indeed cost some human jobs, but I do think it will push more humans into the “generalist” or “specialist” camps as a result. Roles that I feel are naturally more fulfilling for humans, by the way.

This is not an abstract question anymore. This is real, as proved by my app on the App Store and my daily git commits for my job.

<div class='asterisk-spacer'> * * * </div>

<a href="/img/chatgpt/ss-4.png" onclick="microLite(this); return false;"><img src="/img/chatgpt/ss-4.png" width="100%" class="inline" /></a>

After about three weeks of work in my free time my first app, Basic Birthdays App, is [available for iPad and iPhone](https://apps.apple.com/us/app/basic-birthdays-app/id6450400469). I also [open-sourced all the code](https://github.com/i-a-n/basic-birthdays-app) if you want to read it, or build your own app with it.

My next apps will be a Basic Period-Tracker App and a Basic Recipes App. Although my Basic Suite of apps won’t change the world or save us from the ickiness of modern corporate bloatware-disguised-as-apps, I’m hopeful a couple of people out there will find them useful.

And, hopefully, ChatGPT will empower a few more of us novices to invent more pleasant apps, making the modern “app ecosystem” just a bit nicer. Perhaps we can take just the tiniest little slice of digital real estate back from the corporate monoliths.
