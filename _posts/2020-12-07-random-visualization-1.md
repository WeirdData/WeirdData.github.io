---
author: Rohit Suratekar 
avatar: rohit_suratekar.jpg 
layout: post 
title:  Visualizations Collection 2020 
categories: analysis
tags: python, visualization
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar 
header_image: 2020-12-07-random-visualizations-1/graph-biz.jpg 
assets: /assets/article_images/2020-12-07-random-visualizations-1
---

<p style='text-align: justify;'>
For most of the people, the year 2020 was a disaster in many aspects, but it turned out pretty good 
for my data analysis streaks. I did a lot of data analysis on many data-sets ranging from Running Records 
to World's Tea Export. Some received positive response while on others negative. Nonetheless, 
I enjoyed each one of them. They were all scattered throughout many social media posts over the year. 
Here I am trying to create a collection of selected visualizations. I hope you enjoy them.
</p>


|<img src="{{page.assets}}/job.png" width="80%"/>|
|:--:|
| **Job Hunting during the pandemic** : This Sankey plot is derived from the data collected during the career transition of my wife in 2020. It shows how stressful was to find any job during the pandemic even for highly skilled person<sup>[1](#ref1)</sup>.|

|<img src="{{page.assets}}/running.png" width="100%"/>|
|:--:|
|**Top 2000 world records of 100m running** : You can clearly see huge difference between male runners and female runners. In addition, it shows how world records were increased heavily in recent years compared to past<sup>[2](#ref2)</sup>|

|<img src="{{page.assets}}/bbt.png" width="100%"/>|
|:--:|
|**Number of times country is referenced in the Big Bang Theory** : Big Bang Theory is one of my favorite sitcom. I analysed its subtitles from each episode. After little NLP analysis, I landed up on this <sup>[3](#ref3)</sup>. |

|<img src="{{page.assets}}/books.png" width="80%"/>|
|:--:|
|**Top 20 word stems appeared in the book titles** : Before naming your book, take a look at this plot <sup>[4](#ref4)</sup> :)|

|<img src="{{page.assets}}/tea.png" width="100%"/>|
|:--:|
|**71% of world's total tea export is done by these countries** : I was surprised by Germany and Poland in this list. However, I leaned that they are also in top countries who import tea. After reading further about this, I learned very interesting trading practices. Many countries import raw tea and export flavoured tea!<sup>[5](#ref5)</sup> |

|<img src="{{page.assets}}/friends.png" width="80%"/>|
|:--:|
|**Relationships of FRIENDS characters** : FRIENDS is probably one of the best sitcom I have ever watched. Being huge fan of this TV Show, I did little data analysis on it as well. It was interesting to see Joe at the bottom this chart given how his persona was created in the original serial <sup>[6](#ref6)</sup>.|

|<img src="{{page.assets}}/covid.png" width="80%"/>|
|:--:|
|**Top Exporters and Importers of COVID-19 essentials** : My data-analysis streak won't complete unless I did at least some analysis on COVID-19<sup>[7](#ref7)</sup>.|

|<img src="{{page.assets}}/nobel.png" width="100%"/>|
|:--:|
|**Nobel Laureate in Medicine : where they were born and where they worked** : This analysis was inspired from [anther](https://www.chemistryworld.com/nobel-prize/the-data-behind-the-nobel-prizes/4010453.article) very interesting analysis on Nobel Prizes in Chemistry<sup>[8](#ref8)</sup>.|

|<img src="{{page.assets}}/nature.png" width="80%"/>|
|:--:|
|**Nature's recent 'free' article fees in the context of yearly salaries of Indian researchers** : I posted this graph on [twitter](https://twitter.com/rohitsuratekar/status/1331331461111304199?s=20) when Nature Publishing Group released their ridiculous fees for Open Access article<sup>[9](#ref9)</sup>.|


|<video width="80%" controls> <source src="{{page.assets}}/rainfall.mp4" type="video/mp4"></video>|
|:--:|
|**115 Years of rainfall in Meteorological Subdivisions of India** : This very rich data-set clearly shows how Indian Monsoon enters and retracts<sup>[10](#ref10)</sup>|


There were many other memes, illustrations and data analysis I performed in 2020. Follow me on [Twitter](https://twitter.com/rohitsuratekar), 
[Reddit](https://www.reddit.com/user/rohitsuratekar) or [LinkedIn](https://www.linkedin.com/in/rohitsuratekar/) where 
usually I post my data-analysis related work!

## References, Tools and Code
1. <a name="ref1"></a> Data: Personal data, Tools: [http://www.sankeymatic.com/build/](http://www.sankeymatic.com/build/)
2. <a name="ref2"></a> Data: [Running Records](https://www.alltime-athletics.com/) and [Animals](https://www.speedofanimals.com/), Code: [GitHub](https://github.com/WeirdData/GeoAnalysis/blob/master/world/running.py)
3. <a name="ref3"></a> Data: Subtitles from each episode, Code: [GitHub](https://github.com/WeirdData/GeoAnalysis/blob/master/world/bbt.py)
4. <a name="ref4"></a> Data: [Book Names](https://www.kaggle.com/jealousleopard/goodreadsbooks), Code: [Gist](https://gist.github.com/rohitsuratekar/84f109aa4e846a6fac43339a7f3e18f0)
5. <a name="ref5"></a> Data: [Tea Exporters](http://www.worldstopexports.com/tea-exports-by-country/), Code: [GitHub](https://github.com/WeirdData/GeoAnalysis/blob/master/world/tea.py)
6. <a name="ref6"></a> Data: [Friends Relationships](https://friends.fandom.com/wiki/Relationships), Code: [Gist](https://gist.github.com/rohitsuratekar/c3158797bb83198abaed91ea29f7d2c1)
7. <a name="ref7"></a> Data: [Covid Exporters](https://wits.worldbank.org/), Tools: `python3` and Gimp
8. <a name="ref8"></a> Data: [Nobel Prizes](https://www.kaggle.com/nobelfoundation/nobel-laureates), Code: [Gist](https://gist.github.com/rohitsuratekar/c546c0c31b9481b309e49e87c9a27b7e)
9. <a name="ref9"></a> Data: From various Indian Government Websites, Code: [Gist](https://gist.github.com/rohitsuratekar/9131d632c176f7aef65176d971f33118)
10. <a name="ref10"></a> Data: [Indian Rainfall](https://data.gov.in/catalog/rainfall-india), Code: [GitHub](https://github.com/WeirdData/GeoAnalysis/blob/master/india/rainfall.py)


*(Header image by <a href="https://pixabay.com/users/stocksnap-894430">StockSnap</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*