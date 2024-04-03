+++
date = "2024-03-23T19:41:01+05:30"
title = "Text Mining: Pitchfork Reviews"
draft = false
image = "img/portfolio/pitchfork_wordcloud.png"
showonlyimage = false
weight = 1
+++

Used sentiment analysis, latent dirichlet allocation, cluster analysis, predictive modeling, and other text mining methodologies to understand the relationship between the content of an album review and the album's ranking on Pitchfork.

<!--more-->

---

> The code for this project can be found in [this GitHub repository](https://github.com/acwilb/Pitchfork-Review-Text-Mining/). All data cleaning, analysis, and visualizations were done in R.

---

#### Introduction

Pitchfork is an online music publication that publishes album reviews for artists across all genres of music. The website was founded in 1996 and originally covered alternative and independent music, eventually expanding to cover more genres and reach a larger audience.

Pitchfork is widely considered to be the “Most Trusted Voice in Music”, and many music fans turn to the platform to determine whether or not new albums are worth a listen. The motivation behind this project was to understand the relationship between the content of an album review and the album's ranking on Pitchfork.

#### The Data

The dataset used in this project comes from the Kaggle dataset “Pitchfork Reviews: Music Critiques Over the Years”, collected by user timstafford on Kaggle and can be found [here](https://www.kaggle.com/datasets/timstafford/pitchfork-reviews).

Each album has been archived by artist name(s), album name, album score (rated on a scale from 0 to 10), the album’s release year, the author of the review, the album’s genre(s), record label, the date the review was published, the summary of the album review, the full album review, and whether the album was awarded “Best New Reissue” or “Best New Music”. The main variables of interest were the **album scores**, the **album genres**, and the **album reviews**.

#### Exploratory Data Analysis

Examining the overall distribution of ratings on the website tells us whether the distribution of album ratings is skewed in a particular direction, which could indicate bias in Pitchfork’s criteria when rating albums.

![Distribution of Album Scores](/img/pitchfork/pitchfork_eda_1.png)

Based on the distribution of the album scores, we see that the median score is 7.3, with most reviews scoring between 6 and 8. This left-skewed distribution of scores indicates that Pitchfork is selective when it comes to the albums they choose to publish reviews on and that they generally are not too harsh in their ratings of albums. Authors on Pitchfork may select the albums they review based on whether an album or artist is generating buzz among the music community or whether an artist has already established a strong presence within the community.

Another indication of possible bias in Pitchfork's reviews may be uncovered through examining how ratings vary across different genres. Significant differences in scores between genres could indicate whether Pitchfork reviews tend to be biased toward any particular genre.

![Distibution of Median per Genre](/img/pitchfork/pitchfork_eda_2.png)

From the distribution of median scores for each genre, we see that the median score of each genre falls between 7 and 8. The median was measured in order to ensure that any outlier album ratings would not affect these findings.

The genres with the highest median album ratings were Global, Jazz, and Experimental. Since the median scores are similar across all genres, this indicates that Pitchfork reviews favor no particular genre. It should be noted that, for the top 3 genres with the highest median scores, these genres tended to have fewer reviews than those with lower median scores, such as Pop, Rap, and Rock. Since the frequency of reviews are more heavily skewed toward these genres, we can infer that there is a larger range of albums to review and therefore a wider range of scores than for Global, Jazz, and Experimental.

#### Frequent Terms

In order to get a better understanding of the text data, we begin by using R's [tidytext](https://cran.r-project.org/web/packages/tidytext/index.html) package to convert the column with text (**Album Review**) into a tidy text format, tokenizing the terms, and removing stop words from the text.

After preprocessing the text, we use R's [wordcloud2](https://cran.r-project.org/web/packages/wordcloud2/index.html) package to generate the following word cloud, where the most frequently used terms are larger than less frequently used terms.

![Pitchfork Review Word Cloud](/img/pitchfork/pitchfork_wordcloud.png)

Based on the largest terms in the word cloud, we see that the most frequently used terms are musical, particularly relating to genre. In addition to musical terms such as “guitar”, “production”, and “beats”, there are many words that are used to describe the emotions an album can evoke in the listener, with terms such as “feels”, “moments”, and “sense.”

![Pitchfork Most Frequent Bigrams](/img/pitchfork/pitchfork_freq_bigrams.png)

Looking closer at the most characteristic terms, we see that the two terms that appear together the most (bigrams), after cleaning the text data and removing stop words, are “hip hop”, which makes sense given that many reviews are given to albums of the Hip Hop genre. The second most frequent bigrams are “title track”, which is often used to kick off an album’s review when describing the various songs on an album. A majority of the most frequent bigrams are subgenre descriptors such as “singer-songwriter”, “post-punk”, and “indie rock”, that are often used to describe the album in more detail than their main categorized genre.

![Bigram Network](/img/pitchfork/pitchfork_bigram_network.png)

Visualizing a network of the grammar of these bigrams as a Markov Chain allows us to understand the core terms that connect each review with their album's rating.

#### Sentiment Analysis

To perform sentiment analysis on our data set, we convert the text data into a tidy format, extract sentiments from R's [Bing sentiment lexicon](https://search.r-project.org/CRAN/refmans/textdata/html/lexicon_bing.html) -- which categorizes words into positive or negative values, and follow the procedure of tokenizing the tidy text data into words and performing an inner join with the Bing sentiments.

![Most Frequent Positive Terms](/img/pitchfork/pitchfork_pos_terms.png)

From the distribution of the top ten most frequent terms asociated with positive reviews, we see that the word “like” is used far more frequently than any of the others. In the context of the album reviews, the word “like” was used to describe what the author liked about each album, and was additionally used to compare elements of the albums to other musical elements that are often characteristic of specific genres. Since Pitchfork writes specifically for the online community of music fans, it is very common for album reviews to contain sections that are very comparative in nature. The word “like” is often used for the purpose of allowing the reader to understand what a new album sounds like based on a description of a song or album they are most likely familiar with.

Other frequently used positive terms include “best”, “work”, “well”, and “love”, which are often used to describe what the author of the review argued were the best elements of well-rated albums, as well as what made the album good from their perspective.

![Most Frequent Negative Terms](/img/pitchfork/pitchfork_neg_terms.png)

From the distribution of the top ten most frequent terms associated with negative reviews, we see that the most frequently used term is “hard”, which was used in phrases such as “hard to know” and generally used by reviewers to express confusion over the album. Negative reviews on Pitchfork tend to criticize the content of the album, whether it be confusion over the creative direction the artist was going for on their album or a lack of interesting changes in sound as the album progresses. The latter is often reflected with the words “slow” and “lost”, which are also the most frequently used negative words. The rest of the negative terms depict the more negative themes that albums can be based around, with words such as “dark” and “death.”

![Sentiment Distribution Pie Chart](/img/pitchfork/pitchfork_sent_dist.png)

From the overall proportions of positive and negative reviews in the data set, it is clear that the majority of Pitchfork reviews have an overall positive sentiment. When comparing this distribution of sentiments with the distribution of album scores across the data set, it is clear that our overall findings properly reflect the relationship between a review’s sentiment and the album’s score.

#### Topic Modeling

Topic modeling was used on the large dataset of album reviews as one approach to determine the natural groups that the reviews could be clustered into. Using Latent Dirichlet Allocation (LDA), the topic model for the Pitchfork reviews used the context of the text to differentiate between various groups and split them into different topics. After creating a five topic model (k = 5), the top ten most frequent terms of each topic are depicted in the figure below.

![Pitchfork LDA Topic Modeling](/img/pitchfork/pitchfork_lda.png)

Based on the most frequent words from each topic, we can infer which topics refer to the various groups of reviews. Since Topic 1’s most frequent words include “dark”, “guitar”, and “acoustic”, we can infer that these reviews fall under the “Rock/Metal” genre category. Topic 2’s most frequent words include “long”, “lyric”, and “acoustic”, which indicates that these reviews fall under the “Folk/Country” genre category. The most frequent words in Topic 3 include “sense”, “break”, and “always” which could indicate that these reviews fall under the “Jazz” category given that reviews for this genre use more abstract terms to describe the music. Topic 4’s most frequent words include “one”, “voice”, and “range”, which indicates that these reviews fall under the “Pop/R&B” genre category since pop albums most notably discuss the artist’s use of their voice. Finally, since Topic 5 includes the most frequent terms “matter”, “track”, and “shade”, this could indicate that these reviews fall under the “Rap” category since one of the characteristic themes of rap artists’ lyrics is often described as “throwing shade.”

Another notable aspect of the LDA output is that the term “Buckner” is seen throughout most of these topics as one of the most frequent terms. This likely refers to the artist Richard Buckner, whose reviewed albums all fall under the Rock genre category. One reason Buckner would be mentioned across reviews for different genres could be that some Pitchfork reviews include information about newly released music announcements in the subheadings of the reviews. There are additionally many Pitchfork articles called “News in Brief” which discuss new music releases, combining all genres into one review article.

#### Cluster Analysis

Another approach used to determine the natural groups that the reviews could be clustered into was k-means cluster analysis. In order to determine whether sentiment scores had any effect on how reviews were classified, we append the positive and negative sentiment scores from [R's NRC lexicon](https://search.r-project.org/CRAN/refmans/textdata/html/lexicon_nrc.html) (which assigns a numerical value of each word's association with various sentiments) to the reviews data set. After scaling the numerical data, we use the Gap Statistic method to determine the optimal number of clusters to use for our k-means clustering. This method compares the total intracluster variation for different values of k with the expected values that would fall under a distribution with no obvious clustering.

![Gap Statistic Optimal Number of Clusters Plot](/img/pitchfork/pitchfork_gapstat.png)

Based on the visualization above, since the plot bends at k = 2, the optimal number of clusters to use for our data is two. Using this parameter for R's kmeans() function with nstart = 25, we obtain the following visualization of the clustering for our reviews.

![Visualization of Clusters](/img/pitchfork/pitchfork_cluster.png)

Based on the distribution of observations in each cluster, we can infer that the reviews have been clustered into reviews with positive sentiments (cluster 1) and reviews with negative sentiments (cluster 2).

After examining the median scores across each genre, the clustering analysis output indicates that reviews in cluster 1 tend to have a higher median score than those in cluster 2.

#### Predictive Model

After categorizing the album's ratings into binary values, 1 = "High Rating" and 0 = "Low Rating", using the median 7.3 as the cutoff (high score > 7.3, low score < 7.3), the baseline accuracy of this classification is about 47.8%. After using random forest with ntrees = 50, we achieve a baseline accuracy of 63.8% when predicting whether an album will be high scoring or not.

This increase in accuracy implied that the model was successful, but could be improved. However, due to the issue of the model becoming too computationally expensive to execute, this model will be the final predictive model. Under this model, roughly 64% of the album reviews are higly rated, while 36% of the album reviews have low ratings. Looking back at the distribution of positive and negative reviews across Pitchfork's website, this model aligns well with the original findings of the data.
