+++
date = "yyyy-mm-dd"
title = "Screenshots: Why readers love them, but writers hate them"
description = "On screenshots and why they're a hassle to maintain."
draft = "true"
highlight = "true"
tags = [
    "documentation",    
    "screenshots"
]
categories = [
    "",
    ""
]
+++

The human brain is [lightning fast][1] at processing visual information. According to [some sources][2], we process it 60,000 times faster than text. It's hardly surprising, therefore, that people constantly ask for screenshots in documentation.

As a reader, I like screenshots too. But as a writer, they can really get in your way. As much as they make the reader's life easier, they can really depress writer.

## Should I use screenshots?

Should I focus on text or screenshots? The motto is: support as many types of learners as possible. Some people learn visually, others verbally. You can't please everybody, but try to cover as many bases as you can.

Like the question "Should I focus on table of contents or search?", the answer is: both.

## How many screenshots is too many?


<!-- Chat logs from WTD -->

So I’m here with an age old question: how do you feel about screenshots in documentation? Specifically, I’m talking about docs focused on admin/advanced users.

I inherited a help system with, in my opinion, waaaaaaaaay too many screenshots. I think that more than 90% of the screenshots could be removed, because most of them just show an image of a screen that’s being discussed which I feel is redundant.

[4:05]
This may have been discussed before, and I tried searching, but I can’t see very far back in the Slack history.

[4:07]
I’ve exhausted the articles I can find via Google, but just curious and would like to get a feel for what everyones thoughts are currently.

wouter.veeken
[4:13 PM]
Unless it makes your projects completely unmanageable, more screenshots = more better. You want to support as many kinds of learners as you can.


jason.gray [4:15 PM]
I try to take a minimalist approach to screenshots. It's often a sign that developers have written a document, when instead of instructions you get a page of screenshots with lines pointing every which way.


krollins [4:16 PM]
@mikelandry The question is, does it help users, and is the time cost worth it? Maintaining screenshots can be expensive time-wise. I think it's a balance you need to determine for every help system. In the case of advanced users, I'd err on the side of less is more.

shauna [4:16 PM]
I'd say as long as the screenshots provide the relevant information. A screenshot of an entire screen outside of the "this is what the dashboard looks like" is less than useful. A screenshot with either the relevant part highlighted or cropped to that part is far more useful IMO


steveburnett [4:17 PM]
As few as possible, and trimmed to only the relevant section of the screenshot but include enough that the reader can find the clipped section when they’re looking at their screen.

[4:18]
Screenshots are brittle in that they age badly: any change to the UI that is visible in the screenshot - be it color, shape, text - will result in a need to update that screenshot for a change that has nothing to do with the task or feature being documented. Because of that, screenshots can add a lot of additional work to a doc cycle. Also they cause challenges for internationalization and localization of the documentation.


jason.gray [4:18 PM]
Also, whenever a system UI changes, you have to go back and redo all the shots.

[4:18]
Yes as @steveburnett says

wouter.veeken
[4:20 PM]
That's an important point. My thing is, though, when you're switching back and forth between a list of numbered steps and a GUI, every switch requires a mental translation between text and image. Screenshots can really smooth that transition.


[4:21]
Also, they're good 'landmarks' for scanning.

jason.gray [4:23 PM]
Yea it really depends how many you're talking about. I just don't feel it looks very professional when a page is bogged down with screenshots. The shot should generally highlight something that is less than obvious - maybe by combining several navigational steps into one image, for instance. It's all about the balance

wouter.veeken
[4:24 PM]
> It's all about the balance
As always :wink:

mikelandry [4:35 PM]
Thanks all, I appreciate the input. A lot of this confirms my own impressions, observations, and instincts.

[4:35]
Now to start Project: Screenshot Eradication

starfallprojects [4:46 PM]
I like reading things with screenshots, and I like including them. That said, I'm starting from a set of docs with almost nothing, and large chunks of text. Everything in moderation :slightly_smiling_face:

conor [4:50 PM]
I’d add two pieces if you do include screenshots in your help content:

