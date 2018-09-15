---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Grant Proposal, Science Book and Fiction
date:   2018-09-15 09:00:00
categories: science
tags: science, language, books
author_bio: Author is a computational biologist at NCBS, Bangalore.
author_twitter: rohitsuratekar
header_image: 2018-09-15-orf-applications/writing_cover.jpg
---

I recently saw a news that one of the biggest scientific grant agency, Wellcome Trust, is [sharing](https://wellcome.ac.uk/funding/open-research-fund-applications-submitted) details of eligible applications for [Open Research Fund](https://wellcome.ac.uk/funding/open-research-fund) (ORF). As I am in process of various postdoctoral fellowship applications, I got curious to know how other researchers write their proposal. I read few of these proposals and wondered there must be some similarities between all these diverse proposals. It was obvious that there must be some similarity because they were written for a common theme. Nonetheless, I started analyzing these proposals to look for some similarities. Dirtiest way to check similarity is to check the grammar of proposals and what different kinds of words they use. 

### Controls
To check if grammar analysis is doing a correct job, I needed a few controls. In addition to these ORF proposals, I started looking for different text source which can be used in this analysis. I selected two different kinds of literary work, 
* **On the Origin of Species** by *Charles Darwin*  [Scientific, Non-Fiction, Treatise]
* **To Kill a Mockingbird** by *Harper Lee* [Bildungsroman, Fiction, Southern Gothic]

I also wanted to compare with "Harry Potter and the philosopher's stone" but there is no free version<sup>[1](#ref1)</sup> available for this book. ORF application data had a total of **87** proposals with total character length of **476381** (including spaces) (5475 on average). It includes on average **838.72** words per proposal. Just to cross if this is correct, I checked what is the word limit in the official [guidelines](https://wellcome.ac.uk/sites/default/files/sample-application-form-open-research-fund.pdf). It is 850 words. Hence I picked only first 476381 characters of 'On the Origin of Species' and 'To Kill a Mockingbird'. Headers were removed before text processing. 

### Tools
Next thing I needed was a way to analyze grammar. I can just split all content and then check which words are used most commonly. However, that will be the crudest thing one can do. I found a better option. I used Natural Language Toolkit ( `nltk` ) library<sup> [2](#ref2)</sup> of `python`. I used this library to tag each word of my text content. In nutshell, tagging will tell you what kind of grammatical object (*adjective, adverb, noun, verb* etc) is a current word in the context of the entire sentence. I used 'Universal Part-of-Speech Tagset' for simplicity. Further details regarding this tagging functions can be found [here](http://www.nltk.org/book/ch05.html#tab-universal-tagset). The code used in this analysis can be found on [GitHub](https://gist.github.com/rohitsuratekar/a76ec4c4abb9e041d5d6e8a4fc4683d1). 

### Most Common Objects
I checked what are the most common grammatical objects used in all three text content. 
<a name="fig1"></a>

|![Fig 1: adjective](/assets/article_images/2018-09-15-orf-applications/adjective.png "adjective")|
|:--:|
|Fig 1: Most common adjectives used. <sup>[3](#ref3)</sup>|

As it was Open Research Fund, I was expecting to get 'open' and 'new' as one of the most used adjectives (Fig [1](#fig1)). I was amused to see that Origin of Species has 'same' and 'other' as a top adjective. This makes sense considering Darwin was comparing a lot of observations in his famous book. 

Next obvious thing and probably most important in this context is to check most common nouns. 
<a name="fig2"></a>

|![Fig 2: noun](/assets/article_images/2018-09-15-orf-applications/noun.png "noun")|
|:--:|
|Fig 2: Most common nouns used. <sup>[3](#ref3)</sup>|

As seen in Fig [2](#fig2), 'Data', 'Research' and 'Researchers' were most used nouns in the ORF proposals. It looks like everyone likes to concentrate on the 'data'. 'health' and 'community' is also on top because one of the aims of ORF is to 'making health research more open'. Few more of most common nouns are shown in Fig [3](#fig3). Our control worked as expected. To kill a Mockingbird gave 'jem', 'atticus' and 'dill' as most common nouns which are names of few of the main characters of the book. Furthermore, it was not surprising to see 'species' and 'selection' as most common nouns from the origin of species. I am little surprised by seeing the word 'science' at such a lower rank in ORF proposals (Fig [3](#fig3)).
<a name="fig3"></a>

|![Fig 3: noun extra](/assets/article_images/2018-09-15-orf-applications/word_cloud.png "noun extra")|
|:--:|
|Fig 3: Top 100 nouns used in ORF applications. <sup>[3](#ref3)</sup>|


|![Fig 4: word cloud](/assets/article_images/2018-09-15-orf-applications/other_cloud.png "word cloud")|
|:--:|
|Fig 4: Top 100 nouns used in On the Origin of Species and To Kill a Mockingbird. <sup>[3](#ref3)</sup>|

Next, I checked what are the most common verbs. Interesting to see how the 'tense' is changing in a different kind of literary work. As we are looking into proposals, we will get future tense of verbs. I was surprised to see the similarity between proposals and the origin of species. 

|![Fig 5: verb](/assets/article_images/2018-09-15-orf-applications/verb.png "verb")|
|:--:|
|Fig 5: Most common verbs. <sup>[3](#ref3)</sup>|

Following are few more plots which shows some more grammatical objects and their distribution,

|![Fig 6: adverb](/assets/article_images/2018-09-15-orf-applications/adverb.png "adverb")|
|:--:|
|Fig 6: Most common adverbs. <sup>[3](#ref3)</sup>|

|![Fig 7: adposition](/assets/article_images/2018-09-15-orf-applications/adposition.png "adposition")|
|:--:|
|Fig 7: Most common adpositions. <sup>[3](#ref3)</sup>|

|![Fig 8: pronoun](/assets/article_images/2018-09-15-orf-applications/pronoun.png "pronoun")|
|:--:|
|Fig 8: Most common pronoun. <sup>[3](#ref3)</sup>|

### Final Remarks

In the end, I can't say I found any similarity between these proposals. However, for sure there are some similar grammatical structures as words popping up. This is very small data-set to conclude anything. This will be probe to develop new classifier which should able to classify article or text content into its genera based on grammar structure and words used. 


### References and Notes
1. <a name="ref1"></a> Free text for both the books was taken from Archive.org. : [The origin of species](https://archive.org/stream/originofspecies00darwuoft/originofspecies00darwuoft_djvu.txt), [To Kill A Mockingbird](https://archive.org/stream/ToKillAMockingbird_201604/To%20Kill%20A%20Mockingbird_djvu.txt)
2. <a name="ref2"></a> Bird, Steven, Edward Loper and Ewan Klein (2009). Natural Language Processing with Python.  O'Reilly Media Inc.
3. <a name="ref3"></a> In 476381 characters including spaces. 

Code used in the above analysis can be found [here](https://gist.github.com/rohitsuratekar/a76ec4c4abb9e041d5d6e8a4fc4683d1).

*(Header image is downloaded from Pixabay.com under CC0-license)*