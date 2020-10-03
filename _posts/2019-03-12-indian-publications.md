---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  Academic Publications in India
date:   2019-03-12 09:00:00
categories: visualization
tags: india, visualization, academic
author_bio: Author is a computational biologist at IIMCB, Warsaw.
author_twitter: rohitsuratekar
header_image: 2019-03-12-indian-publications/publish.jpg
---

A few days ago, India celebrated its National Science Day which marks the scientific achievement of Sir C. V. Raman and also inspires many Indians to pursue science. In 1996, government budget for research and development was 0.65% of GDP while same was decreased to 0.65% of GDP in 2015 <sup>[1](#ref1)</sup>. For year 2018-19, even after financial boost, it was around 0.8% of GDP <sup>[2](#ref2)</sup>. Government is trying to boost research by providing incentives like a financial reward for the publication. Although such schemes have received mixed responses from the Indian scientific community <sup>[4](#ref4), [5](#ref5)</sup>, there is no proper data regarding scientific advances in India. Hence I decided to check it by myself.

|![Fig 1: budget](/assets/article_images/2019-03-12-indian-publications/budget_data.png "Budget")|
|:--:|
|Fig 1: Research and Development expenditure of India <sup>[1](#ref1), [3](#ref3)</sup>. |

### Data and Limitations
There are multiple factors like budget allocation, research infrastructure, external funding etc which can give you an idea about the scientific environment of the country. I decided to look at most simple factor i.e. peer-reviewed publication records. Another reason to look at this factor is due to the availability and quality of data. The best place to look at such dataset is [PubMed](https://www.ncbi.nlm.nih.gov/pubmed). I decided to look at only PubMed indexed publications <sup>[6](#ref6)</sup>. The first hurdle I faced while retrieving this data was to filter it based on publications from a specific country. Unfortunately, such filter or meta-data was not available at PubMed. One of the ways to overcome this problem was to retrieve affiliations from all the authors and check the affiliation of the corresponding author. However, it will need a huge amount of storage space, internet bandwidth and computational power. As I had previously worked with such PubMed database, I know there is a further problem in getting proper affiliations and corresponding author details. Finally, I used a shortcut which will be enough to get an idea about my question. I decided to use PubMed advance search with [affiliation qualifier](https://www.nlm.nih.gov/bsd/disted/pubmedtutorial/020_835.html). For this analysis, I used the following search query

>india[ad]

Then I exported all the results in `.csv` format (send to > file > CSV) for further analysis. Few limitations of this approach are listed below 
1. Journals which don't report proper affiliations will not be available 
2. Any affiliation which has characters 'india' will be picked up (like papers who has the affiliation of Indiana University, Bloomington) 
3. Papers which are published from other countries but have an author with Indian affiliation will be picked up by the search <sup>[7](#ref7)</sup>

Nonetheless, I decided to use this as a preliminary analysis for understanding the original question. This dataset will at least provide us trends <sup>[7](#ref7)</sup>. All the code used in this analysis can be found on [GitHub](https://github.com/WeirdData/PubMedAffiliations) repository. 

### Basic Statistics

In this dataset, there are total **421990** papers from 7332 distinct journals. Oldest <sup>[8](#ref8)</sup> available paper which has Indian affiliation was from [1793](https://www.ncbi.nlm.nih.gov/pubmed/29106209) by Boag W in [Medical Facts and Observations](https://www.ncbi.nlm.nih.gov/pmc/journals/2819/) !! Just on the side note, I got curious and looked at the oldest PubMed entry. It is from [1 Jan 1781](https://www.ncbi.nlm.nih.gov/pubmed/29139653) from *The London medical journal*. I checked which were journals where Indian researchers have published the most between 11 March 2019 to 1793. 

| Journal Name | Number of paper |
|---|:---|
| J Clin Diagn Res. | 6646 |
| PLoS One. | 4198 |
| Indian Pediatr. | 3807 |
| Indian J Exp Biol. | 3676 |

### Academic Publications

Next obvious step was to check information about the publication rate of Indian researchers. 

|![Fig 2: year wise](/assets/article_images/2019-03-12-indian-publications/year_wise.png "Year Wise")|
|:--:|
|Fig 2: Year wise publications of Indian Researchers. There was a long tail to this distribution till 1793 which is not shown here for visual clarity. |

There were **39300** papers published in 2018. If we calculate the rate of publications in the last 10 years (2008-2018) it is 31293.6 publications/year which is **375.9 % increase** compare to 1998-2008 (8325.3 publications/year). Even if the publication rate is very high, we should check where are these paper published. 

|<a name="fig3"></a>![Fig 3: Journals till 2018](/assets/article_images/2019-03-12-indian-publications/journals1.png "Journals till 2018")|
|:--:|
|Fig 3: Top 3 journals where Indian researchers published the most in given year (2000-2018).  |

|<a name="fig4"></a>![Fig 3: Journals till 2000](/assets/article_images/2019-03-12-indian-publications/journals2.png "Journals till 2000")|
|:--:|
| Fig 4: Top 3 journals where Indian researchers published the most in given year (1980-1999).  |

Fig [3](#fig3) and [4](#fig4) shows interesting trends of publications. During the 1980s almost 60% of the papers were published in journals. One of the reasons for such a high percentage might be a lower number of total papers (total 83 in 1980). This percentage, however, has come down to less than 10% in 2018. However, this is still huge by considering a number of journals available. Sadly, I could not get data regarding statistics on the area of research. 

### Scientific Collaborations

One more aspect which will impact scientific progress is collaborations. Best way to look at it is to have data on all of the author affiliations and then check how much inter and intra-country collaboration is there. Unfortunately, this dataset does not provide information about all of the affiliations. So I checked this aspect by looking at next crudest thing, i.e. number of co-authors. There were total **1835722** authors in our datasets which suggested 4.35 authors per article. I checked how are authors per article changing over the period of time. 

|<a name="fig5"></a>![Fig 5: Authors](/assets/article_images/2019-03-12-indian-publications/author_wise.png "Authors")|
|:--:|
| Fig 5: Authors per article over the period of time.  |

As apparent from Fig [5](#fig5), the number of authors per article is increasing for the last 30 years. This might be a sign of more collaborations. 

### Where does it fit?

Next, I checked how do these statistics look in front of other countries. I took the example of China and the USA which are one of the top countries with the most number of academic publications <sup>[9](#ref9)</sup>. In my dataset, I got more paper in the USA than China which was contradictory to the data shown in <a name="ref9">[9]</a>. This might be the outcome of our way of accessing data. This dataset will also include all the papers which have an author with USA affiliation. This may suggest more collaborations of USA. 

|<a name="fig6"></a>![Fig 6: Year Wise Others](/assets/article_images/2019-03-12-indian-publications/year_wise_other.png "Year Wise Others")|
|:--:|
| Fig 6: Number of papers published by researchers from US and China over the years.|

|<a name="fig7"></a>![Fig 7: Others](/assets/article_images/2019-03-12-indian-publications/other.png "Others")|
|:--:|
| Fig 7: Top 3 journals where US and China researchers published the most in given year.  |

Overall statistics regarding top journals for US  (total of 4379149 papers in 15489 distinct journals)  and China (total of 1356651 papers in 8146 distinct journals) is given below

| USA (number of paper) |  China (number of papers)|
|---|:---|
| PLoS One. (59832) | PLoS One. (31863) |
| J Biol Chem. (47819) | Sci Rep. (26499) |
| Proc Natl Acad Sci USA. (39167) | Chem Commun (Camb). (11551) |
| J Am Chem Soc. (26193)| Chin Med J (Engl) (11133)|

In conclusion, this analysis provides a wider perspective on Indian science. Above table, Fig [6](#fig6) and [7](#fig7) suggest that publication trends of Indian researchers were similar to that of US and China. However, properly curated data should be able to provide us with a more clear picture. 

### References and Notes
1. <a name="ref1"></a> UNESCO Institute for Statistics, [The World Bank ](https://data.worldbank.org/indicator/GB.XPD.RSDV.GD.ZS)
2. <a name="ref2"></a>T.V. Padma (2018) Indian science budget fails to impress — despite funding boost; [Nature News](https://www.nature.com/articles/d41586-018-01504-5)
3. <a name="ref3"></a> Data was not available for year 2012-2014
4. <a name="ref4"></a> Sudhakar Srivastava (2019) Let's Discuss the 'Reward for Publication' Idea Instead of Trashing It so Fast; [The Wire](https://thewire.in/the-sciences/lets-discuss-the-reward-for-publication-idea-instead-of-trashing-it-so-fast)
5. <a name="ref5"></a> Gayathri Vaidyanathan (2019) Indian payment-for-papers proposal rattles scientists; [Nature News](https://www.nature.com/articles/d41586-019-00514-1)
6. <a name="ref6"></a> This will ommit some scintific areas or journals which are not indexed by PubMed but due to limited availability of peoperly categorized data in other sources, this was unavoidable. 
7. <a name="ref7"></a> Out of 3 points raised in the limitations, only third point will impact sufficiently our results. However, if Indian researcher have contributed to the paper, I think it is safe to incude it in understanding progress of Indian science. 
8. <a name="ref8"></a> Oldest paper which has'India' in it's affiliation. I tried searching few more terms related to India but this was the oldest entry. 
9. <a name="ref9"></a> Jeff Tollefson (2018) China declared world’s largest producer of scientific articles; [Nature News](https://www.nature.com/articles/d41586-018-00927-4)



Code used in the above analysis can be found [here](https://github.com/WeirdData/PubMedAffiliations).

*(Header image by <a href="https://pixabay.com/users/felixioncool-324952/">felixioncool</a> from <a href="https://pixabay.com/">Pixabay</a>, released under CC0-license.)*