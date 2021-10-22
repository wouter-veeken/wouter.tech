+++
date = "2021-10-22"
title = "Why you shouldn't use readability scores for technical documentation (and what to use instead)"
description = ""
draft = "false"
highlight = "true"
tags = [
    "documentation",    
    "analytics"
]
categories = [
    "technical writing",
    ""
]
+++

# Why you shouldn't use readability scores for technical documentation (and what to use instead)

Readability scores promise a simple, unambiguous metric for how easy a given piece of text is to read. There are many different readability scoring systems, but the ones I know to be in common use are:

- [Flesch-Kincaid Grade Level]
- [Gunning Fog Index]
- [SMOG Index]

Each score uses its own subtly different equation based on the ratios between characters, syllables, words, and sentences in the text. The result is usually meant to express how educated a reader must be to understand the text.

The problem with these readability scores in the context of technical documentation, is that word length is not as meaningful a measure of complexity as it might be in ordinary prose. That is: while the clarity of a newspaper article might be improved by writing "connect up" instead of "concatenate", or "ask" instead of "request", the reverse is often true for documentation intended for software developers. 

Attempting to use any of the abovementioned scores as a measure of clarity for your documentation can lead to editing choices that raise the score while lowering readability. In other words, _you'll be making your text worse while thinking you're making it better_.

## Alternative quality metrics for docs

I'm no mathematician, so I wouldn't how to devise a better readability formula. But I do suspect that one or more of the following metrics could feature as components in the equation:

- **Average number of sentences per paragraph.** A long text full of complex ideas is easier to read when split it into brief paragraphs. 3-4 sentences to a paragraph, including 1 topic sentence and 2-3 supporting sentences, is usually best. ("Ratio of topic sentences versus supporting sentences" could be a useful secondary metric.)

- **Ratio of headings vs. paragraphs.** Readers are impatient and like to skim. Rather than reading a page top to bottom, they'll often jump straight to the part that's most relevant to them. Using plenty of (meaningful) headings helps them determine at a glance where that part is. For online documentation, 1 heading per 2-4 paragraphs is probably a good target ratio.

- **Distance between the beginning of a paragraph and its most meaningful words.** If you're familiar with the [F-shaped reading pattern](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) observed in readers of online content, you know that the first few words in a paragraph are the ones most likely to be read. Strive to put the most important information as close to that position as possible. If you can, make the [first two words](https://www.nngroup.com/articles/first-2-words-a-signal-for-scanning/) meaningful.

- **Ratio of passive vs. active constructions.** Passive voice is harder to process than active voice. You can't always avoid passive voice (nor should you), but I would try to keep the ratio of passive to active constructions to no more than 1:6.

- **Ratio of adverbs vs. verbs; adjectives vs. nouns.** Clear documentation is light on adverbs and adjectives. The information conveyed by these words is often not relevant, but when it is, they can signal that you're packing too much information into a single sentence. I'd aim for a ratio of no more than 1:5 for both adjectives:nouns and adverbs:verbs.

- **Ratio of code vs. prose.** The core of good developer documentation is good sample code. Readers will forgive a surprising amount of bad writing if it's surrounding blocks of clear, usable code. I'd say a good code:prose ratio is at least 50:50, but that is basically a guess and will not be true for every type of doc.

- **Ratio of content words vs. function words.** Nouns, verbs, adjectives, and adverbs are content words; prepositions, articles, and conjunctions are function words. You need both to write a coherent text, but if you want it to be easy to understand, you should maximize the ratio of content words relative to function words. [Some research](https://www.researchgate.net/figure/Mean-Content-WordFunction-Word-Ratio-as-Percentage-of-Total-Words-Per-Answer_tbl2_265115908) suggests that a good content:function ratio might be 6:4.

## What do you think?

The above is intended as a basis for discussion. I'm making some poorly supported claims here—I certainly don't have any data to back them up. But this topic is very interesting to me and I'd love to get your perspective on it. Perhaps together, we can come up with a readability score that actually works for software documentation. Feel free to leave your thoughts below!

<!-- Links and references -->

[Flesch-Kincaid Grade Level]: https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests
[Gunning Fog Index]: https://en.wikipedia.org/wiki/Gunning_fog_index
[SMOG Index]: https://en.wikipedia.org/wiki/SMOG