- Consider creating guidelines around how you crop and annotate screenshots. For example, AWeber tends to use a lot of screenshots but their consistency makes things feel clean and clear, IMO: https://help.aweber.com/hc/en-us/articles/215872618
- Take screenshots of realistic and contextual scenarios, perhaps with a “staging company” to help (à la #5 here: https://www.helpscout.net/blog/improve-help-content/) (edited)


sej [5:52 PM]
I would say as less screenshots as possible.

1. With the rapid changes in UX, it's almost impossible to keep screenshots up-to-date.
2. With writers working in agile most times you may not even get screenshots when you are writing the
 docs.
3. Screenshots are not accessible. If at all you need to put screenshot, you should add enough description so that user can execute task without seeing screenshots.
4. Too many screenshots increase page load time too.
5. If a procedure with 10 step have about 5 screenshots, it simply makes the end user feel that it's too long procedure and deters them at times, since screenshot will add into the length.


[5:53]
But that said, screenshot does help in explaining complex UI. But on the other hand if you think you must have screenshot to explain the UI then it's a strong point to rethink UI.


jamerkhanov [6:07 PM]
Our UI is insanely complicated, so we think it's important to include plenty of screenshots for guidance. But when I started at the company, I did go through the docs and delete certain types of screenshots, primarily error message and confirmation dialog box screenshots, as well as screenshots of wizards since those have all the instructions you need self-contained as it walks you through the steps.

joster [6:23 PM]
So, obviously this is more difficult to implement with native apps than webby things, but: my personal rule is that screenshots have to be auto-generated (by Selenium for web, or Sikuli for native), because otherwise they're a maintenance nightmare.


[6:24]
So when there's a request for MOAR SCREENSHOTS, my answer is "No problem! Here's the dev time cost."

thejodester_f5
[7:03 PM]
I :heart: screenshots, but I’ve almost completely ceased to use them (and not just because I’m documenting things that don’t have a GUI yet). I’m intrigued by GIFs that show code samples but I’m hesitant to go down that path as well, for the same reason — there is only one of me and I simply don’t have the bandwidth to maintain them for all of the products I document.

lemay [7:05 PM]
I have been burned so badly on screenshots changing out from under me that I admit I’m pretty leery of using them, even though they are often extremely useful for users. (edited)

wouter.veeken
[7:07 PM]
_Screenshots: readers love them, writers hate them._

1 reply 4 days ago View thread

wouter.veeken
[7:09 PM]
Good blog title/topic. (NOBODY STEAL MY IDEA.)

steveburnett [7:18 PM]
“Screenshots: Threat or Menace?”


rosewms
[7:19 PM]
“more tonight at 11!”

neal [7:20 PM]
Not to worry. My blog post will be totally different: “Screenshots: readers love them, writers _loathe_ them” :wink:

starfallprojects [7:26 PM]
Screenshots II: Just when you thought it was safe to go back in the webhelp


thejodester_f5
[7:28 PM]
Screenshots II: Electric Boogaloo

rosewms
[7:30 PM]
_whispers softly_ I actually enjoy screenshots


[7:30]
https://media.giphy.com/media/iuugcO9k7JP5S/giphy.gif (729kB)

neal [7:34 PM]
@rosewms Same! I like working with them.

adammichaelwood [7:37 PM]
There have been a few discussions here and there about automating screen shots with (for example) selenium. This is a topic I'm hoping more people (including myself) will explore.
  7 replies Last reply 4 days ago View thread

mikelandry [7:39 PM]
I would like screenshots more if I had more time to keep them updated.


sej [7:39 PM]
alana and thejodester_f5
So you know if any company doing this? It sounds very interesting.

joster [7:40 PM]
alana and thejodester_f5
I'm doing it, but I'm the only tech writer at my company

joster [7:42 PM]
alana and thejodester_f5
documentation pages with screenshots have new screenshots taken as a git hook with every commit


joster [7:43 PM]
alana and thejodester_f5
theoretically, developers are supposed to let me know when stuff changes that will break screenshots, but if not it's caught by QA when we cut to stable


<!-- Links and references -->
[1]:http://news.mit.edu/2014/in-the-blink-of-an-eye-0116
[2]:https://rhdeepexploration.wordpress.com/2011/12/05/visuals-60000-times-faster/
