+++
date = "2017-03-29"
title = "Creating a responsive layout in Flare's Top Navigation output"
description = ""
draft = "true"
highlight = "true"
tags = [
    "madcap",
    "flare",    
    "css",
    "design"
]
categories = [
    "tutorials",
    "design"
]
+++

<!-- Introduction -->

> **Summary:** This post explains how to create a custom reponsive layout, as shown [here][vc help], for the Top Navigation output in Madcap Flare.

## Introduction

I believe that beautiful docs are docs that get read. So if time allows, I always put a little extra energy into making mine look as nice as possible  -- with varying levels of success, of course. Nowadays, high on the list of requirements for good web design is ['responsiveness'][responsive design]: your content should look good on any device, regardless of screen size.

Madcap Flare offers the Top Navigation output template, which claims to be responsive. And it is, but it takes a somewhat ham-fisted approach. When you scale down the window, elements that don't fit on a smaller screen are simply hidden, rather than placed somewhere else:

![Example of default Flare TopNav output][img flare topnav example]

Compare that to something like the [MailChimp Knowledge Base][mailchimp kb], where the content is intelligently rearranged as the screen gets smaller:

![Responsive design in MailChimp Knowledge Base][img mailchimp kb example]

This post explains how to emulate the responsive design of MailChimp's KB in your Flare project, similar to how I did for [this project][vc help].

### Disclaimer

I am not a web designer. My HTML and CSS skills are not even that strong. Most of what I know is cobbled together from [w3schools][w3schools], [stackoverflow][stackoverflow] and the blogs of true Flare wizards like [Mike Kelley][mike kelly blog] and [Dave Lee][dave lee blog]. So feel free to trust the advice of pretty much anyone over mine when it comes to design best practices and so on. I'm just showing you what I've done, in the hopes it'll be of some use to you!

## How to do it

### Goal

The example I'm using here has a couple of responsive elements:

![Image showing responsive elements][img responsive elements]

On a tablet, these elements are rearranged like so:

![Image showing responsive elements on tablet][img responsive elements tablet]

And on mobile:

![Image showing responsive elements on mobile][img responsive elements mobile]

Basically, it's a horizontal configuration that gradually morphs into a vertical one as the screen gets smaller.

<!-- TODO: Describe: the responsive elements of VC help. -->

### What you'll be doing

A really quick lesson on Flare output styling:

![Diagram showing anatomy of Flare output][img flare styling]

As you can see, the design is controlled on multiple levels: skin, master page, topic and stylesheets. Most of the work you're about to do will mainly touch the master page and stylesheet level.

#### Stylesheet

Like I said earlier, what you're going for is a gradual change from horizontal to vertical. This is basically a matter of cleverly using the `width` property. On a large screen, you want your elements to only take up part of the screen width, so that they can appear side by side. But on a smaller screen, you want them all to be exactly as wide as the entire screen, so that they have to appear under each other.

1. Create a new stylesheet called (for example) `responsive-sizing.css`.
2. Add width classes
3.

You don't have to use a separate stylesheet. I'm just doing what I think is best, and as I said, I'm not really trained. A real web designer can probably tell you what the current ~~dogma is~~ best practices are.

#### Master page


Outline:

* Responsive design: what is it, why do I need it? (Keep this short!)
* The goal (example of end result)
* How to do it:
    * Stylesheet classes
        * sizexofy, mid-sizexofy
        * desktop-only, mobile-only, hide-desktop, hide-mobile
    * Master page

<!-- Links and references -->
[vc help]: http://help.n200.com/visitconnect/
[responsive design]: #
[img flare topnav example]: #
[mailchimp kb]: #
[img mailchimp kb example]: #
[w3schools]: www.w3schools.com
[stackoverflow]: www.stackoverflow.com
[mike kelly blog]: http://mike.kelley.consulting/blog
[dave lee blog]: https://ukauthor.wordpress.com/
[img flare styling]: #
[img responsive elements]: #
[img responsive elements tablet]: #
[img responsive elements mobile]: #
