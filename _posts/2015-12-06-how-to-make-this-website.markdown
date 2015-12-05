---
layout:     post
title:      "How to Make This Website"
subtitle:   "The blog you're looking at was a labor of love. Here's how I made it."
date:       2015-12-16 12:00:00
header-img: "img/post-bg-make-this-website-1.jpg"
published:  true
category:   Code
readtime:   "25 minutes"
---

<p><span class='illuminated-letter'>E</span>very so often it happens that a web developer wakes up one afternoon and decides, against everyone's best judgment, they need a personal website. It could be for professional reasons, or personal ones, or just to try out a new platform. Whatever the case, the web developer will then promptly put off starting the project for a minimum of three months.</p>

<p>After those three months pass, the developer will finally &ldquo;find the time&rdquo; (an enormous lie; they had wasted hundreds of hours doing other things), and get started on The Personal Site That Will Change the World. The problem is, a web developer freelancing for herself in her spare time is like a chef who works sixty hours a week cooking for herself at 2:00am. Sure, she's got the freedom to cook anything she wants, but &ldquo;I make food all day and all I want to do is boil this $0.49 cup of noodles and attempt to inhale it while I sleep&rdquo; always wins out. It's a curious fact most high-stress chefs just eat the easiest food after a shift. Most web developers, when faced with a personal web project, just develop the easiest website.</p>

<p>I found myself in this situation last week. I needed a personal site for various reasons and, since I work full-time as a web developer, I just wanted to inhale some Ramen noodles and go to sleep. I didn't want to deal with databases, WordPress, build servers, any of that. And, as the site took shape, it occurred to me the steps and patterns I used could be of interest to other web developers. Newer coders are easily scared off by complicated-sounding systems and, even if they understand 35 of the 36 steps needed to build a site, all it takes is one incomprehensible direction to sink their project.</p>

<p>So, here, I'm going to outline every single step I took to make and update this blog. I'll use only the simplest concepts and explanations. I want this to be thorough enough for my friends who are interested in front-end coding to be able to follow every step and, hopefully, decide whether this is a career they'd be interested in pursuing.</p>

<p>That, and if I ever make another blog like this, I'll be really happy I wrote it all down.</p>

<h2 class="section-heading">The Requirements</h2>
<p>I don't want to deal with a database-driven CMS, like WordPress or Drupal. Yeah, they're powerful. Yeah, the setup is easy. And if I were a team of people updating my site every day, I'd probably go with one of those. But I'm interested in a &ldquo;set it and forget it&rdquo; option. I don't want to have to ensure a MySQL database server is running 24/7 forever, and have to remember how to troubleshoot it if my site starts returning a mysterious error. I want a flat-file site, where everything from posts to categories are all <i>just files on a filesystem</i>. If all you're doing is making files, you can them host anywhere, and the site's going to be faster and less prone to failure.</p>

<p>I also don't want to pay for it. Sorry, but I don't. There were some sexy-looking options out there, like <a href="http://statamic.com/" target="blank">Statamic</a> and <a href="http://getkirby.com/" target="blank">Kirby</a>, but I want something that's entirely self-contained and could be copied, edited, repeated, and hosted anywhere. Paid options aren't great for that. And also it's tough to justify paying for something that, realistically, could just be a few .txt files.</p>

<p>After weighing my options, which included <a href="http://monstra.org/" target="blank">Monstra</a>, <a href="http://getgrav.org/" target="blank">Grav</a>, and more, I settled on <a href="https://jekyllrb.com/" target="blank">Jekyll</a>. It appealed to me most because of a fairly rich feature set and, crucially, the concept behind it boiled down to this: <i>Just make a bunch of files, put a few variables at the top, and our script will take all of that & give you a single folder that will contain your entire, completed website.</i> This is basically the developer equivalent of <i>just boil a cup of noodles, you lazy useless sloth</i>. Perfect.</p>

