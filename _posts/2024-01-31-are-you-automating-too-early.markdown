---
layout: post
title: "Are you automating too early?"
subtitle: "Press 1 for yes, 2 for no"
date: 2024-01-31
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-bitwise.jpg"
published: true
category: Code
includeSyntax: false
includeLightbox: false
---

<span class='illuminated-letter'>I</span>joined a new gym last week. I went to the LA Fit Expo the weekend before, and this new independent gym had set up a booth and given me a free day pass. So I tried them out in person, liked it, and joined. I was what marketing people might call a "textbook conversion". The gym is so goddamn nice by the way, it's bonkers.

Anyway, they have you sign in for your day pass on a tablet in the reception area, filling out your name & address, etc, and then when you actually sign up for a membership you do it through their app on your own phone. All lovely. When I signed up on the app, it verified my email address and pre-filled my name & address and all that stuff, as it integrated with the "sign in for your day pass" system, I suppose. Makes sense. But one thing it didn't fill out was the answer to a question I had already entered on the tablet: "How did you find out about us?".

I'm sure most people wouldn't think twice, and would just fill that out again. A small percentage of people would probably think "hm, strange I have to fill this particular question out again", and move on. But a very small percentage of people are software engineers who work at big data companies, like me, unfortunately, and think "Okay, who dropped the ball here? Why didn't this data field get normalized and integrated between the two systems? Some kind of data quality issue?"

(I'm not done with this inner monologue by the way. It continues:)

_Oh, the dropdown had significantly different options than the dropdown on the tablet in reception. I guess normalization wasn't obvious so they just left it. Also, because there are so many different expos and events and ever-changing reasons, they'd need to have a standard 'picklist' somewhere that both systems referenced, and they'd obviously need to keep that list up-to-date..._

(...monologue still going...)

_Of course, those lists would need to be versioned, because if you remove an option then you'd lose all previous data for some sign-ups. Oh and maybe you should have some kind of metatagging system, since you might want to know that Event A and Event B were both specific types of events, but users might not care about that distinction, and metatagging would allow—_

I'll cut the monologue there, but it continued for quite a while. This was all happening in my head between bench press sets, by the way. After I was content with my solution for this gym's data quality issues, I looked around. The gym was brand new. There were only three people working out, myself included. The guy who gave me the tour had recognized me from the Fit Expo. Nice little gym community.

That's when it dawned on me. This was a _little_ gym community. Why did my sick corporate-tech brain feel so COMPELLED to come up with some enormous, complex, absolutely unecessary data integration & analytics system for a gym with like 25 members? Am I really that far gone?

The gym does not need a bespoke Salesforce + Mulesoft + Elasticsearch tech stack (starting price $250k a year). It barely even needs to integrate its day pass system with its membership sign up app. It only pre-filled your name and address in the app _as a convenience_. As a fucking convenience to the user! Imagine that!

Systems to automate data used for business intelligence, or sales & marketing analytics, or web/app traffic or ANY of that stuff are only done at corporate scale for the convenience of corporate executives. THEY’RE the ones who want that data stamped and delivered in perfect little JSON bundles because that helps them decide where to allocate resources (and when to fire people, of course) to make themselves more money. That‘s literally it. “The events department had a 3.5% YoY decrease in signups last quarter.. We need to work with Chad to realign our KPIs” is the whole reason this data would ever need to scale to this size. Look at how gross that last sentence is.

I had selected "LA Fit Expo" from the dropdown on the tablet. The guy who gave me the tour said "oh hey, you saw us at the LA Fit Expo, right?". That is, literally, all the data they could ever need to determine that the Fit Expo was why I signed up. The management team (there are probably like two managers, at most) could have a meeting this month and go around the fucking table and just ask each person how many people they met at the Fit Expo and how many of them signed up at the gym. It doesn't have to be that complicated yet! We don't need to automate ourselves to death for every tiny fucking thing!

<div class='asterisk-spacer'> * * * </div>

And this doesn't just apply to small, mom-and-pop companies (or SMBs as my sick tech brain reflexively calls them now). I work at an enormous data company and even here we automate way too much out of reflex. I'll give you an example.

We launched a customer-facing knowledge base system recently, entirely custom built from the ground-up. But one thing we couldn't help ourselves automating was the feedback mechanism. You know the annoying "was this article helpful?" question you get asked all the time? Thumbs up/thumbs down, leave a comment if you want.

We just _had_ to build this big, bulky data collection system, integrating it a million different ways, throwing the data into BigQuery and Elasticsearch and pinging a Slack channel when there was any feedback, etc, etc, etc. Just a huge undertaking. And now that it's launched guess how many likes/dislikes we get? One a month, if we're lucky. No one uses it. We didn't need to automate at this scale yet.

Do you run a small knowledge base and want to know if an article is good or not? Just check out the tickets/chats where it was sent to a customer and then read what the customer says in response. If the customer says "thanks!" and closes the chat, guess what? That article was helpful! If the customer says "this doesn't answer my question", then go read the article and see if it's poorly-written or inaccurate. Yes, this is some manual work for you, or for the person whose job it is to ensure knowledge base quality, but it's much less work than automating this huge system and getting zero helpful responses because we aren't Google, whose least-read knowledge article probably gets 300,000 views a day.

So the next time you're constructing an enormously complicated data pipeline, ask yourself: Am I doing this because it's the easiest way to get crucial data I need? Or am I doing this because I'm reflexively imagining a tech executive who looks like a suit model and can't program "Hello world!" wants a nice graph on their next PowerPoint presentation?
