---
layout: default
title:  "Pelican"
parent: Updates
nav_enabled: false
---

![](../../../images/pelican-3.webp)

## Maintaining a Scholarly Presence

Some professional outposts online:

+ [Kathleen Fitzpatrick](https://kfitz.info/)
+ [Jason Heppler](https://jasonheppler.org/)
+ [Chantal Brousseau](https://chantalbrousseau.xyz/)
+ [Tim Sherratt](https://timsherratt.au/) 
+ [Jim Clifford](https://jimclifford.ca/)
+ Kim Martin](https://www.kim-martin.ca/)

What unifies them? How are they different? What audience(s) do they serve? What constitutes effective presence?

What element do you like? What don't you like? How do they make use of an _ecosystem_ of services? (For an example of a broad ecosystem approach, look at [Dan Cohen's space(s)](https://dancohen.org/social-media/).) Here's me: [shawngraham.github.io](https://shawngraham.github.io). What works, what doesn't?

Also: Get to know [reclaimhosting.com](https://reclaimhosting.com). Aside from providing you space to mount your own website, it can also host more complex web-based software or platforms using its [cloud](https://reclaim.cloud/applications/) service. For instance, you could set up your own server using 'Docker' with Reclaim Cloud to keep all of your Zotero materials and sync across devices (outside of Zotero own system.) (You'd set up a space, then while logged into that space, you might eg run [this](https://github.com/giovannifarina/webdav_zotero).)

## On Static Sites

Someone will take us through their experience with:

+ Visconti, Amanda. ‘Building a Static Website with Jekyll and GitHub Pages’. Programming Historian, Apr. 2016. programminghistorian.org, [link](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages).

+ Visconti, Amanda, et al. ‘Running a Collaborative Research Website and Blog with Jekyll and GitHub’. Programming Historian, Nov. 2020. programminghistorian.org, [link](https://programminghistorian.org/en/lessons/collaborative-blog-with-jekyll-github).

## Building a Static Website With Pelican

There are *many* static site generators out there, all with their own pros and cons. Some of them make it easier to hook in other kinds of interactivity; others make it easier to modify the look and feel. It all really depends on your use case. 

> “Pelican” is an anagram of calepin, which means “notebook” in French.

There might seem to be a lot of steps in what follows, but trust me, this is more straight forward than many other options and once you get the hang of it it’s all pretty quick.


### Ingredients

Things you’ll need: a github account; a computer with python installed. Github: This will be for hosting and deploying the site. (There are other services out there you could use.) Python: a general purpose programming language, which the Pelican site generator is built with and which Pelican uses to transform your writing into a website.

Go sign up for a free account on Github. Under no circumstances pay for anything; I will never require you to pay for something in order to achieve the goals in this course. If in doubt, STOP and contact me.

Let’s get started!

### Needful Things

You'll need a place to put your website, a server to make your html actually a functioning website. We'll use Github Pages for now.

+ while logged into your github account, make a new repository: click on the + at the top right of your screen when looking at your list of repositories.
+ give the repository a sensible name
+ **initialize it with a readme** (this is achieved by ticking off a checkbox when you create the repo)
+ once your new repository is created, hit the cogwheel icon ‘settings’ link at top-rightish of the page. (Not the coghweel beside the word ‘about’)
+ under ‘general’ click on ‘pages’
+ under ‘build and deployment’ select ‘build from branch’
+ under ‘branch’ have it set to ‘main’. Leave alone where it says ‘/(root)’. Hit save.
+ Nothing much will appear to happen, BUT if you now click on ‘actions’ you’ll see that there’s a little progress indicator whirling around as github turns your repository into a website. When it finishes whirling around, your website will be online!
+ if your repo was: github.com/shawngraham/demo, your site would be at shawngraham.github.io/demo. Got it? Your username goes at the front, github.com changes to github.io, then /your-repo-name.

Ok. That wasn’t too bad, eh? Now for the next part. Let’s install Pelican. (Information about Pelican is at [https://getpelican.com/](https://getpelican.com/); this [blog post](https://medium.com/felipearcarolabs/getting-started-with-pelican-static-site-generator-written-in-python-36fa561072b6) is handy too).

**If you don't have python**[download it from here](https://www.python.org/downloads/). The website will detect your OS and the button will download the correct version for you.

Now: open a command prompt or terminal prompt on your machine.

We’re going to create an ‘environment’ for our work. What this means is that we’re going to make a special copy of Python that we only use when we’re using Pelican. This keeps the different lego pieces (the various python ‘packages’ that are configured to do specific things) from conflicting. We’ll call this special version of python ‘env-pelican’.

Type this:

```bash
python -m venv env-pelican
```

That says to your computer: using python and the 'venv' (-m)odule, create a basic copy of python in a folder called 'env-pelican'. 

Now, on a mac, type:

```bash
source env-pelican/bin/activate
```

on windows (don't forget the period!):

```bash
./env-pelican/Scripts/activate
```

This 'activate' command tells the computer that for the rest of the session you want it to use the version of python in the env-pelican environment you had it make. This will keep us from mucking up our lego blocks (if you only used one environment for _all_ of your python work, you'd end up with conflicts between different lego pieces! Very messy.)

### Build the framework

At the prompt, we’re now going to install the python lego pieces that constitute pelican by using this complete command:

```bash
python -m pip install “pelican[markdown]”
```
We're going to add one plugin for Pelican that turns wikilinks (these things: ```[[link to a note]]```) into regular html internal links, once we start writing content. So at the command prompt / terminal:

```bash
pip install minchin.pelican.plugins.wikilinks
```

And we should add this too:

```bash
pip install minchin.pelican.plugins.nojekyll
```
This last plugin adds a bit of information to our eventual site that tells Github _not_ to run our website through _its_ jekyll generator. It's not a big deal if we didn't have this plugin, but it does make updating your website through github pages run faster.



To keep things nice and tidy, we're going to create a subfolder now on your computer where you'll stash all of this website mucking about. We’ll make a new directory where your website project (and its content) is going to live. The following three commands will make a new directory called ‘website’, will **C**hange**D**irectory into that new website (ie, all of your subsequent actions are taking place on the files within that directory), and then invoke Pelican to set up everything you need for a website:

```bash
mkdir -p website
cd website
pelican quickstart
```

You’ll now be asked some questions. The first question will be:

```Where do you want to create your new web site? [.]```

That `[.]` is its suggestion, which means, ‘right here, in this directory’. Just hit enter on that one. The next questions are self-explanatory.

When it says,

```Do you want to specify a URL prefix? e.g., `https://example.com (Y/n)```

type n

When it says,

```Do you want to generate a tasks.py/Makefile to automate generation and publishing? (Y/n)```

probably easiest right now to say: n

Now, when it’s finished, if you type `ls` (or `dir`, on pc) you’ll see that you have some new files and folders, one of which is called ‘content‘. That’s where we’re going to make some text files that Pelican will turn into a website for us!

### Make some content

You can use any text editor you want to write content; make sure every file `save as` is a text file using the `.md` file extension.

For Pelican to work, you’ll need to include the following metadata right at the top of every note, formatted like this:

```
Title: My First Article
Date: 2024-07-25 10:44
Category: getting-started
```
Pelican parses that metadata to know how to format the resulting html and so on.

Write as you want. Links to other pages depend on using the wikilink convention, eg, `[[` and `]]` around the target file name.

Have a note called 'index.md'. This will be the main page for your website. Write a few more notes, and make sure the index page links to them.

Congrats, you're writing a website! Let's see how it looks with the 'preview' command: 

(type at the terminal/command prompt):

```bash
pelican -r -l
```

(Your command prompt / terminal window will fill up with messages as the temporary server that the preview command creates reports on whether or not the website is loaded in your browser, if you've clicked on things, any errors and so on.)

Now go to [http://localhost:8000/](http://localhost:8000/) in your browser and you’ll see your website! If you make changes in your text files, these _should_ automatically update in the preview, as I recall.

Hit `ctrl+c` in your terminal/command prompt to turn off the preview and return control of the prompt to you (your website will continue to be displayed in your browser, but links/refresh will return an error).

To generate your website, all of the html and all of the supporting bits and pieces, type

```bash
pelican
```

and in a moment, you’ll have a complete static website sitting in your `output` folder.

### Put it online!

The last step is to take all of the files/subfolders in your output folder and drop them into your repository on github. We'll need to configure the settings/gh-pages portion of your repository so that Github knows to serve the files as a website. We'll do this part together. Then:

+ Make sure you’re logged into github and have your repository open. Click the plus button beside the green code button.
+ Select ‘upload files’.
+ Drag all of the files and folders in ‘output’ onto the file upload panel.
+ hit the green ‘commit’ button at the bottom of the page.

Once it’s finished processing the files, Github will automatically begin the process of updating the github.io version; you can keep an eye on the process by clicking on the ‘actions’ button. Once it’s finished, you can navigate to your site – you might need to hit the ‘reload’ button if it’s already open in your browser – and voilà! You have a lovely shiny static website, and you’re using Obsidian to handle the writing of the content.

**Remember** - if your repository is at ```https://github.com/your-user-name/your-repository``` the **live** site will be at ```https://your-user-name.github.io/your-repository```. You can always click on the 'actions' link in your github repository page to see if the site has finished updating.

#### Themes

If you want to modify the theme used to generate your site, you can open the `pelicanconf.py` file in your website folder using a text editor, and change the line that looks like this:

```python
THEME = ''
```
to one of the default themes, eg:

``` python
THEME = "notmyidea"
```

Then save that file, and rerun the pelican preview or the main pelican command.

There are a lot of themes available, see [https://pelicanthemes.com/](https://pelicanthemes.com/)

For exact instructions on installing these themes, see [https://github.com/getpelican/pelican-themes](https://pelicanthemes.com/). Basically, you either clone or download that repo, then change the `THEME` setting in your pelicanconf.py to point to the exact file you want. Eg:

```THEME = '/Users/shawngraham/pelican-themes/pelican-twitchy'```

(I download the pelican-themes repo as a zip file, unzipped it in my /shawngraham/ folder.)

If you really want to get wild, there are [other plugins to extend pelican](https://github.com/orgs/pelican-plugins/repositories) with things like search, footnotes, better image handling etc. Installing and configuring these can be a bit tricky, but if you go this way, just take your time.

### Profit!

Take a moment to consider all of the _new_ things that you've just done. You have:

1) configured a github repository to both store your work _and_ serve it as a website

2) installed python

3) made a python environment for a specific task

4) installed modules into that environment to generate a static website from basic text files

5) used note-taking software as an authoring environment

6) generated a working website, previewed it

7) pushed the resulting files online for the world to see.

Not too shabby, as Adam Sandler once said.