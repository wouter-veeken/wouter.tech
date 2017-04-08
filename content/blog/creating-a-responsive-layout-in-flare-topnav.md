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

I believe that beautiful docs are docs that get read. So whenever time allows, I invest extra effort into trying to make mine look as nice as possible (with varying levels of success). Nowadays, a clear requirement in that respect is ['responsiveness'][responsive design]: your content should look good on any device, regardless of screen size.

Madcap Flare offers the Top Navigation output template, which claims to be responsive. However, I'd describe its implementation of responsive design as somewhat ham-fisted. When you scale down the window, any elements that don't fit on a smaller screen are simply hidden, rather than placed somewhere else:

![Example of default Flare TopNav output][img flare topnav example]

Compare that to something like the [MailChimp Knowledge Base][mailchimp kb], where the content is intelligently rearranged as the screen gets smaller:

![Responsive design in MailChimp Knowledge Base][img mailchimp kb example]

In fact, I did my best to borrow (i.e. steal) the best parts of MailChimp's KB for my own design for the [Visit Connect Help][vc help]. The rest of this post discusses a few of the tricks I learned in the process.

### Disclaimer

I am not a web designer. My HTML and CSS skills are not even that strong. Most of what I know is cobbled together from [w3schools][w3schools], [stackoverflow][stackoverflow] and the blogs of true Flare wizards like [Mike Kelley][mike kelly blog] and [Dave Lee][dave lee blog]. So feel free to trust the advice of pretty much anyone over mine when it comes to design best practices and so on. I'm just showing you what I've done, in the hopes it'll be of some use to you!

## Get stuck in

### What you're aiming for

The example I'm using here has a couple of responsive elements:

![Image showing responsive elements][img responsive elements]

On a tablet, these elements are rearranged like so:

![Image showing responsive elements on tablet][img responsive elements tablet]

And on mobile:

![Image showing responsive elements on mobile][img responsive elements mobile]

So essentially, things gradually go from a horizontal to a vertical configuration.

<!-- TODO: Describe: the responsive elements of VC help. -->

### How to do it

A really quick lesson on Flare output styling:

![Diagram showing anatomy of Flare output][img flare styling]

The responsiveness we're aiming for is mainly controlled from the stylesheet and master page level.

#### Stylesheet

The change from horizontal to vertical is mostly a matter of cleverly using the `width` property on floating `<div>` elements.

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
