---
id: 469
title: 'Going static: Jekyll power'
date: 2018-10-22T21:21:42+01:00
author: Daniel Pett
layout: revision
guid: https://769E81FC-317E-4C97-8E4E-262F645EEBF0
permalink: /466-revision-v1/
---
At the Fitzwilliam Museum, we have a large amount of old websites that were built over the last decade. Many of these are now presenting security risks as they are on old WordPress installations, or they are just plain hand coded HTML. To alleviate the burden for supporting these sites, I have been transferring as much as possible to Jekyll powered Github Pages instances (although I am also looking at Gatsby). 

Generating a Jekyll site is pretty straightforward, and this post outlines how I built the University of Cambridge Museums tutorial site for the Festival of Ideas event I ran on Photogrammetry.

### Installing Jekyll

I am assuming in this instance, you, the reader will be on OSX and have homebrew installed, RVM and the lastest Ruby and can use terminal.  If you have all of those set up, you will now need to install the Jekyll gem. So go to terminal and issue this command:   

<code>gem install bundler jekyll<br /></code>

Once that has completed (if your permissions are all set correctly) you should have Jekyll ready to go.

### Generating the site skeleton

You&#8217;re now ready to create the basic outline for the site. In terminal again run the following command, replacing {sitename} with the folder you want to create:

<code>jekyll new {sitename}<br /></code>

This creates a new folder with the base skeleton for a Jekyll app. Change directory to this:

<code>cd {sitename}</code>

You will find the following structure after the &#8216;Running bundle install in &#8216; response has finished running. 

<code>404.html<br />Gemfile<br />Gemfile.lock<br />_config.yml<br />_posts<br />about.md<br />index.md</code>

For the site I built, I was not interested in having the default post format that you will find in the majority of examples. If you change directory into _posts:

<code>cd _posts </code>

You will find a file with the name in this format below:

<code>2018-10-22-welcome-to-jekyll.markdown<br /></code>

We are going to generate a site with custom page structure and to do this we&#8217;re going to use collections and delete the posts structure. To do this, we&#8217;ll edit the _config.yml file and set up some extra folder structure; in this case we want a folder called tutorials. 

Remove \_posts, make folder and then edit the \_config file:

<code>rm -R _posts<br />mkdir _tutorials<br />nano _config.yml</code>

Now upon entering the edit screen you will need to edit the config file to have an entry for collections. Look for the line below which starts collections and how this is output.

<code># Welcome to Jekyll!<br /># You can create any custom variable you would like, and they will be accessible# in the templates via {{ site.myvariable }}.<br /><br />title: Cambridge Festival of Ideas Photogrammetry workshop<br /><br />email: dejp3@cam.ac.uk<br /><br />description: >- # This site will provide training material for the Museum of Classical Archaeology's workshop on photogrammetry.<br /><br />baseurl: "/festivalOfIdeas" <br /><br />url: "https://UniversityofCambridgeMuseums.github.io/" <br />twitter_username: dejpett<br />github_username:  portableant<br />logo: images/festivalLogo.jpg<br /><br /># Build settings<br /><br />markdown: kramdown<br />theme: jekyll-theme-minimal<br />plugins:  <br />    - jekyll-feed  <br />    - jekyll-sitemap  <br />    - jekyll-seo-tag  <br />    - jemoji  <br />    - jekyll-mentions<br /><br /># Custom structure<br />collections:  <br />   tutorials:    <br />      output: true<br /></code>