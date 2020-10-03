---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  How far can you reach by walking?
date:   2018-07-15 13:34:25
categories: featured
tags: maps, cartography
author_bio: Author is a computational biologist at NCBS, Bangalore.
author_twitter: rohitsuratekar
header_image: 2018-07-15-longest-distance/distance_feature.JPG
---

I recently ‘re-watched’ movie [Forrest Gump](https://www.imdb.com/title/tt0109830/). Tom Hanks' acting was magical. There is [scene](https://www.youtube.com/watch?v=ymiZFPauvlQ) in the movie where he starts running whole day and roams around the city. It got me thinking about such random running. If I were to do something like that what different areas can I visit around my institute? 

### Strategy 

I immediately fired up my Google Maps app and started fiddling around. One way to answer this question is to check how far I can go from the origin (my institute) in different time steps. Crudest thing I can do is to assume some average walking speed and draw a circle around my institute with radius equal to my speed into time. However, this will not be correct measurement as I am not going to be walking in straight line. Walking route will have multiple turns and dead ends. Actual distance covered will depend on an exact tracing of the route. Hence, I decided to test this with some program where I can trace all possible routes around my origin. 

I have previously played around with Google Map API as well as Google Earth Engine. These two are very feature-rich and used by millions of researchers across the globe. Somehow, I was not able to do such analysis with this API. Then I stumbled upon [OSMnx](https://github.com/gboeing/osmnx) library on github. This simple library was developed by [Geoff Boeing](http://geoffboeing.com) of UC Berkeley. This library uses Open Street Map API along with `rTree` and `Geopandas` to construct simple functions. I was excited to see these simple functions doing some crazy analysis. Setting up this library on Windows in `conda` environment was very tricky. After frustrating 3 hours of internet search and downgrading few dependencies, finally it started working and I am ready to go.


### Analysis Method

First, I checked what is an average walking speed of human. I found out that average speed of men is **5.72+/-0.69 km/h** while that of women is **5.54+/-0.64 km/h** <sup>[1](#myfootnote1)</sup>. This speed was for an adult who walks for an exercise. I assume casual walking speed will be slower. Also to make calculations simpler, I used **5 km/h**. I decided to use time points as 10, 20, 30 and 60 min. Now plan was to download map of desired place and 4.5 km <sup>[2](#myfootnote2)</sup> around it. Then I will try to trace all possible combinations of locations where one can reach in given time period. Fortunately, `OSMnx` does all the magic for me. You can check out how it performs this analysis at their [blog post](http://geoffboeing.com/2016/11/osmnx-python-street-networks/). You can check my simple `python` [script](https://gist.github.com/rohitsuratekar/1bd089668168b2343446cf27c91954a3) to perform this analysis. 

### Farthest distance from NCBS

First, I checked how far can I go walking from [NCBS](http://ncbs.res.in/).

|![Fig 1: Farthest distance from NCBS](/assets/article_images/2018-07-15-longest-distance/ncbs.png "NCBS")|
|:--:|
|Fig 1: Farthest distance one can reach by walking from NCBS with any possible route <sup>[4](#myfootnote4)</sup>. Only walking routes are considered in this analysis. We are assuming constant speed through out our walk. Different color represents different travel time with lighter representing farthest area.|


To validate if this analysis is providing good enough information, I cross checked few areas around NCBS which I have personaly visited and timed. As seen in Fig 1, towards South, I can reach Sahakara Nagar in 20 min. Towards North-West, I can reach Tindlu Circle in 30 min. Towards East, I can hit Bellary road in 30 min. These all timings are more or less accurate!

### Well connected institutes

Now we can use such map to check if institute is well connected to rest of the city. In this simplest analysis we will assume farthest distance one was travel is direct proxy for well connection to the city <sup>[3](#myfootnote3)</sup>. I will add only representative institutes. I have tried to include institute area which has some kind of variation. You can check out your own by using python script from [here](https://gist.github.com/rohitsuratekar/1bd089668168b2343446cf27c91954a3). 

|![Fig 2: Farthest walking distance from IISc and TIFR](/assets/article_images/2018-07-15-longest-distance/inst1.png "IISc and TIFR")|
|:--:|
|Fig 2: Farthest walking distance from IISc and TIFR <sup>[4](#myfootnote4)</sup>. Here blank area around TIFR is the Arabian Sea. Because of highly interconnected roads around IISc, we can see symetrical spread of farthest areas. |

|![Fig 3: Farthest walking distance from IIT Bombay and IIT Kharagpur](/assets/article_images/2018-07-15-longest-distance/inst2.png "IIT B and IIT KGP")|
|:--:|
|Fig 3: Farthest walking distance from IIT Bombay and IIT Kharagpur <sup>[4](#myfootnote4)</sup>. |

|![Fig 4: Farthest walking distance from IIT Delhi and IIT Madras](/assets/article_images/2018-07-15-longest-distance/inst3.png "IIT D and IIT M")|
|:--:|
|Fig 4: Farthest walking distance from IIT Delhi and IIT Madras <sup>[4](#myfootnote4)</sup>|

### References and Notes

1. <a name="myfootnote1"> </a> Parise C, Sternfeld B, Samuels S, Tager IB. Brisk walking speed in older adults who walk for exercise. J Am Geriatr Soc. 2004 Mar;52(3):411-6. PubMed PMID: 14962157
2. <a name="myfootnote2"> </a>I know speed is 5 km/hr so it is highly unlikely that route tracking is going to go hit my map bounds which is at 4.5 km. I selected such a low cut off for better visualization.
3. <a name="myfootnote3"> </a> As student will have good access to market and other required facilities. In reality this is not accurate but good enough for some simple analysis.
4. <a name="myfootnote4"> </a>Please note that even though all maps are named with institute names, they are actually extracted by selecting 4.5 km area surrounding random point inside institute area.  

Code used in the above analysis can be found [here](https://gist.github.com/rohitsuratekar/1bd089668168b2343446cf27c91954a3).

*(Header image is downloaded from Pixabay.com under CC0-license)*