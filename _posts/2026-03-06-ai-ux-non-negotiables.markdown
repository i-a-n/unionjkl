---
layout: post
title: "Building an AI assistant? Here are my top four non-negotiable UX principles you should follow."
date: 2026-03-06
header-img: "img/post-bg-bitwise.jpg"
thumbnail-img: "img/post-thumb-bitwise.jpg"
published: true
category: Code
includeSyntax: false
includeLightbox: false
---

<span class='illuminated-letter'>L</span>ike almost everyone in my field of software engineering, I've seen my company, team and projects pivot toward developing AI-powered products in the past year-and-a-half or so. Everyone’s doing it. I want to set aside my personal feelings on whether this is a good thing generally, since that's such a big and messy question of which I only have fair-to-middlin' expertise, and instead focus on something I have much more experience in: Ensuring AI assistants’ user experiences aren’t terrible.

I wrote about making my own proto-LLM [way back in 2016](https://blog.union.io/thoughts/2016/11/30/finnegans-wake/), then about the first major LLM coding agent [in 2021](https://blog.union.io/code/2021/07/14/code-robot/), and then about interviewing software engineers who use AI coding agents [last year](https://blog.union.io/code/2025/02/18/interviewing-in-the-age-of-ai/), so I know a thing or two about the evolution of AI in the software space. I also designed and led development of an LLM-powered chatbot for Elastic’s support portal, which recently won an industry award for [best use of AI for customer support](https://www.elastic.co/blog/elastic-wins-2025-best-use-of-ai-for-assisted-support). And in that time, I’ve seen and purposefully declined tons of annoying UX patterns that are being used by the industry at large.

Here are my top four non-negotiables for ensuring you don’t wreck your users’ experiences with an LLM-powered chatbot.

## 1. Never make a user wait for a response if they didn’t ask for a response.

A single unwanted interaction can ruin a user’s entire perception of a product, and by extension, of a company; for many users, AI is intrinsically an unwanted, useless burden that does nothing except steal data and autocomplete sentences. **Those users must be allowed to “turn off” AI where practical, and should absolutely never be made to wait for an AI response before ignoring it.**

Making them participate in an AI conversation against their will is not viable, nor respectful, nor a way to convince anyone your tool will help them in the future. Always ensure a user purposefully engages with your chatbot before showing a loading or streaming element that cannot be skipped quickly.

## 2. Don’t splinter the experience. Talking to an AI bot should only happen through one single UI element.

Often the path of least resistence, when adding a new feature, will be to simply “throw a text box in there somewhere and let them start a conversation about it”. This is the easiest thing for us as developers and maintainers of an AI system to talk about, reason about, etc. It’s clear to us this is just another window into our existing AI toolset. However, this is not clear to a passive, disengaged user. It is not easy for them to reason about who they are conversing with, and what “shape” our AI assistant is taking, if there are multiple unrelated interfaces for talking with it.

**There should only be one UI element for conversing with a given AI assistant.** If you need an additional interface, or additional space, that single element should animate into that other space. Need a “fullscreen” experience? Animate in and out from the existing chat interface. Need a flyout? Same thing. Product teams will find this is a very easy rule to bend and break. It will be much more difficult to keep saying “no” to new chat inputs. But I feel it’s absolutely vital to the brand, voice and the tone of a strong AI assistant to maintain its singular shape.

## 3. Reserve the “text message interface” for conversational dialogue. Not every AI-powered interaction is a chat.

AI can be used for a million things, but not every thing it does belongs in a back-and-forth, text message-style interface. Displaying search results without accepting conversational feedback from a user? No need to have a chat interface; just use a search results page. Using AI to generate a block of text to be submitted? Stream the results into the existing form fields; refinement can be done inline, or with future edits overwriting in place.

Are users _actually_ talking to your LLM-powered assistant with a cute name behind the scenes? Maybe. Does the user need to know that? No!

It will often be the easier path to just throw the next new feature into the existing chat window. But, like the previous consideration, product teams must keep a holistic view of their product in the forefront, and make the decision to maintain a strong, thematic voice & tone for an AI assistant, even if that’s more difficult sometimes.

## 4. When someone opts-out, you must opt them out immediately and, more or less, forever.

**Similar to the first consideration, if a user declines to interact with an AI assistant, you should assume that declination is permanent.** Or at least, permanent within a very long time range. When a user declines to initiate a conversation, say, when attempting to open a support ticket, that decision should be respected when the next ticket is opened as well. Users are not goldfish: They will remember that they can converse with an AI assistant, even if they declined the first time.

As AI grows and is integrated into more support experiences, I think it’s vital to maintain a discrete, well-structured product, and to always be cautious and err on the side of passivity with regards to users’ time and attention.

In conclusion: **Keep your chatbot out of the way**, **respect your anti-AI users**, and, even when it’s the more difficult decision, **protect your product’s brand integrity**, even when your boss’s boss wants AI in every single textarea.
