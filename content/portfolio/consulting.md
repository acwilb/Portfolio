+++
showonlyimage = false
draft = false
image = "img/portfolio/StatConsult.png"
date = "2016-11-05T19:59:22+05:30"
title = "Statistical Consulting: Identifying Trends in High School Students' Perceptions of Drugs"
weight = 4
+++

Worked with real-world clients on a statistical consulting problem for UCLA statistics capstone course.

<!--more-->

---

> The code for this project can be found in [this GitHub repository](https://github.com/acwilb/Statistical-Consulting-Project). All data cleaning, analysis, and visualizations were done in R.

---

#### Introduction

This study investigates whether Hispanic students in Los Angeles generally perceive party drugs of the categories Hallucinogens, MDMA, and GHB to be more harmful and addictive than Non-Hispanic students do.

Using the zip codes of student participants, we explore general trends of how student rankings of harmfulness and addictiveness differ based on where they live. After examining the students’ initial perceptions of the dangers associated with these drugs, we evaluate the impact of the client's intervention (informative classroom presentation) on students’ perceptions by identifying differences between pre-visit and post-visit survey responses.

#### The Data

The data used in this study combines the client's Pre-Visit Survey dataset (survey questions filled out by students before the client's presentation) with the client's Post-Visit survey responses, both from the year 2019. The Pre-Visit survey responses were used to examine the relationship between student demographics and their initial perceptions of harmfulness and addictiveness of each category of party drugs, while the Post-Visit survey responses were used to evaluate the impact of the client's intervention on students’ perceptions of the dangers of party drugs.

##### Research Questions

> Do Hispanic students in Los Angeles school districts generalize the perceived harmfulness and addictiveness of party drugs in their rankings more than Non-Hispanic students?

> Did the client's intervention have any effect on students’ perceptions of the dangers associated with each drug category?

##### Variables in the Study

Participants in this study were high school students from Los Angeles school districts. The client's 2019 Pre-Visit and Post-Visit surveys included students’ demographic information (race and zipcode), familiarity ratings, perceived harmfulness rating, and perceived addictiveness ratings of specific drugs.

Our variables of interest for these particular research questions included students’ **race**, **zip code**, and **harmfulness and addictiveness ratings** for party drugs that fall under the categories of Hallucinogens, MDMA, and GHB. The variables Zipcode and Race were measured as categorical variables, while Harmfulness and Addictiveness ratings were measured using the Likert scale (range from 1 to 5).

After examining the initial perceptions, the client's Post-Visit survey was used to assess the effectiveness of the client's intervention on harmfulness and addictiveness ratings for Hallucinogens, MDMA, and GHB.

###### A snippet of the pre-visit dataset:

![Dataset Snippet](/img/consulting/dataset.png)

#### Exploratory Data Analysis

###### Pre-Visit Survey

In the pre-visit sample, Hispanic students make up about 58% and Non-Hispanic students make up about
42%. We see that a majority of students live in the 90034 area and that most of these students are Hispanic.
Looking at the overall proportions of students’ initial perceptions of the dangers of party drugs, we see that
the ratings were mostly high among both groups, and a trend of more Non-Hispanic students with lower
ratings of perceived dangers than Hispanic students.

![Distribution of Zipcode](/img/consulting/zipcode.png)

##### Hallucinogens

For the category of Hallucinogens, we see that the distribution of ratings for harmfulness and addictiveness
are about the same for Hispanic students, with a ranking of 5 being the most prominent for both. The
distribution of harmfulness for Non-Hispanic students saw a ranking of 4 as the most prominent, and a
ranking of 5 for addictiveness.

|                                                                               |                                                                                |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| ![Distribution of Hallucinogens Harmfulness](/img/consulting/hal_harmful.png) | ![Distribution of Hallucinogens Addictiveness](/img/consulting/hal_addict.png) |

##### MDMA

