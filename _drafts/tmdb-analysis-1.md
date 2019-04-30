---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Movies and Neural Networks part I - the strategy
categories: ML
tags: machine learning, movies, TMDB
author_bio: Author is a computational biologist at NCBS, Bangalore.
author_twitter: rohitsuratekar
header_image: 2018-10-10-tmdb-analysis-1/reel.jpg
---

Anyone who is a fan of movies or TV serials have visited [IMDB](https://www.imdb.com/) at least once. It is currently one of the biggest movies and television database available (as of October 2018). Such a huge database inevitably calls for [some](https://www.google.com/search?q=imdb+and+machine+learning) machine learning analysis and profitable predictions. Various companies are already using it to analyze reviews and recommend movies/TV shows to their customers. For example, more than 80% of the TV shows people watch on Netflix are discovered through the platform’s recommendation system which uses machine learning approaches<sup>[1](#ref1)</sup>. This provides evidence of huge economical benefits of such analysis. As IMDB is a subsidiary of the Amazon, you can think of what kind of data-analysis will be going on behind the scenes :P Nonetheless, I wanted to take a handle on such data and play around with it.  In next few sections I will explain my strategy for such analysis. However, just a note to readers, I am not going to discuss any results in this blog post. I will just illustrate a preliminary analysis and some visualizations to understand data. 

### The database

I needed properly annotated data-set related to movies. There is one [section](https://www.imdb.com/interfaces/) on the IMDB website about their data-set. This includes lot of details like title, cast and crew etc. However, it is subset of their full data-set. In addition TV serials are included in this data-set. For simplicity, I had decided to use only movies (for now). Hence, I decided to use some other data-set which concentrates on movies and other people have tried and tested for machine learning related analysis. I could just remove TV serial entries from IMDB data-set but it will reduce data points heavily. Hence I finally decided to use [TMDB](https://www.themoviedb.org) data-set. I had previously used this [data-set](https://www.kaggle.com/tmdb/tmdb-movie-metadata) in one of the [workshop](https://ncbs-students.github.io/Workshop2017/) I arranged some time ago. So I knew that it is well annotated and have everything I need.

### Database Visualization

I started with basic dataset check points,

Number of Entries: 


### References and Notes
1. <a name="ref1"></a> Libby Plummer (2017) This is how Netflix's top-secret recommendation system works. [Wired](https://www.wired.co.uk/article/how-do-netflixs-algorithms-work-machine-learning-helps-to-predict-what-viewers-will-like) Accessed on 10 Oct 2018. 

*(Header image is downloaded from Pixabay.com under CC0-license)*