<h2 class="section-heading">The Tools Needed</h2>
<p>Jekyll is for developers. It's not a button to click or a download-and-open it application. You have to spend some real time learning how to use the tools needed to run it. This is exactly what being a front-end developer means. Most outsiders think software engineering is all math, or hacking, or both. It isn't. What it boils down to is taking the time and patience to figure out a pattern or a concept or tool you can then reuse. It may take you minutes, it may take you weeks, but once you've learned it you've got it forever. And once you've mastered a few basic concepts and patterns, you're suddenly a front-end developer who makes more money than your high school principal. So learn these tools:</p>

<h4>1. Git & Github</h4>
<p>These are the bread and butter of modern coding. You can read about git's history <a href="https://en.wikipedia.org/wiki/Git_(software)" target="blank">on Wikipedia</a>, but it can probably be described best in one sentence: It keeps track of all of your files, logs your changes to them, and then stores them on a server so any number of people can work on them without stepping on each others' toes. This also means you can "revert" changes to any point in its history, see who wrote which lines of code, and much more. It's also free. Learning the basics takes an afternoon and mastering the advanced stuff is something you'll probably never need to do. There are a million great tutorials for learning git, like <a href="https://www.liquidlight.co.uk/blog/article/git-for-beginners-an-overview-and-basic-workflow/" target="blank">this one</a> and similar. Go nuts.</p>

<p><a href="http://github.com" target="blank">GitHub</a> is just a place to store the files you're managing with git. That's it. It's also free for personal use. It provides great interfaces and tools for seeing your files and history and why they give away all that great stuff for free I'll never know. Once you have the basics of git down, you'll understand GitHub. Get an account today, right now. There's no reason not to.</p>

<p>I decided to keep all of the code for this website <a href="https://github.com/i-a-n/unionjkl">on my github account</a>. This will allow me to pull the code onto any server I want, and also keeps a complete version history of every change I'll ever make. So that's where my code will officially live.</p>

<h4>2. Any code editor</h4>
<p>This one's easy. If you want to write code, you need to find a code editor you love. There are a bunch of free options and you can use anything from VIM (if you like command-line) to TextMate (if you don't) to <a href="http://www.sublimetext.com/">Sublime</a> (if you want the best of both worlds). I prefer <a href="https://atom.io/">Atom</a>, which is a bit more technical but still easy enough to use. Just download one and get to touchin' files.</p>

<h4>3. Basic UNIX command-line</h4>
<p>Running web things generally requires basic command-line knowledge. If you're on a Mac or Linux box, just open up a terminal (in OS X, it's the "Terminal" app) and start messing around. Google anything you don't know how to do. You'll be using these terminal commands to actually run Jekyll, commit to your git repository, and publish your site to a server. You can get the basics down in a few hours and then spend a lifetime learning to be mediocre at command line. It's tough and the nerds who master it are mythical Linux titans who basically run the world (but can't wear matching socks).</p>

<h4>4. The basics of web hosting</h4>
<p>The concepts behind basic web hosting used to be a mystery reserved only for "sysadmins" and "webmasters". They could charge unknowing clients thousands of dollars a month for what amounted to a Dell laptop hooked up to a DSL line in Romania. Nowadays that doesn't fly, as solid, expandable webhosting is cheap and easy to understand. Learning how a basic web server works, how to connect and set up a website, varies from host to host. I'd personally recommend a place like <a href="https://www.digitalocean.com/" target="blank">Digital Ocean</a> who, for only a few bucks a month, keep a little slice of the internet at your disposal, 24/7 for whenever you need it. But, any good host with lots of online support will work. I'm hosting this site, currently, on a <a href="https://mediatemple.net/webhosting/vps/developer/" target="blank">Media Temple VPS</a>.</p>

<h4>5. StackOverflow</h4>
<p>When I'm hiring a front-end developer, I always ask one question: &ldquo;If you don't know how to write something, how do you learn how?&rdquo;. The candidates that answer &ldquo;Probably Googling it and looking for the <a href="http://stackoverflow.com" target="blank">StackOverflow</a> thread&rdquo; usually end up getting the job. It's arguably the web developers' number one tool. Learn to love it, you'll be searching it daily.</p>

