---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Creating an artificial screenplay with neural networks
categories: analysis 
tags: python, machine-learning, neural-networks
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar
header_image: 2020-10-16-text-generation/got.jpg
assets: /assets/article_images/2020-10-16-text-generation
---

National Language Processing ([NLP](https://en.wikipedia.org/wiki/Natural_language_processing)) is one of the highly researched topics in the field 
of Artificial Intelligence ([AI](https://en.wikipedia.org/wiki/Artificial_intelligence)). It is widely used in different contexts like language 
translation, personal assistants (like [Siri](https://en.wikipedia.org/wiki/Siri)), spam detection, document tagging, speech 
recognition etc. Researchers are developing new methods and tools every day related to NLP. 
This has led to a drastic improvement in many machine learning algorithms. I have been curious 
about NLP for a long time.  Before even understanding the nitty-gritty of it, I was unknowingly 
using it in my old data-analysis projects (like [this](https://weirddata.github.io/2018/09/15/orf-applications.html) and [this](https://weirddata.github.io/2019/03/12/indian-publications.html)). In the past, I have worked 
on a variety of text data-sets like books, news, articles, social media posts etc.


Since last year, I have been playing with the subtitles of different TV serials. There is a 
plethora of it on the internet. Those are ready-made datasets for many NLP related tasks 
like tagging, sentiment analysis, tokenizing etc. I have been using a few of such methods in 
analyzing these subtitles. This blog provides an overview of some of the early results of that 
analysis. It is a continuously evolving project. You can track the progress on its GitHub [repository](https://github.com/WeirdData/SubtitleAnalysis).

> If you do not wish to read the full blog, [here](https://subtitleanalysis.web.app/) is the live implementation of this concept.


## Idea and Concept

Simple idea was to make a platform where one can generate their screen-play for the entire TV serial. 
Where the user can tell how they want the dialogue to start and AI will complete the rest of the conversation. 
It will provide enough space for both creativity as well as NLP implementation.


Generating such an artificial text is not a novel idea. Many people have used it in a variety of contexts before. 
Most notably, to generate a summary of existing documents or articles<sup>[1](#ref1)</sup>. The main idea behind such analysis is 
to ‘learn’ the grammar, style and words used in a given text corpus. This ‘learning’ is typically done by 
generating probability matrices or training neural networks based on similar kinds of text. Technical details 
of this process are out of the scope of this blog post.


I took a similar approach. I reasoned that even if TV serials dialogues are written by multiple screenwriters, at the end the 
tone of the serial will be similar throughout its broadcast time. For example, dialogues of fantasy series like [Game of Thrones](https://www.imdb.com/title/tt0944947/) 
will use typical old-style English. It will have sentence structures which will mimic the fictional world of magic. In contrast,
 crime drama series like [Criminal Minds](https://www.imdb.com/title/tt0452046/) will have a lot of words related to crime and police work. Their structure will 
 represent real life. So, if I develop an NLP model based on either of these text sources, it should preserve such sentence style and grammar. 
 Once I have that, I can use it to generate the dialogues which will preserve the same sentence structure and grammar.
 
## Dataset
I use publicly available subtitles for different serials. In this blog I will talk about three 
different series of different genres. 

|TV Serial | Genre |No. of Episodes |
| -- | -- | -- |
| [Game of Thrones](https://www.imdb.com/title/tt0944947/) | Fantasy  | 60 |
| [The Big Bang Theory](https://www.imdb.com/title/tt0898266/)  | Comedy  | 279 |
| [Criminal Minds](https://www.imdb.com/title/tt0452046/)  | Crime Drama  | 299 |


I extracted the text from subtitles of all of these TV serials. I wanted to develop three different models 
representing these 3 serials. To avoid data bais, I decided to build the models based on the same amount of 
source material.  As these series had different amounts of dialogues and screen time, I used the first 
250000 characters from each of them. This much text was good enough to fit in my computer memory and perform 
heavy analysis. Once I decided on the amount of text, I cleaned it (by removing unnecessary information like 
timestamp, Html tags etc) and prepared it for the next step.

## The Neural Network

One of the reasons behind picking up this project was also to learn about Recurrent Neural Networks ([RRN](https://en.wikipedia.org/wiki/Recurrent_neural_network)). 
They work like magic in so many different contexts<sup>[2](#ref2)</sup>. I used [LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory) 
in constructing a neural network in `keras` (see Fig [1](#fig1)). I fed in a different serial text to respective models.

|<a name="fig1"></a> <img src="{{page.assets}}/got_model.png" width="40%"/>|
|:--:|
| Fig 1: Architecture of the neural network used in this blog|

These models will take a series of strings as an input and will predict the next word. 
Then I can feed this output again back to my model and get the next word. One can repeat this 
process as many times to construct the entire screen-play :)

## The Screen-Play

Following are first 15 words predicted by all models based on respective starting input,

|Input | GOT Model | BBT Model | CM Model |
| -- | -- | -- | -- |
| who is | _who is_ your in life, how was she? so there would seem, my brother | _who is_ introduce us a waitress once. i can't look to look at that. | _who is_ n't. he's lying on the top of the conversation's to 15. |
| yesterday he | _yesterday he_ and the night's rule without a bastard, talk. it was said you... | _yesterday he_ capitol emotionally....hey, jerk, listen. then there's no problem... | _yesterday he_ almost playing. they're set over the house's well. but's television |
| king in the | _king in the_ vale, you must be robb. i'll make you lord ! i'm... | _king in the_ talents of hugh grant or sandra bullock. interesting. and would you agree that...| _king in the_ level of being worth office. wh how should you feel about me? we... |


As you can see, they are far from perfect. However, you can see the wording and tones of the sentences. 
I think, with little more training data and adjusting model parameters, I can improve the grammatical 
structure of the predictions.

I created a simple [website](https://subtitleanalysis.web.app/) where you can try out these model predictions by 
yourself. Please go through it and enjoy it!

## What’s next?

The first step of improvement will be to adjust various parameters and improve the grammatical structure 
of the prediction. Once I get grammar correctly, I will add full-sentence information in my model. 
This will improve the context-based prediction. Later on, I can provide weightage to specific serial 
characters and can assign proper dialogue to proper characters.


The final aim of this project will be to combine different models and produce the screen-play 
for inter-genre hypothetical TV series. If I could find some collaborator with [DeepFake](https://en.wikipedia.org/wiki/Deepfake) expertise, 
I could essentially make an entire artificial TV Serial :D

## References

1. <a name="ref1"></a> Subramanian et al. “On Extractive and Abstractive Neural Document Summarization with Transformer Language Models.” 
ArXiv:1909.03186 [Cs], Apr. 2020. [arXiv.org](http://arxiv.org/abs/1909.03186)
2. <a name="ref2"></a> The Unreasonable Effectiveness of Recurrent Neural Networks. https://karpathy.github.io/2015/05/21/rnn-effectiveness. [Accessed 16 Oct. 2020]
 

Full code can be found [here](https://github.com/WeirdData/SubtitleAnalysis). 

_All web links provided in this article are accessed on 16 Oct 2020 (if not mentioned otherwise)_

  
*(Header image by <a href="https://pixabay.com/users/simisi1-5920903/">simisi1</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*
