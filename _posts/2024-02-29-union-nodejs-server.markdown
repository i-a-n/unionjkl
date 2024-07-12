---
layout: post
title: "Did the world need another web server? No. Did I? Yes."
subtitle: "Introducing union 1.0, a NodeJS-powered multi-domain web server"
date: 2024-02-29
header-img: "img/post-bg-svgs-react-1.jpg"
thumbnail-img: "img/post-thumb-bitwise.jpg"
published: true
category: Code
includeSyntax: false
includeLightbox: true
---

<span class='illuminated-letter'>W</span>hen I first started making web apps—way back when they were called “websites”, which consisted of these ancient things called “web pages”, which were files made by people called “web masters” (yeesh)—there was more or less a standard way to serve them. You rented a little space at a hosting provider, and then either they, or you, would run something called [Apache](https://en.wikipedia.org/wiki/Apache_HTTP_Server). That was the web server. Back then, and this was 20+ years ago, Apache was already an ancient beast, having been the first mega-popular web server software. It was as close to “standard” as you could get.

It is now the year of our lord 2024 AD and, amazingly, Apache is still fairly standard today, although it shares its market dominance with a relative newcomer to the scene, nginx (“““only””” 20 years old now). Somewhat surprisingly, they both share very similar overall user experiences, conceptual architectures and distribution/installation methods. Most hosted web apps can switch between the two with very little effort. How has something as fast-moving and ever-changing as web development clung to the same software pattern for so long?

Well, part of it is that Apache is very good at what it does. It starts up when the server does, it runs as root to open the standard ports and load your secret SSL files, it re-spawns processes when they crash, it has been through a hundred billion trials-by-fire every day... It’s good software.

On the other hand, it’s a pain in the fucking ass to install and configure this monster when all you want to do is serve a couple of blogs and a React app for your friend’s art gallery or whatever.

Why do I have to write all of these boilerplate config files in some far-off `/etc/` directory, the location and name of which I have to look up every time and—I think?—use `sudo`? Why do I have to look up all of these exotic Apache-specific directives to shove in there? Have you seen the Apache config file, by the way? The default one? [It’s literally 500+ lines long](https://gist.github.com/TheSunMan/4008088). What in the fuck. I don’t want to do this. I just want to serve my modern web things in a modern way.

## Meet the Modern™ web server

Modern web app development is mostly done in NodeJS these days, which ships with its own way to create an HTTP server with one line of code. The standard web server for developing NodeJS apps is called Express, which can be installed by—gasp!—a non-root user and then run by simply `require()`-ing and `.listen()`-ing with it in a JavaScript file. Developers discovering this radically simple server felt something like taking a big gulp of fresh air after being submerged in a swimming pool for about five seconds longer than you should have been. _Where has this been all my life?_

But people don’t use Express for serving “real” websites. There are a couple of reasons for that.

### 1. Low port numbers are off-limits

I think the number one reason we don’t use NodeJS servers to serve real domains is that unix-like operating systems don’t let regular users open processes that listen on ports 80 or 443—the default ports your browser connects to when going to a website. That’s because ports lower than 1024 are reserved for root only. Why? I have no fucking idea! If your system has a compromised user who is running arbitrary processes, does it actually matter if they listen on port 80 or 8080? Maybe it matters a tiny bit, but I don’t think it matters that much. It’s already a critical breach! In fact, if a malicoius user runs something on port 80, at least you’ll notice your web server is fucked and you’ll be able to shut it down faster. For me, personally, I absolutely do not give a shit if my own user—the only user I created on my machine!—can open a port with a number lower than 1024. But alas, this bit of security threater ensures most NodeJS-powered servers can only be used during development.

### 2. Multi-domain hosting sucks

Configuring Express to serve multiple domains is complicated. Well, not really complicated, but definitely not supported out-of-the-box. Throw in the problem of individual SSL certificates for each domain, and, well, you might as well be configuring Apache. Shitty!

### 3. Perceived immaturity

As the old saying goes, no one ever got fired for picking Apache. It’s safe to pick Apache. Is a NodeJS server ready for primetime? Is it safe? “It doesn’t even run on port 80 by default!” “It can’t load balance or serve 10,000 connections at once or serve NSA top-secret documents!” “It must be a novelty.” Even developers who are running small, mom-n-pop-style servers get dissuaded from picking NodeJS servers because they imagine they will need to do all of these super-advanced, super-mature things that only Apache can do. The truth is, they usually don’t need to do that stuff. And as a point of fact, most of NodeJS servers’ perceived immaturity is just that: perceived. Lots of developers who call NodeJS servers immature are actually fine running NodeJS servers behind an Apache proxy! Guess it’s not _that_ immature, huh?

## A union of the old and new

The standard way to bridge the gap between old and new server architectures is typically to [run both of them at the same time](https://blog.logrocket.com/how-to-run-a-node-js-server-with-nginx/). Yep, wish I were joking. The standard way is to just run Apache/nginx like normal, then proxy each request to your own NodeJS server running on some higher port number on your same machine. This is stable and it works, but is extreme overkill for what a lot of developers need. I just want to serve a few static sites and React apps on my $5 server! I don’t want to have to install, run and maintain all of this shit!!

So I invented [union](https://github.com/i-a-n/union), a NodeJS web server designed to just serve multiple domains on normal web ports, with SSL support baked in. It runs itself as a daemon in the background, so it’ll restart itself if it crashes. In direct contrast to Apache, it is absurdly quick to install and configure and run:

1. `npm init`
2. `npm install @union.io/union`
3. `npx union`

That’s literally it. Run those three commands wherever your domain folders are located (`/var/www/vhosts`, for instance) and you’ll have yourself a web server. It reads your folders that look like domain names and serves each of them automatically. I also included instructions with common commands to open up low web ports to normal users, read SSL certificates without root, and start the server up automatically when your machine boots/reboots. Stuff to make your plain NodeJS server act like a real server!

And how do I know it works? You’re reading this post on a union server right now. Beep boop.

## The future

I started this project just because I needed it for my own stuff. Maybe some other people will find it useful, maybe not, that’s fine. But if it does start getting used, it’ll need some work in a few areas to be a truly viable Apache/nginx replacement for a critical mass of projects:

- Load balancing and multi-threading
- Windows and other OS support
- Expanded SSL support (including instructions for non-Letsencrypt workflows)

So there’s plenty of room for improvement. But if you find yourself needing to serve multiple basic domains in a standard, NodeJS-friendly way, [give union a try](https://www.npmjs.com/package/@union.io/union) and let me know how you like it.