<h2 class="section-heading">The Setup</h2>
<p>Armed with these tools, I was ready to make this site happen. Little spoiler here: I've made a thousand websites in my life. I'm well-acquainted with every tool and framework I needed. This site is stupid-simple to make and maintain. But, even considering all that, developing this site took me days. And hours of abject frustration. If this strikes you as awful, illogical, or undesirable in any way, turn back now. Web development isn't for you. For those of you still with me, here's what I did.</p>

<img src="http://union.io/images/repo/20151205-00--3bbf38.jpg" class="full" alt="wireframe. very advanced.">
<span class="caption text-muted">My very, very advanced wireframe concept.</span>

<p>First things first: Draw out what you want the site to look like. Pictured above is my very advanced wireframe concept. I drew it on a post-it note in five seconds. But, strangely enough, it was pretty useful. Armed with that, I started looking for <a href="https://github.com/jekyll/jekyll/wiki/Themes" target="blank">open source Jekyll themes</a> that might be easy to customize into my post-it note idea. I found one called <a href="https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll" target="blank">Clean Blog</a> which, you guessed it, is a clean-looking blog theme. Looked good, and included all the basic Jekyll files and structure already, so that was a pretty easy choice.</p>

<p>I created a new repository on my GitHub account, downloaded and copied over the files from the Clean Blog theme, and <a href="https://github.com/i-a-n/unionjkl/tree/018bdb0e99812bc8867fd77b5a4dae52e7652d5f" target="blank">made my first commit</a>. It was as easy as using Terminal to run a few git commands. If you are unsure how to do this, just Google it. These are well-trodden paths. Any error you run into, Google that too. This is the Creed of Everyone Who Works on Internet Things.</p>

<img src="http://union.io/images/repo/20151205-01--614e4b.png" class="full" alt="Hyper-detailed instructions">
<span class="caption text-muted">Hyper-detailed instructions to self.</span>

<p>Using this Creed, I distilled everything I needed to do to run Jekyll&mdash;and create an actual website folder&mdash;down into the four steps shown above. Then I saved those instructions to my git repo, so I'll never lose or forget them. Running those commands in Terminal will now make a website, and host it so only you can visit it. You should be able to see some light at the end of the tunnel now: With only minor configuration tweaks, <i>I basically already have a functional website</i>, and if I run it on a public web server I'll have a working, functional blog instantly. Not bad!</p>

<h2 class="section-heading">The Customization</h2>
<p>So now I had something safe, simple, and repeatable. But it basically looked like the default "Clean Blog" theme, and I wanted something highly customized. This is the more creative part of the process; I love front-end development precisely because it's a marriage of both creative and logical thinking. Choosing the fonts (I chose <a href="https://www.google.com/fonts/specimen/Lora" target="blank">Lora</a> and <a href="https://www.google.com/fonts/specimen/Montserrat" target="blank">Montserrat</a>), colors, sizes, and icons are enormously fun. You can customize any site infinitely by editing the CSS and tweaking the layouts (Google how to do those in a Jekyll layout). Front-end people love this part but all-too-rarely get to do it. After a few hours too many of playing with variables, I was happy with the general look at feel.</p>

