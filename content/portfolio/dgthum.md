+++
image = "img/portfolio/TableauMap.png"
showonlyimage = false
date = "2024-03-20T19:44:32+05:30"
title = "Digital Humanities: Combining Data Science with Qualitative Research"
draft = false
weight = 3
+++

Used web scraping, classification models, and text mining, combined with qualitative research, in a web-based digital presentation (Wordpress website) that explores the societal implications of the emergence of the Hip Hop genre.

<!--more-->

---

> The code for this project can be found in [this GitHub repository](https://github.com/acwilb/Digital-Humanities-Project). All data cleaning, analysis, and visualizations were done in R and Tableau.

---

#### Introduction

The purpose of this project was to combine quantitative and qualitative research into a single project which focused on a humanistic topic. The overarching theme of the data collection and analysis focuses on the shifting genre trends in American popular music over time, while the theme of the qualitative research revolves around the marginalization of Black artists throughout U.S. music history, focusing particularly on the reception of Hip Hop's emergence.

The following walkthrough of this project's processes will mainly focus on the quanititative aspect of this project. The website displaying the final product of this research, which focuses more on the relationship between the quantitative and qualitative data, can be found at https://theafternoon.humspace.ucla.edu/.

#### The Data

The [original dataset](https://github.com/walkerkq/musiclyrics/blob/master/billboard_lyrics_1964-2015.csv) included all Billboard Year-End Top 100 entries from 1964 to 2015, with the variables "Rank", "Song", "Artist", "Year", "Lyrics", and "Lyric Source". Using the R packages [rvest](https://rvest.tidyverse.org/) and [RCurl](https://cran.r-project.org/web/packages/RCurl/index.html), Billboard Top 100 entries from 2016 to 2023 were added to the dataset as well as the corresponding lyrics. Additionally, using Python's [Spotify API](https://spotipy.readthedocs.io/en/2.22.1/), the variable "Genre" was added to the dataset.

The updated dataset can be found [here](https://github.com/acwilb/Digital-Humanities-Project/blob/main/billboard_1965-2023.csv).

#### Methodology

##### Web Scraping

Using R's rvest package, the Wikipedia pages "Billboard Year-End Hot 100 Singles" for each year were scraped for song information such as song ranking, song name and song artist. This was done using a loop that iterates through the years of interest (2016 to 2023), inputting each year into the predictable URL string for each Billboard page (e.g. "wikipedia.org/wiki/Billboard_Year-End_Hot_100_singles_of_2017"), and scraping each webpage's .wikitable objects to output all songs and artists on the Billboard Hot 100 chart for each year.

![Wikitable Example](/img/dgthum/wikitable.png)

Using the rvest package in combination with R's RCurl package, the lyrics for each song were then scraped from letras.com. This was done using a loop that inputs each song's name and artist into the predictable URL string for each song's lyric page in the format "letras.com/ARTIST/SONG.html". If a particular song's lyric page did not exist on letras.com, the loop moved past this observation and indicated that the lyrics were not found.

Once the original dataset was updated, with all Billboard Year-End Hot 100 entries from 1965 to 2023, the "Genre" column was added to the dataset through scraping the Spotify API. The artist ID for each song was inputted into the API, and the genres of music for each artist were outputted. At this point, one observation of the genre column looked something like "['pop rap', 'rap', 'southern hip hop', 'trap', 'viral trap']", with many subgenres listed.

##### Genre Classification

In order to standardize the Genre column to make the analysis easier to understand, the R package [dplyr](https://dplyr.tidyverse.org/) was utilized along with regex and classifcation loops to simplify observations such as "['pop rap', 'rap', 'southern hip hop', 'trap', 'viral trap']" into "Hip Hop".

The first step toward this standardization was to remove the "[]'" symbols from each row in the Genre column. This was done uing R's gsub() function. Each string of genres was then split into individual genres using R's strsplit() function.

The custom function split_genres() was then written to iterate through each row's string of subgenres and categorize the sting of genres into one main genre based on which term was most frequent in that string. For example, if the subgenre "indie rock" was present in the string, the song was categorized into the "Rock" genre.

From there, the custom function replace_genre() was written to replace the list of subgenres throughout the data frame with their main genre assigned to them from the split_genres() function.

Once the genre classification was implemented for each row of the dataset, the values in the Genre column were "Rock", "Soul", "Country", "Pop", "Hip Hop", "R&B", and "Other".

#### Exploratory Data Analysis

Genre was the main variable of interest when exploring this dataset. The first step toward understanding the prevalence of each genre was to visualize the overall distribution of genre across all entries of the Billboard Year-End Hot 100 from 1965 to 2023.

![Distribution of Genre](/img/dgthum/genre_dist.png)

The top three most prevalent genres on the U.S. top charts are Rock, Pop, and Hip Hop. Since this spans nearly six decades of music, breaking the distribution of genre down by decade would provide better insight into the evolving landscaoe of the music industry over time.

![Distribution of Genre per Decade](/img/dgthum/genre_dist_decade.png)

Rock dominated the charts from the 1960s through the 1980s, with Pop and Hip Hop becoming more prominent starting in the 1990s. From that point onward, Pop dominated the charts. Notably, Hip Hop emerged in the 1990s and has maintained a strong presence on the top charts since then.

![Genre Trends over Time](/img/dgthum/genre_trends.png)

Similar findings can be displayed through the above line graph, allowing us to see the years in which each genre peaked in popularity on the Billboard Year-End Charts.

Rock reached its highest peak of frequency in the top charts in [1982](https://en.wikipedia.org/wiki/Billboard_Year-End_Hot_100_singles_of_1982), which was the year Soul had significanly less frequncy on the charts that previouly seen. Songs such as "Eye of the Tiger", "I Love Rock 'n Roll", and "Don't Stop Believin'" topped the charts during this time.

Pop reached its highest peak of frequncy in the top charts in [2016](https://en.wikipedia.org/wiki/Billboard_Year-End_Hot_100_singles_of_2016), with Hip Hop following as the second highest in frequency. Artists such as Justin Bieber, Adele, Rihanna, Drake, and Future frequented the charts during this time.

Hip Hop reached it highest peak of frequency in the top charts in [2004](https://en.wikipedia.org/wiki/Billboard_Year-End_Hot_100_singles_of_2004), with Pop following as the second highest in frequency. Usher appeared on the charts four times this year, with OutKast, Kanye West, and Jay-Z also frequnting the charts during this time.

#### Integrating Qualitative Data into the Findings

The research question of the Digital Humities project was:

> How have socio-cultural dynamics influenced the marginalization of Black artists and stigma surrounding the emergence of Hip Hop, as viewed through the lens of music?

In order to answer this question using both the findings above and qualitative research surrounding the topic of the marginalization of Black artists, constructing a coherent narrative arround these visualizations was crucial.

One way of integrating both the quantitiative and qualitative data into one visualization was through a geographical map. One source for the qualitative research dove into the role geography played in the start of Hip Hop artists' careers as the genre rose to prominence. As a supplement to this portion of the project's narrative, a geographic dataset was created by web scraping the career origin locations of all Hip Hop artists that appeared on the Billboard Year-End Hot 100 charts over the span of 25 years. Using Tableau, the [hotspots of Hip Hop career origins](https://public.tableau.com/app/profile/alison.wilbur/viz/25YearsofHipHop-BillboardTop100/Sheet1) in the U.S. were visualized.

![Tableau Map of Hip Hop Hotspots](/img/dgthum/tableau_map.png)

In addition, the quantitative analysis was used to answer the research question throughout the project's narrative as the findings were used to support the most relevant quotes from the various qualitative sources.
