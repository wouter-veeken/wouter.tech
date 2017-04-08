+++
date = "2017-04-08"
title = "Customizing the printed version of your Flare web output"
description = "Learn how to determine what gets printed and what doesn't."
draft = "false"
highlight = "true"
tags = [
    "madcap",
    "flare",    
    "css",
    "design"  
]
categories = [
    "design"
]
+++

Lots of people who read docs, myself included, like to occasionally print (parts of) them to read them the old-fashioned way. So if you're using any kind of web output for your Flare project, it's a good idea include a **Print** button on each page. The most obvious way to do this is to [add a topic toolbar proxy to your master page][url-topic-toolbar-proxy].

If you've customized your master pages a lot, however, you might notice a problem when you print a page: in addition to the topic's body text, all sorts of unnecessary elements are also printed, e.g. the side menu, mini-TOCs, breadcrumbs, etc. Luckily, there's an easy way to determine which parts should and shouldn't be printed:

1. Add the following lines to your project/topic stylesheet:

    ```css
    @media print {
        .no-print,
	      .no-print * {
		         display: none !important;
	      }
    }
    ```

    This means that any elements with the class `no-print`, _and_ any children of elements with that class, will be hidden from printed output.

2. In your master pages, add the `no-print` class to all relevant elements.

It will probably take a bit of trial and error before you get the printed output to look exactly as you want. Remember that you can use the developer console in your browser (**F12** or **Ctrl + Shift + I**) to add and remove classes on the fly.

[url-topic-toolbar-proxy]: http://help.madcapsoftware.com/flare2017/Content/Proxies/Using_the_Topic_Toolbar_Proxy.htm
