---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Spurious Correlations - Indian Premier League Edition
categories: correlation
tags: statistics, visualization
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar
header_image: 2020-12-13-spurious-correlations/graph.jpg
assets: /assets/article_images/2020-12-13-spurious-correlations
---

When we are analysing big data, many times we encounter weird correlations. There is a scientific name for it - **Spurious Relationship** or **Spurious Correlation** <sup>[1](#ref1)</sup>. You may have heard about the [book](https://www.tylervigen.com/spurious-correlations)
by mathematician Tyler Vigen which talks about this phenomenon. It is no surprise that I often encounter them in my daily data analysis tasks. Most of the time I ignore it and move on to the next analysis. However, the case I am going to talk about has so many such relations that I decided to write a full blog article for it. In the end, I will try to reason why we are getting so many correlations in this case.

## Indian Premier League

Indian Premier League ([IPL](https://en.wikipedia.org/wiki/Indian_Premier_League)) is one of the most famous [T20](https://en.wikipedia.org/wiki/Twenty20)
the tournament in the world. It was the first sporting event which was broadcast live on YouTube <sup>[2](#ref2)</sup>. Since 2008,
there have been 13 seasons of IPL generating a tremendous amount of data and feast for data-scientists :) I had my eye on IPL data
for a long time and finally got a chance to play around with that data. While playing around with data, I realize there are these weird correlations keep popping up. Hence, I decided to focus on finding these 'spurious' correlations than doing any specific analysis task.

### The Data

There are many IPL datasets available on the internet. I used the one on [Kaggle](https://www.kaggle.com/patrickb1912/ipl-complete-dataset-20082020) and 
curated by Prateek Bhardwaj. I think the original data was scraped from [CrickInfo](https://www.espncricinfo.com/). Data contains statistics 
of **816** matches played between 2008 - 2020. Out of which 5 matches were tied. I performed data cleaning by converting team names to their location. 
It was important as few of the teams had changed their names over the IPL seasons. The outcome of every match is shown in Fig [1](#fig1).

|<a name="fig1"></a> <img src="{{page.assets}}/ipl.png" width="80%"/>|
|:--:|
| Fig 1: Outcome of every match in IPL (2008-2020). Tie matches are not shown.|


## Spurious Correlations

I tested the correlation between few variables related to the cricket match and a total number of matches won by the given team. 
Few selected ones with a good statistical correlation are shown below. I fitted line 
to these correlations and tested **R<sup>2</sup>** value for each correlation. Closer the value of R<sup>2</sup> to 1, better 
is the correlation. 

Let us start with the toss :)

|<a name="fig2"></a> <img src="{{page.assets}}/toss.png" width="80%"/>|
|:--:|
| Fig 2: Correlation between no of times team won the match vs no of time they won the toss|

Now team has to take a decision weather to bat first or field.

|<a name="fig3"></a> <img src="{{page.assets}}/bat.png" width="80%"/>|
|:--:|
| Fig 3: Correlation between no of times team won the match vs no of times they decided to bat first after winning the toss|

What if they decoded to field first instead bat?

|<a name="fig4"></a> <img src="{{page.assets}}/field.png" width="80%"/>|
|:--:|
| Fig 4: Correlation between no of times team won the match vs no of times they decided to field first after winning the toss|

Is it depend on number of matches team has played? Why not :)

|<a name="fig5"></a> <img src="{{page.assets}}/matches.png" width="80%"/>|
|:--:|
| Fig 5: Correlation between no of times team won the match vs number of matches played by that team.|

Maybe weather is affecting these results? Well, I did not have time to extract historic weather data, but 
I did next best thing. Looked at in which city match was played.

|<a name="fig6"></a> <img src="{{page.assets}}/city.png" width="80%"/>|
|:--:|
| Fig 6: Correlation between no of times team won the match on their home ground vs number of team has played the match on their home ground.|

## What is happening?

If you are a keen observer, it is pretty obvious that all these correlations might be due to two clusters of teams, 
Pune, Gujarat, Kochi (which were active for only few IPL seasons) vs rest. You are on the right track. See Fig [7]($fig), 
after removing these three teams, R<sup>2</sup> value dropped drastically when I removed those teams from the 
correlation analysis. I observed a similar trend in all other plots. 

|<a name="fig7"></a> <img src="{{page.assets}}/city_removed.png" width="80%"/>|
|:--:|
| Fig 7: Correlation between no of times team won the match on their home ground vs number of team has played the match on their home ground. After removing Pune, Gujarat and Kochi|

These three team were clear outliers in our correlation analysis. How can we prove this in more systematic way? I just aggregated data
shown in all the plots above and then performed PCA. I was happy with the results. As expected, we can clearly see two clusters 
of team (see Fig [8](#fig8)). It suggests that 95% of variation in our data can be explained by just one variable (see x-axis of Fig 
[8](#fig8)).

|<a name="fig8"></a> <img src="{{page.assets}}/pca.png" width="80%"/>|
|:--:|
| Fig 8: PCA plot of all the data shown in this article.|

Another way to perform proper correlation is by normalizing each team with their number of matches played. You can see the 
correlation vanishes (as seen by lower R<sup>2</sup> value) in Fig [9](#fig9) in contrast to Fig [2](#fig2).

|<a name="fig9"></a> <img src="{{page.assets}}/toss_norm.png" width="80%"/>|
|:--:|
| Fig 9:  Correlation between no of times team won the match vs winning toss. Data is normalized to number of matches played by the respective team.|

There are still more variables in this dataset which can provide more 'spurious' correlations. Maybe next time:)


## References
1. <a name="ref1"></a> Spurious relationship - [Wikipedia](https://en.wikipedia.org/wiki/Spurious_relationship) [Accessed on 12 Dec 2020]
2. <a name="ref2"></a> IPL matches to be broadcast live on Youtube - [ESPNCricInfo](https://www.espncricinfo.com/story/ipl-matches-to-be-broadcast-live-on-youtube-445173) [Accessed on 12 Dec 2020]

Full code can be found [here](https://github.com/WeirdData/RandomAnalysis) and [here](https://gist.github.com/rohitsuratekar/7f774e60fa40409e67ae713b560b1b39).

_All web links provided in this article are accessed on 13 Dec 2020 (if not mentioned otherwise)_

*(Header image by <a href="https://pixabay.com/users/geralt-9301">Gerd Altmann</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*


