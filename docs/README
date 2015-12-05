This is the union.io Jekyll site. Hi.

Here's the structure:
---
public_html/
| - _site/                          // Destination for compiled site. Don't touch.
| - css/                            // Destination for compiled css. Don't touch.
| - js/                             // Both compiled and ugly JS goes here
|   | - file.js                         // Ugly JS. Touch.
|   | - file.min.js                     // Grunt makes these. Don't touch.
| - less/                           // LESS/CSS. Touch.
| - _config.yml                     // Jekyll config. See Jekyll docs.
|
| - _posts/                         // Posts
|   | - 2015-01-01-title.markdown       // Post naming scheme
| - _layouts/                       // Templates
| - _includes/                      // Basic header/body/footer includes
| - file.html                       // A page. See header of existing one for syntax.


Here's how to build:
---
1. Get all the files from github.
`git clone git@github.com:i-a-n/unionjkl.git'

2. cd into it, then install and run grunt.
`npm install grunt -g; npm install; grunt watch'

3. Then serve it through Jekyll.
`jekyll serve --watch'

4. Site will live (by default) on http://0.0.0.0:4000/

Here's how to deploy:
---
I have .gitignore set to ignore a file called 'deploy.sh' in the root of the project. This would be a good place to put a deploy script. My current one simply builds the site, then uses scp to move the files onto my web server. Here's one dumb, current script:

```
#!/bin/bash

jekyll build
scp -r _site/* union.io:/var/www/vhosts/blog.union.io/site/
```
End result: I have to manually run `deploy.sh' whenever I want to deploy. Not the coolest thing but it works.
