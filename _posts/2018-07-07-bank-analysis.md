---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Distribution of banks across India
date:   2018-07-07 13:34:25
categories: featured
tags: finance, banks
author_bio: Author is a computational biologist at NCBS, Bangalore.
author_twitter: rohitsuratekar
header_image: 2018-07-07-bank-analysis/bank_feature.JPG
---

I was developing one android app for storing bank account details securely. One of the fuction I was thinking of adding was to search bank [IFSC](https://en.wikipedia.org/wiki/Indian_Financial_System_Code) code. For this purpose I needed database of all Indian banks who have valid IFSC code. This code is imporant for performing [NEFT](https://en.wikipedia.org/wiki/National_Electronic_Funds_Transfer) or [RTGS](https://en.wikipedia.org/wiki/Real-time_gross_settlement) transactions. In search of such database I scaned Reserve Bank of India's (RBI) website. I did find that [database](https://m.rbi.org.in/Scripts/bs_viewcontent.aspx?Id=2009) however total size of that database was more than 10 MB. Hence it was not a good idea to embbed this data into app itself. On top of that, I need to update this database in future as RBI approves new bank branches. Finally I found good [API](https://github.com/razorpay/ifsc-api) for achieving this. After that when I was about to delete all the files related to downloaded data, my inner data scientist woke up and I decided to analyze this data further. 

### The Database

Developers at [RazorPay](https://ifsc.razorpay.com/) have compiled all of the RBI data into properly [labeled dataset](https://github.com/razorpay/ifsc/releases). This made my job even easier. I wrote simple `python` [script](https://gist.github.com/rohitsuratekar/15b3ea7a97e0f6a86aa91bb54dc9fed4) to analyze this dataset. This dataset had **141996** entries <sup>[1](#myfootnote1)</sup> on 7 July 2018 (Note: all further analysis is done on data available on 7 July 2018.). 

This itself is very big number. This suggest there are on average **3944** bank branches per state (29 states + 7 union territories). There is 1 bank branch per **9325** citizens. This is significantly higher number compare to United States. It had 80,227 FDIC-insured commercial bank in 2016 <sup>[2](#myfootnote2)</sup>. That comes down to only 1 bank per 4682  citizens. Although this statistics is 2 year old, going by average growth in US banks in past 10 years <sup>[2](#myfootnote2)</sup>, we can assume this number won't change drastically for 2018. Now we can analyze this data in little bit more details.

### Distribution by Banks
First, I checked which bank has most number of branches in India. 


|![Fig 1: Bank Wise Distribution of Indian Banks](/assets/article_images/2018-07-07-bank-analysis/bank_wise.png "Bank Wise")|
|:--:|
|Fig 1: Bank Wise Distribution of Indian Banks|

<br>
As expected, with 26222 branches all over the India, **State Bank of India** (SBI) has most number of branches (Fig 1). It is 18.46 % of all bank branches. These top 10 banks accounts for **53.10%** of total Indian bank branches. 

### Disribution by geography

Next I checked how bank branches are distributed geographically. 

|![Fig 2: State Wise Distribution of Indian Banks](/assets/article_images/2018-07-07-bank-analysis/state_wise.png "State Wise")|
|:--:|
|Fig 2: State Wise Distribution of Indian Banks|

<br>
Fig 2 shows top 10 states (or union territories) who has most number of bank branches. With 18220 branches **Maharashtra** tops this list. This is 12.83% of total bank branches in India. This is **88.25%** of total branches in India.

However this can be misleading as population of these states are very different. To understand which state has more number of bank branches per person, I used population database <sup>[3](#myfootnote3)</sup>. I just normalized number of bank branches with its population (Fig 3). 

|![Fig 3: Top 10 state who has highest number of bank branches per person.](/assets/article_images/2018-07-07-bank-analysis/pop_to_branch.png "Branch to Population Ratio")|
|:--:|
|Fig 3: Top 10 state who has highest number of bank branches per person.|

<br>
Fig 4 suggest that Chandigarh has highest number of bank branches per person (Branches: 1990, Population: 1110820 <sup>[3](#myfootnote3)</sup>). 


### More detais

Generally we presume bank branches will be concentrated in metro cities. To test this hypothesis I checked how is the city wise distribution. 

|![Fig 4: City wise distribution of bank branches.](/assets/article_images/2018-07-07-bank-analysis/city_wise.png "City Wise")|
|:--:|
|Fig 4: City wise distribution of bank branches.|

<br>

Indeed they are concentrated in metro cities. Fig 4 shows exactly same trend. As I was expecting most number of banks are present in Indias financial capital, **Mumbai** <sup>[4](#myfootnote4)</sup>, with 3132 bank branches which is 17.18% of all bank branches in Maharashtra. National capital **Delhi** <sup>[5](#myfootnote5)</sup> was on second place with 3047 bank branches. These top 10 cities have **16.18%** of India's total bank branches. Finally I checked how different banks are distributed within these top 10 cities. 

|![Fig 5: City wise distribution of branches of top banks.](/assets/article_images/2018-07-07-bank-analysis/complex.png "Complex Wise")|
|:--:|
|Fig 5: City wise distribution of branches of top banks.|

<br>


### References and Notes

1. <a name="myfootnote1"> </a> This list consists of ony NEFT enabled banks. Few state and union cooerative banks might be missing in this list. 
2. <a name="myfootnote2"></a> https://www.statista.com/statistics/193041/number-of-fdic-insured-us-commercial-bank-branches/ [Accessed on 7 July 2018]
3. <a name="myfootnote3"></a>Projected population for 2017 by UIDAI - https://uidai.gov.in/images/state_wise_aadhaar_saturation_02052017.pdf [Accessed on 7 July 2018]
4. <a name="myfootnote4"> </a> Excluding "Greater Bombay" area. I have no idea how this was classified. I did not cross check regarding this.
5. <a name="myfootnote5"> </a> Excluding "New Delhi" area.


Code used in the above analysis can be found [here](https://gist.github.com/rohitsuratekar/15b3ea7a97e0f6a86aa91bb54dc9fed4).

*(Header image is captured by Rohit Suratekar in Poland Warsaw)*