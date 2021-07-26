---
layout:          post
title:           "Is Your App a House of Cards, or Is It Stable? Both, Probably."
date:            2021-07-26 12:00:00
header-img:     "img/post-bg-cards-1.jpg"
thumbnail-img:  "img/post-thumb-cards.jpg"
published:       true
category:        Code
readtime:        "8 minutes"
includeSyntax:   false
includeLightbox: false
---

<span class='illuminated-letter'>I</span>’ve found, generally, that the first established app you work on when you start writing code will come to represent, in your head, an almost mythical level of complexity, advanced architecture and, above all, stability that you’ll forever feel is unattainable within your own apps. That very first big project you’re allowed to contribute to in a small way? “Wow, I can’t believe they let me touch this! It’s so big and important, it’s engineered The Right Way by a bunch of Senior Geniuses, I could never write something like this!”

That app for me was a monstrous, custom management system called “HostOps”, which ran the entirety of the backend operations at Media Temple, my first software company. It was millions of lines of code, patched together PHP and Perl mostly, using CPAN for modules and SVN for version control. It was accessed by every member of every team, and had to be up 24/7/365. When I was allowed to submit my first line of code to it, it was already at least ten years old, with parts of it much, much older.

To me, HostOps was unassailable. It was the Mother of All Apps. A few of its creators were still at the company, and to me they were titans of code. To make it even more intimidating, I was hired originally as a support engineer who had to login to HostOps every day... So to be handed a small key to this kingdom when I moved into software development? Almost unimaginable.

Think about the most recent app you built or helped build from the ground up. Maybe a `create-react-app`, or even a server you’ve stood up with Apache running on it. Anything that has to be up and functional 24/7. How do you feel about it?

If you’re anything like me, you feel like it’s a bunch of popsicle sticks held together with a combination of Scotch tape, melted marshmallows and luck. You could imagine about a hundred different ways it could fall down and expose how the combination of a modern software ecosystem plus your own professional shortcomings equals the unstable house of cards you knew it was all along. Your app is no HostOps. It could never be so stable.

<div class='asterisk-spacer'> * * * </div>

But I want to tell you a bit more about HostOps. Things I learned about it as I peeked behind the curtain for the next five-plus years.

After getting settled into the HostOps codebase, I slowly got introduced to the core of the recurring billing system, which was written in C and named BillMax. I wondered why it was named that, and had its own logo, since all of the code was ours (or at least, lived in our package system). After some investigating, I found that BillMax was at one time a vendor of ours, and we had grown so large that we simply purchased their source code, and all the rights to it. But at the time they couldn’t agree on the best way to send and store a copy of the code securely, so BillMax just sent us a CD-ROM with the source code on it. We took this CD, and, inexplicably, decided to just buy a safe to store it in. Yes, a physical safe. I saw the safe with my own eyes. However, there was one bigger problem: “Uh.. yeah.. during an office move.. someone lost the key”, I was told. I wish I were making this up, dear reader. But sadly, I am not.

But I still thought HostOps was engineered The Right Way, of course.

On a lunch break one day I ran into one of the Senior Geniuses who helped build HostOps, and he mentioned a security issue that had just been raised. The issue was that one of our support engineers (the same job I used to do) had just found out he could log into HostOps by only typing in the first half of his password. After the first few characters, he could type in random junk and it would still log him in. “Oh yeah,” the Genius told me, “I was afraid someone would rediscover that. When we built it, we had to trim the password input down for some reason or another, so every password is only the first six characters of what employees think their password is.” My jaw dropped. “We were supposed to fix that later, but never got around to it.”

But even after learning all this about HostOps, it was still, in my mind, a Very Real And Stable App.

Sometime later, as my time at Media Temple was winding down, the guys at the data center were finishing up a very large cleanup task, simplifying the network topology and doing physical hardware and network upgrades where necessary. A question came back from one of them in a company chat channel: “Does anyone know why there’s tape on the back of VZ332?” After a bit, we determined that VZ332 (or whatever he said) was the HostOps server. That jogged someone’s memory. “Oh, yeah. Years and years ago the main CAT-5 cable’s little plastic thing snapped off, and we just had to Scotch tape the cable into the port since HostOps couldn’t go down while we were finding a new cable. Guess we forgot to fix it?”

That’s right. HostOps—the cannot-go-down, paragon of stability upon which the entire company depended—was literally held together by Scotch tape. And I mean that in the most literal sense.

<div class='asterisk-spacer'> * * * </div>

It occurs to me now, at this more senior stage in my career, that I’ve helped develop multiple HostOps. Scores of junior devs, at companies I’ve long ago left, may have come to think of me as A Guy Who Wrote That One Stable App That Keeps Us All Going. But I’ve rarely _felt_ like that’s true, even though I see now that it is. I felt that way, I now realize, because it turns out _all_ software is rickety and unstable. All software grows obsolete, convoluted and messy over time. This is, and I cannot stress this enough, unavoidable.

HostOps was never stable, nor well-engineered. I only thought it was because I used it every day for years without seeing the code or knowing its history. And all software is like that. A house of cards to its creators, a Real App to its users and junior devs. Just as crucial as being able to recognize and work through imposter syndrome, I think, is the ability to recognize and work through the fact your app is real, valuable and stable, despite your knowing where all the scary monsters may lurk.

One last thought: For all of HostOps’ faults, it’s still functioning today (I’m told). It was the nerve center of Media Temple from the company’s inception to its eventual $100 million sale to GoDaddy. It made all of that possible. It was, in the end, real software.

And it was really held together by Scotch tape.