For the category of MDMA, we see a trend of both Hispanic and Non-Hispanic responses rating the harmfulness and addictiveness as 4 or 5, indicating that students perceive drugs such as Molly and Ecstasy to be the most dangerous of all party drugs.

|                                                                       |                                                                        |
| --------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| ![Distribution of MDMA Harmfulness](/img/consulting/mdma_harmful.png) | ![Distribution of MDMA Addictiveness](/img/consulting/mdma_addict.png) |

##### GHB

For the category of GHB, we see that the distributions for both Hispanic and Non-Hispanic students differ the most from the previous distributions we’ve looked at. For both groups, the most frequent rating of harmfulness and addictiveness was 3, indicating that students in both groups perceive the dangers of sedative club drugs to be the either the most neutral, or that most students have the least amount of knowledge of these drugs.

|                                                                     |                                                                       |
| ------------------------------------------------------------------- | --------------------------------------------------------------------- |
| ![Distribution of GHB Harmfulness](/img/consulting/ghb_harmful.png) | ![Distribution of MDMA Addictiveness](/img/consulting/ghb_addict.png) |

###### Post-Visit Survey

The change in harmfulness and addictiveness ratings of each drug group were calculated by subtracting each student’s pre-survey response from their post-survey response. Positive values indicate an increase in the perceived danger of the drug, while negative values indicate a decrease in perceived danger.

|                                                                          |                                                                           |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| ![Difference in Harmfulness Ratings](/img/consulting/change_harmful.png) | ![Difference in Addictiveness Ratings](/img/consulting/change_addict.png) |

After the client's intervention, harmfulness ratings of Hallucinogens and GHB generally increased, while MDMA generally stayed the same. Addictiveness ratings of Hallucinogens, MDMA, and GHB generally increased.

#### Statistical Analysis

In the statistical analysis, we seek to determine whether the client’s educational intervention led to significant
changes in the perceptions of harmfulness and addictiveness for hallucinogens, MDMA, and GHB, comparing
pre-visit and post-visit scores. Utilizing t-tests, we examine if there are any significant differences in
students’ perceptions after the intervention, aiming to identify both fixed and proportional changes from
their original pre-visit scores.

![t-test Output](/img/consulting/t_test.png)

##### Hallucinogens

For harmfulness, the paired t-test yielded a p-value of 0.4010539, suggesting that the intervention did not
significantly change the students’ perceptions of hallucinogens’ harmfulness. For addictiveness, perceptions
of addictiveness did not show a significant change post-intervention, with a p-value of 0.7596341.

##### MDMA

For harmfulness, a p-value of 0.4661176 was observed, indicating a non-significant intervention effect on
the perceived harmfulness of MDMA. Likewise, the intervention did not significantly affect the perceived
addictiveness of MDMA, as indicated by a p-value of 0.879436 for addictiveness.

##### GHB

For harmfulness, the intervention’s influence on the perceived harmfulness of GHB was not significant, with
a p-value of 0.3181954. However, a significant change in the perception of GHB’s addictiveness is present, given that the
paired t-test resulted in a p-value of 0.1061151, approaching the conventional threshold for significance.
The confidence intervals provide a deeper insight into the potential range of the true mean differences. The
results indicate variability in the intervention’s impact across the drug categories. These findings suggest
a need for further investigation into the factors that contribute to the changes in perception, particularly
regarding GHB, which showed a trend toward a significant change in perceived addictiveness.

#### Conclusion

The statistical analysis conducted on the data after the client's intervention revealed that there were no significant changes in the students’ perceptions of the harmfulness and addictiveness of hallucinogens, MDMA, and GHB as a direct result of the intervention.

The p-values indicated that the perceived risks associated with these drugs did not differ significantly before and after the intervention among the surveyed groups. The confidence intervals corroborated these findings, displaying a range that includes values suggesting no change and, for GHB’s addictiveness, a trend towards significance that warrants further investigation.

This analysis underscores the complexity of altering substance-related perceptions among high school students and highlights the importance of tailoring educational interventions to achieve desired outcomes.
