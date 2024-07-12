---
layout: post
title: "Dummy Codes: My dumb little error code idea"
date: 2024-07-12
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-bitwise.jpg"
published: true
category: Code
includeSyntax: false
includeLightbox: false
---

<span class='illuminated-letter'>I</span> made up a dumb little error code idea last year to help solve a problem every web app has. The problem is this. When a user encounters an error in a complicated part of your app—let's say a part where three or four smaller parts could have failed—you don't want to blast them in the face with a huge, technical error.

```
ERROR: The fetch() call to our internal API endpoint failed at the client-level: The API returned a 501 error when trying to retrieve your user's session data from the /user/session endpoint.
```

Users hate long technical messages and don't care at all which part failed. So, usually, we go the extreme opposite direction and don't give them any data at all.

```
Oops! Something went wrong. Please try again later.
```

A nicer user experience, for sure. But that means it's entirely up to us developers to track down the error when it's reported to us. Maybe a customer support person will message me, "Hey, this user says they see _Oops! Something went wrong._ Do we know what happened?" Well, no, we have no idea. Now it's time to gather more info. Perhaps we'll need the user's email address, or the date/time they tried the thing that failed, etc, so we can look up where in the app the error occurred. Then we can track down any errors in our logs and find which line of code threw the exception, so we can see where the failure occurred. This can get messy quick, especially if the user doesn't remember when exactly they did the thing, or they misremember what they did or their own email address, etc.

But hang on. What if there's a middle ground here? _What if there's a way for the user to get a BRIEF, USEFUL error message that doesn't reveal too much about our internal systems, and when they mention it to us it'll mean something and help us troubleshoot?_

That was the idea I had. I tossed around a few ideas for how to simplify the error message (color-coded? a numbering system?), but ultimately they all relied on us keeping a separate error-code-to-real-code translator somewhere, and I didn't want that, since it would absolutely become outdated and obsolete over time.

So here was my idea. Every place in your app that could `throw` an error should `throw` an error all the way to the user. Each `throw` should send a unique, super short error message... And that error message should be self-referential. The best way to do it, I think, is like this.

If the `throw` is located in a file called: `/backend/api/routes/session/get_session.ts`, and it's the first `throw` in the file, the message should be:

```
Error BARSG-1: Something went wrong.
```

What? What the hell is `BARSG-1`? Well dear reader, it is simply the first letter of each directory in your codebase, all the way up to the file where the error was thrown. **b**ackend/**a**pi/**r**outes/**s**ession/**g**et_session = BARSG. Then add the "1" at the end because it's the first `throw` in the file. Easy.

Now the user will see `Error BARSG-1: Something went wrong.` and when they complain to someone in support, I now get a Slack message "Hey, this customer got an error BARSG-1. Do we know what happened?". Yep! We know exactly what happened! Easy to look up, doesn't require a separate error code translator, and doesn't even require a codebase search. Just navigate to the file in your codebase and there you have it.

It's also much easier to find that error in your logs/APM interface if you need to get really granular.

Anyway, this has actually been a very useful little idea since I've implemented it, and now I recommend Dummy Codes to everyone who writes web apps. If you try it out, let me know how it goes.