<p>(I should note, since I used git, you can simply <a href="https://github.com/i-a-n/unionjkl/commits/master" target="blank">rewind my GitHub repository</a> to see the changes I made, when I made them, and my dumb comments with each commit. This probably isn't too interesting, but it does function as a complete development history for the entire project, should you care to see it.)</p>

<img src="http://union.io/images/repo/20151205-02--8ec3be.png" class="full" alt="Jekyll front-matter">
<span class="caption text-muted">Standard Jekyll post variables.</span>

Another step I took was customizing the Jekyll post variables. Posts in Jekyll are just text files with a bunch of post information at the top of them. The default variables, pictured above, didn't quite have everything I wanted. Jekyll lets you add any variable at all to the top of the post, and then access that variable in the layout by referencing 'page.variablename'. So, for instance, I wanted an &ldquo;estimated reading time&rdquo; variable with each post. I just added a "readtime" variable like so:

<img src="http://union.io/images/repo/20151205-03--57694c.png" class="full" alt="Jekyll front-matter">

<p>Then added it to the template, like this:</p>

<img src="http://union.io/images/repo/20151205-04--ec3432.png" class="full" alt="Jekyll front-matter">

<p>You'll need to Google the syntax and specifics for the templating language. Remember the Creed. After some trial and error I finally got that stupid Estimated Reading Time to work. <i>It's learning how to do dumb stuff like this, dozens of times a day, that makes developers so valuable</i>.</p>

<h2 class="section-heading">The Deploy</h2>
<p>So now I had a customized blog, with a few silly posts, loading locally on my laptop. Showing it to the world takes some big decisions. GitHub does offer Jekyll hosting for free, but I want to eventually do some complicated things outside of the blog, so I decided to self-host. I had two major options for deploying:</p>

<h3>First option: Deploy a script on the server to listen for changes to the GitHub repo, pull them in, and automatically rebuild the site</h3>
<p>Whoa there Einstein, slow down! This one appealed heavily to the nerd in me. The concept is basically this. When I commit a change (new post, new image, anything) to my GitHub repository, a script on my public server would spring into action, pulling in the new change and then using Jekyll to rebuild the site instantly. Very little overhead, very efficient. Also, in the event I need to load-balance or deploy to many servers, each one would update itself instantly. Awesome.</p>
<h3>Second option: Write a local script to build the site, then copy the finished files directly to the server</h3>
<p>This one is so boring. Running a script manually? What am I, a caveman? Instead of just committing a change and being done with it, I'd then have to run a command that does the actual update to the server. This one did not seem sexy and I wanted to avoid it.</p>

<h3>I went with the second one.</h3>

<p>Yes, it's true. I tried a few server-side auto-deploys first, but just couldn't make any of them bulletproof. I did get them working but it introduced, literally, a dozen new and interesting ways to fail. I'd also have to track new GitHub keys, and give new servers access to my personal GitHub account. I'd have to maintain identical Jekyll versions on my laptops and web servers. I'd have to ensure there were no problems with <i>every single commit</i>, since even a change that didn't impact my site (like documentation) would spawn a new rebuild on the server.</p>

<p>In the end, I wrote a script I called "deploy.sh". It is two lines of code. When I want to update my site, I just run "./deploy.sh" and my site is updated to the latest version I'm working on. It's less appealing, but it's basically bulletproof. I documented the entire process <a href="https://github.com/i-a-n/unionjkl/tree/73490715273756bf6e921a37fe3306b5f8d97cbb/docs" target="blank">here</a>. Feel free to copy.</p>

<p>You can use the 'scp' or 'rsync' commands to do this, as long as the server you're pushing to is configured to accept your SSH keys, that way you can connect to it without a password. The best tutorial on how to set up SSH keys is <a href="https://mediatemple.net/community/products/dv/204644740/using-ssh-keys-on-your-server" target="blank">here</a>.</p>

<h2>The Conclusion</h2>

<p>After much tweaking, I now had a script that compiled my site using Jekyll, and pushed the whole thing anywhere I wanted. All I had left to do was ensure the whole site was pushed to a logical place on my server (I used the file path /var/www/vhosts/blog.union.io/), point my web server to that location when it got a request for "blog.union.io" (Google how to do that for your specific hosting setup), and then tell the Internet to send requests for "blog.union.io" to that server's IP address. You'll do that part at your domain registrar or DNS host, which can be anywhere (I recommend <a href="http://google.com/domains" target="blank">Google Domains</a>).</p>

<p>And finally, I followed a few tutorials on <a href="http://www.chrisanthropic.com/blog/2014/jekyll-themed-category-pages-without-plugins/" target="blank">how to make category pages</a> and <a href="http://davidensinger.com/2013/04/adding-open-graph-tags-to-jekyll/" target="blank">how to add Facebook data</a> to each post. These each had their frustrating moments but in the end, anyone can get through them with enough time. And when that was done, I had that moment. The moment you realize you created something with real value, that fills a real need. Visitors to my site&mdash;few and fleeting, sure&mdash;don't see the frustration that went into it, or the flaws and frailties I can't stop focusing on. Learning to accept that you just made something of professional caliber is the final boss of software development.</p>

<p>So sit back and have a whisky. Or two. You'll need it, because as a web developer, you're going to repeat some variation of the above process eight times a month until you retire.</p>

<p>And I love it.</p>
