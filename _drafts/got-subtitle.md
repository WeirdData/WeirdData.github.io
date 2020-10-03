---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title: Insights into Game of Thrones dialogues
categories: NPL
tags: language, tv
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar
header_image: 2020-04-24-got-analysis/got.jpg
assets: /assets/article_images/2020-04-24-got-analysis
---

Since my childhood, I am reading fantasy novels and comics. I also grew up watching fantasy TV serials like 
[Alif Laila](https://en.wikipedia.org/wiki/Alif_Laila), That time I was limited to serials which were chosen by [Doordarshan](https://en.wikipedia.org/wiki/Doordarshan). 
However, now with so many available streaming services, we have so many choices that we spend much more time in deciding 
what to watch, as some call it <b>Netflix Fatigue</b> <sup>[1](#ref1)</sup>. With all plethora of movies and tv shows,
some creates cult <sup>[2](#ref2)</sup>. One of such cults I followed (and potentially you too) is HBO's 
 [Game of Thrones](https://www.hbo.com/game-of-thrones). It generated billions of dollars of revenue for HBO <sup>[3](#ref3)</sup>. 
 It has [won](https://www.imdb.com/title/tt0944947/awards) many awards including Golden Glob and many Primetime Emmy.
 This G.R.R.Martin's fantasy world has also attracted many researchers/analysts to perform [data-analysis](https://www.kaggle.com/search?q=game+of+thrones) 
 to publish [paper](https://www.tandfonline.com/doi/abs/10.1080/08164649.2014.998453). In this blog post, I will try to analyse 
 dialogues from this TV serial. 
 
### Data Collection
 
As I couldn't find original script/screenplays, the best way to access dialogues is to take a look at its subtitles. 
There were many existing subtitle databases on Kaggle, but most of them were incomplete or included only text. Hence, I 
decided to collect my own dataset. I looked around many subtitle providing websites and finally settled on *my-subs.co*. It 
allowed free download of community translated subtitles. I will be using only English subtitles. To automatically download
and format, I wrote small web-scrapping [script](https://github.com/WeirdData/SubtitleAnalysis) which can download 
subtitles from any TV show available on the website. These subtitles gave me all dialogues with timestamps. Finally, I 
had total of **73 subtitle files** representing all episodes from 8 seasons of Game of Thrones (GOT). 

### Method

To analyse all the next, of course, I used Natural Language Processing. I had previous experience with python's 
`nltk` package. I decided to use this package instead writing my own new methods. To get the full text, I removed timestamps
and other html formatting tags from the text. My aim was to identify <b>Part of Speech</b> (POS) tag of every word. I had 
to perform some text cleaning steps and assume few things to get appropriate results. 

#### Tokanization
It was most straightforward step in this analysis. In this step, I will extract all words from the sentence. For example,

> This is a sentence.

Above sentence will be converted into list of 5 tokens,

> ['this', 'is', 'a', 'sentence', '.']

For this, I just collected all sentences from all subtitle files and 
parsed them with default <b>word tokanizer</b> of `nltk`. Here script assumes that each sentence is separated by 
full-stop. Upon further inspection I found out that subtitle have some html tags like '\<i\>' and '\</i\>'.
I remove such tags from the text before tokanizing them. 

For tokanizing sentences, I use direct `sent_tokenize` function. 

#### Parsing and Tagging

Next step was to get [POS tags](https://en.wikipedia.org/wiki/Part-of-speech_tagging) from my tokanized text. For this, my 
initial strategy for tagging was to use N-gram tagger (n=3) with unigram as backoff. I was planning to train the model on
corpus of fantasy novels. Unfortunately, I could not find a proper corpus for this. I decided to use 'nltk' default corpus.

The most important problem I encounter was [truecasing](https://en.wikipedia.org/wiki/Truecasing). This can specially affect the
POS tag. It is a well-known problem in Natural Language Processing. For my simple analysis, I ignored this. My assumption was
that it will only affect pronoun tagging as we are mostly dealing with dialogues.

#### Calculating Frequencies
Word or Sentence frequencies are calculated with `FreqDist` class from `nltk`. In some cases I used python's `Counter` class.
While calculating frquencing, appropriate filters were applied before sending words into the `FreqDist`.

### Observations Regarding Sentences









Code used in the above analysis can be found [here](https://github.com/WeirdData/SubtitleAnalysis).

### References and Notes
1. <a name="ref1"></a> Kindra Cooper (2019). Netflix Fatigue: Too Many Streaming Services, Too Much Consumer Choice? Accessed on 24 April 2020 : [link](https://www.customercontactweekdigital.com/customer-insights-analytics/articles/netflix-subscription-fatigue). 
2. <a name="ref2"></a> Patrick Hanlon (2015). How 'Game Of Thrones' Has Become HBO's Global Cult. Accessed on 24 April 2020 : [link](https://www.forbes.com/sites/patrickhanlon/2015/04/10/why-hbos-game-of-thrones-has-become-a-global-cult/#253ded0a4d46). 
3. <a name="ref3"></a> Entertainment Strategy Guy (2019). How ‘Game of Thrones’ Generated $2.2 Billion Worth of Profit for HBO. Accessed on 24 April 2020 : [link](https://decider.com/2019/05/21/game-of-thrones-hbo-profits/)

*All web links from the article were accessed on 24 April 2020 (unless mentioned)*

*(Header image by <a href="https://pixabay.com/users/simisi1-5920903/">simisi1</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*
