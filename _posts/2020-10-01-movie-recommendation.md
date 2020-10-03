---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Yet Another Movie Recommender System
categories: analysis 
tags: python, machine-learning, neural-networks
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar
header_image: 2020-10-01-movie-recommendation/reel.jpg
assets: /assets/article_images/2020-10-01-movie-recommendation
---

In this internet age, you must have encountered at least one or another form of Machine Learning (ML) in your daily use. It can be simple [Captcha](https://en.wikipedia.org/wiki/CAPTCHA) , [Language Translation](https://en.wikipedia.org/wiki/Neural_machine_translation) or all the [ads](https://en.wikipedia.org/wiki/Digital_display_advertising) you see on various websites. ML has invaded our lives whether you believe it or not. This blog post is about a special type of ML usage called ‘[recommender system](https://en.wikipedia.org/wiki/Recommender_system)’ which has been heavily used in providing recommendations to the user in various context. Most popular examples of this system are movie recommendation in Netflix<sup>[1](#ref1)</sup>, item listing in Amazon <sup>[2](#ref2)</sup>, next song in Spotify<sup>[3](#ref3)</sup>, explore photos in Instagram<sup>[4](#ref4)</sup> and the list goes on. So it is not surprising that many of ML courses use a recommender system to explain basic ML concepts. Here I will explore one such recommender system using a very famous [MovieLens](https://movielens.org/) database. I will make a simple recommender system which will show me movie recommendations based on my history.

## The Strategy
This database is used by literally thousands of people around the world. They [all](https://duckduckgo.com/?q=movielens+recommender+system&t=ffab&ia=web) have created a recommender system from mostly similar techniques. In this blog post, I will use two distinct scenarios where I can implement these concepts (See Fig [1](#fig1)).

|<a name="fig1"></a> <img src="{{page.assets}}/category.png" width="70%"/>|
|:--:|
| Fig 1: Two different scenarios used in this analysis.|

Following details shows the overview of the MovieLens database (as of 1O Oct 2020),

|Description|Value|
|--|--|
|Total Movies| 27022|
|Total Categories| 19|
|Movies Year| 1894 to 2015|
|Total Ratings| 20000263|
|Total Users| 138493|

## Content-Based Filtering

In this method, we will find ‘similar movies’. One can provide any movie name as an input and we will show similar movies. Our code will gather information about this movie by looking at its genres and tags given by other users. We will then generate a matrix which will have both our tags and genres. This entire process is shown in Fig [2](#fig2). Code used in achieving this can be found [here](https://github.com/WeirdData/MovieLensAnalysis).

 |<a name="fig2"></a> <img src="{{page.assets}}/content_based.png" width="70%"/>|
 |:--:|
 | Fig 2: Steps in content-based filtering method.|


Our code will generate the `cosine-similarity` <sup>[5](#ref5)</sup> matrix between every movie based on each movies tags and genres. When user input’s their movie name, we will just search in our `cosine-similarity` matrix and get a list of movies which are most similar to each other. Besides, we will reorder them based on their ranking. Another simple tweak I did was reduced the weight of genre in calculating final distance. It improved our similar movie predictions. Following are some of the results from this method

|Input Movie | Similar Movies (top 3, in order) |
| -- | -- |
| Spider-Man | Spider-Man 2, Spider-Man 3, X-Men |
| The Shawshank Redemption | The Godfather, The Green Mile, Mystic River |
| Toy Story | Toy Story 2, Finding Nemo, Monsters, Inc. |
| The Grudge | The Haunting , The Ring, The Amityville Horror |
| The Wolf of Wall Street | Mr. Nice, Spun, Trainspotting |
| The Notebook | Blue Valentine, Titanic, The Vow |
| Memento | Se7en, The Usual Suspects, The Game |

I must say, these are pretty accurate predictions. In most of the results, we got movies similar to our input movie. This suggests tagging done by users is pretty good and our cosine-similarity is working as expected. In future, we can expand by taking multiple movies as input and predicting movie similar to those.

### Advice for large data

The generation of the `cosine-similarity` matrix for a huge number of movies is very time consuming and computationally heavy. Be careful about your system configuration. You will need huge RAM depending on the number of movies and ratings you are using. It is a good idea to save the matrix on the disk and access it for our future predictions. I used the _HDF5_ file to save the matrix and used it for future predictions.

## User-Based Filtering

Content-based filtering provided good recommendations given a specific movie. However, the most important limitation of that method is that we will never get a prediction for the movie from some another genre or completely different movie which user might like. This is where _user-based filtering_ will help us. In this method, we will train the neural network which will predict movie rating based on the rating history of any user.  With this method, the user will provide names of movies and their ratings. Our model will predict movies which the user might like. This strategy is shown in Fig [3](#fig3).

 |<a name="fig3"></a> <img src="{{page.assets}}/user_based.png" width="90%"/>|
 |:--:|
 | Fig 3: Steps in user-based filtering method.|

### The Neural Network

I won’t go into details about how the neural network was designed and what one should think about. There are plenty of blogs to tackle any aspect of this process including how to improve accuracy, speed and computation time. I used `keras` functional programming to build the model (Fig [4](#fig4)). In this model, I used `Embedding` Layers to represent big input matrix in lower dimensions. I projected all input onto 16 dimensions. This is an arbitrary number, there is no logic to this. I wanted to use more dimensions but given limited computational power, I stuck to 16. Later on, I just combined these dimensions by concatenating them. Few of the blogs online have suggested using DOT product, however, in my experience, in this case, contcatenation was better as I wanted a representation of both users and movies. Next, I used a `Dense` layers which acts like hidden layer with 32 neurons and the final output layer with 1 neuron which should give me value between 0-1. 

|<a name="fig4"></a> <img src="{{page.assets}}/model.png" width="90%"/>|
 |:--:|
 | Fig 4: The Neural Network generated in `keras`|

I have normalized my rating such that 1 will represent 5 and 0 will represent 0. Other parameters like an epoch, loss function, batch size etc are used randomly. One should use multiple such parameters to fine-tune their model. Model accuracy history across multiple epochs is shown in Fig [5](#fig5). We got pretty good accuracy in pour model as our final `Loss` was around 0.024. Even validation loss was minimal and did not show overfitting. 

|<a name="fig5"></a> <img src="{{page.assets}}/fitting.png"/>|
 |:--:|
 | Fig 5: Loss curv for model shown in Fig [4](#fig4). X-axis represents time (here, epochs) while Y-axis represents Loss. |

### Cold-Start Problem for the Neural Network

Cold-start problem is a pretty old and consistent problem for any recommender system. Our system is no exception. Our neural network is trained with `user-id` and `movie-id` pair (See Fig [3](#fig3) and [4](#fig4)). So to get any prediction from our trained model, we need to provide `user-id`. However, as we are predicting movie ratings for a completely new user, we will not have `user-id` to provide input to our model. 

To circumvent this issue, I decided to search for the most similar existing user from our database. This can be achieved by looking at `cosine-similarity` between the movie-rating matrix of the new user and existing users. From this, we can get a user who closely resembles the new user and we can use its recommendations for our new user. In reality, such a recommender system usually go for general recommendations based on user location, country, season etc. And later they will include new users to their revised model as a new user will keep watching more movies.

### Predictions from the Neural Network 

Following are some of the predictions from this model.

| Input Movies [Input Ratings] | Top 5 Recommendations [Score]| 
| -- | -- |
| The Godfather [4.5] <br/> The Godfather: Part III [4] | The Shawshank Redemption [0.879] <br/> The Usual Suspects [0.866] <br/> Fight Club [0.857]<br/>The Departed [0.836] <br/> American History X [0.832] |
| Batman Begins [4.5] <br/> Batman: Assault on Arkham [5] <br/> The Avengers [3.5] <br/> Iron Man 3 [4] | The Sound of Music [0.926] <br/> Anne of Green Gables [0.926] <br/> Pride and Prejudice [0.925] <br/> White Christmas [0.923] <br/> Babylon 5: In the Beginning [0.919] |
| Batman Begins [1] <br/> Batman: Assault on Arkham [1] <br/> The Avengers [1]  <br/> Iron Man 3 [1] | The Dark Knight [0.973] <br/> The Usual Suspects [0.952] <br/> The Shawshank Redemption [0.948] <br/> Inception [0.94] <br/> The Matrix [0.939] |
| The Haunting [3.5] <br/> The Ring [4] <br/> The Grudge [4.5] <br/> Iron Man 3 [1] | Ravenous [1.005] <br/> The Devil's Rejects [0.983] <br/> From Dusk Till Dawn [0.976] <br/> Saw II [0.969] <br/> Cruel Intentions [0.967] |
| Toy Story [4.5] <br/> Toy Story 2 [4] <br/> Finding Nemo [3] <br/> Monsters, Inc. [3.5] | The Civil War [1.015] <br/> Schindler's List [1.003] <br/> The Shawshank Redemption [0.996] <br/> Band of Brothers [0.994] <br/> Wallace & Gromit: The Wrong Trousers [0.985] |

We got pretty interesting predictions. I deliberately used multiple movies and changed their rating to see how my predictions will change. There are intriguing predictions like “The Sound of Music” was recommended where the user had given all Marvel action movies. I think this has happened because multiple users have rated high for both action and romantic movies. This is the biggest advantage of user-based filtering as we would have never received this recommendation in content-based filtering. There are some clear issues in this recommendation. Like when I lowered Batman movie ratings, then I received more appropriate predictions than when those ratings were high. Input with all animated kids movies received war movie recommendations. Next section will talk about what can be the issue and how one may overcome it. 

### Further improvements

One area of improvement which many other models use but I have not used here is to add ‘user-bias’ to our neural network. Many users rate all movies with high rating or low rating. It creates the bias towards ratings. We can potentially correct for such bias by multiplying user bias in our neural network. Current model is biased towards favorite movies and do not consider hated movies properly. One can add this information in normalizing ratings. Another important point which I did not address while building the model is selecting correct user from multiple of similar users (for cold-start problem). This is little complicated to address but careful selection of proper distance matrix can overcome this. 

In addition to above, there are multiple things which we can do to further improve these predictions like adding more data regarding movies (like reviews, cast and crew information etc) or user (like location, country etc). We can also use mixed strategy where we can use distance matrix from various parameters and train our neural network. One can also add user-interaction information (like which movie user select, watches trailer etc). If you are part of multi-billion dollar company, you can easily get such data along with many more additional parameters :)


_Pro Tip_: I was limited by computational power. Many of my big models were just too complicated for my 4-year-old laptop. To get a little bit better computational power, I used Kaggle Notebooks. Few of the testing models were trained on their notebooks. So thank you Kaggle :)

Full code can be found [here](https://github.com/WeirdData/MovieLensAnalysis). 

_All web links provided in this article are accessed on 1 Oct 2020 (if not mentioned otherwise)_


## References
1. <a name="ref1"></a> How Netflix’s Recommendations System works - https://help.netflix.com/en/node/100639 [accessed on 1 Oct 2020]
2. <a name="ref2"></a> Real-time personalization and recommendation - https://aws.amazon.com/personalize/ [accessed on 1 Oct 2020]
3. <a name="ref3"></a> Guidelines for surfacing Categorized Content Recommendations in your mobile app - https://developer.spotify.com/use-cases/mobile-apps/content-recommendations/ [accessed on 1 Oct 2020]
4. <a name="ref4"></a> Powered by AI: Instagram’s Explore recommender system - https://ai.facebook.com/blog/powered-by-ai-instagrams-explore-recommender-system/ [accessed on 1 Oct 2020]
5. <a name="ref5"></a> Cosine similarity - https://en.wikipedia.org/wiki/Cosine_similarity [accessed on 1 Oct 2020]


*(Header image by <a href="https://pixabay.com/photos/movie-reel-projector-film-cinema-918655/">free-photos-242387</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*
