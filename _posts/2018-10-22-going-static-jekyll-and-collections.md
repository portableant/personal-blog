---
id: 466
title: 'Going static: Jekyll and collections'
date: 2018-10-22T22:04:17+01:00
author: Daniel Pett
layout: default
guid: https://4C800C11-27ED-46F9-9CE3-5E8385B26762
permalink: /going-static-jekyll-and-collections/
wtr-disable-reading-progress:
  - ""
wtr-disable-time-commitment:
  - ""
image: /images/2018/10/Screen-Shot-2018-10-22-at-23.10.04.png
categories:
  - Techie stuff
tags:
  - jekyll
  - ruby
  - tutorial
---

<figure >
<img src="/images/2018/10/Screen-Shot-2018-10-22-at-23.10.04.png" alt="" class="img-fluid 473"  />
<figurecaption>3D instructional website screenshot</figurecaption>
</figure>

At the Fitzwilliam Museum, we have a large amount of old websites that were built over the last decade. Many of these are now presenting security risks as they are on old WordPress installations, or they are just plain hand coded HTML. To alleviate the burden for supporting these sites, I have been transferring as much as possible to [Jekyll](https://jekyllrb.com/) powered Github Pages instances (although I am also looking at [Gatsby](https://gatsbyjs.com)).

I'm attracted to Jekyll, due to the powerful conversion of very simple**markdown** files. Lightweight, easy to edit, hard to break and easy to run through version control. I'm hoping that we can use this format to stay away from heavily customising content management systems for our research sections at the Fitz. The sheer amount of sites that we have now got makes administering them all a gigantic task. Going this way, with simple text files might make it easier, or it might be a red herring.

### How to generate? Is it hard?

Generating a Jekyll site is pretty straightforward, and this post outlines how I built the [University of Cambridge Museums tutorial site](https://github.com/UniversityofCambridgeMuseums/festivalOfIdeas) for the Festival of Ideas event I ran on Photogrammetry. Having an example to build towards, makes the process easier!

**Remember though, this is a bare bones example.**

### Installing Jekyll

I am assuming in this instance, you, the reader will be on OSX and have homebrew installed, RVM and the lastest Ruby and can use terminal. If you have all of those set up, you will now need to install the Jekyll gem. So go to terminal and issue this command:

<code>gem install bundler jekyll<br /></code>

Once that has completed (if your permissions are all set correctly) you should have Jekyll ready to go.

### Generating the site skeleton

You're now ready to create the basic outline for the site. In terminal again run the following command, replacing {sitename} with the folder you want to create:

<code>jekyll new {sitename}<br /></code>

This creates a new folder with the base skeleton for a Jekyll app. Change directory to this:

<code><kbd>cd {sitename}</kbd></code>

You will find the following structure after the &#8216;Running bundle install in &#8216; response has finished running.

<code>
404.html<br />Gemfile<br />Gemfile.lock<br />
_config.yml<br />
_posts<br />about.md
<br />index.md
</code>

For the site I built, I was not interested in having the default post format that you will find in the majority of examples. If you change directory into _posts:

<code>cd _posts</code>

You will find a file with the name in this format below:

<code>2018-10-22-welcome-to-jekyll.markdown<br /></code>

We are going to generate a site with custom page structure and to do this we're going to use collections and delete the posts structure. To do this, we'll edit the _config.yml file and set up some extra folder structure; in this case we want a folder called tutorials.

Remove \_posts, make folder and then edit the \_config file:

<code>rm -R _posts<br />mkdir _tutorials<br />nano _config.yml</code>

Now upon entering the edit screen you will need to edit the config file to have an entry for collections. Look for the line below which starts collections and how this is output.

<code># Welcome to Jekyll!<br /># You can create any custom variable you would like, and they will be accessible# in the templates via {{ site.myvariable }}.<br /><br />title: Cambridge Festival of Ideas Photogrammetry workshop<br /><br />email: dejp3@cam.ac.uk<br /><br />description: &gt;- # This site will provide training material for the Museum of Classical Archaeology's workshop on photogrammetry.<br /><br />baseurl: "/festivalOfIdeas" <br /><br />url: "https://UniversityofCambridgeMuseums.github.io/" <br />twitter_username: dejpett<br />github_username:  portableant<br />logo: images/festivalLogo.jpg<br /><br /># Build settings<br /><br />markdown: kramdown<br />theme: jekyll-theme-minimal<br />plugins:  <br />    - jekyll-feed  <br />    - jekyll-sitemap  <br />    - jekyll-seo-tag  <br />    - jemoji  <br />    - jekyll-mentions<br /><br /># Custom structure<br />collections:  <br />   tutorials:    <br />      output: true<br /></code>

This config file also has:

  * some extra plugins
  * a specified theme style
  * the base url
  * the url I intend to serve from
  * the markdown type
  * the plugins I want to use on gh-pages

If you look at the plugins section, you will see I have asked for feed, sitemap, seo, emoji and git hub mentions to also be included. Now create a page inside the _tutorials folder:

<code>touch _tutorials/introduction.md<br /></code>

Now edit this file and add the following at the top:

<code>
--- <br />
layout: default <br />
author: your name <br />url: tutorials/introduction <br />---</code>

Save the file and then you can test to see if this has worked:

<code>jekyll serve</code>

Go to

<code><a href="http://127.0.0.1:4000/tutorials/introduction ">http://127.0.0.1:4000/tutorials/introduction </a></code>

and you will see a page with the title of the file and your name. Jekyll parses the markdown file name to give the page a title by default. How clever is that? When you run the serve command, a static file is compiled into the _site folder.

Now you can create the page files that you need. Edit the index.md file, 404.html and about.md file as much as you want. You can find more examples of logic for rendering page lists and ordering of these in the repo referred to above.

So that is the basics of getting a Jekyll site running with custom page structure. You now probably want to know how to deploy to Github.

### Github pages

Git scares people, Github is the friendlier face. Still scary for most. So how do you get your Jekyll site running off there. Follow these steps (assuming you have a Github profile):

  1. Create a new empty repository
  2. Look for the instructions on how to add data
  3. Go back to your local folder in which you have been developing and run the following

<code>git init<br />echo "# teachmephotogrammetry" &gt;&gt; README.md<br />git add *<br />git commit -m "Added the base layout"<br />git remote add origin path/to/gitrepo<br />git push -u origin master</code>

You now should have your jekyll code on github if all went well. Now you need to create the branch that will auto-render on [gh-pages](https://pages.github.com/). Follow these steps:

  1. Go to the github repository
  2. click on the branches button
  3. click add new branch and type gh-pages

If you wait for a few minutes and then go to:

<code>https://yourusername.github.io/repositoryname</code>

You should see a jekyll powered website. My general way of working is to push to the master branch any changes I make and then pull these changes across to the gh-pages branch.
