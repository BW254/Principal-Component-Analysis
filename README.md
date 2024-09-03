# Principal-Component-Analysis
## Background-
The conflict between Israel and Hamas has been ongoing for a very long time now. In 2021, Palestine moved a motion calling an end to Israel's occupation of Palestinian territories to the UN General Assembly. Of the 147 votes cast, 139 were in favour of this motion, 9 were against it, while 41 countries abstained from voting.

# The Problem
There were several questions placed before the member countries, with regards to this motion. A given country was free to vote in any way for each of the questions, i.e., either support or fail to support. Considering that there are over 100 countries, pronouncing themselves on more than one issue, it can be difficult to identify patterns in voting. 
Principal component analysis (PCA) is a machine learning dimensionality reduction technique that can come in handy in such a scenario. We can reduce noise and focus on only the important factors.
# Workings
```
{
library(magrittr)
library(tidyverse)
install.packages("globals")
library(globals)
library(recipes)
##Part 1: Unsupervised Learning
#Importing 2 data files (unvotes.csv and issues.csv.) from a GitHub repository
unvote_1 <- read.csv('C:\\Users\\ADMN\\Desktop\\ricoh\\UN_VOTE.csv')
issues_1 <- read.csv('C:\\Users\\ADMN\\Desktop\\ricoh\\ISSUES.csv')


##create a dataframe named unvote_2 comprising columns /country, rcid, and vote/
#change column vote to a factor using mutate fn, with levels /no, abstain, and yes/
#create column /rcid/ by appending prefix /rcid_/ to values of column rcid
# pivot data from long to wide format using "rcid" as column names and "vote" as the values.

unvote_2 <- unvote_1 %>%
  select(country,rcid,vote)%>%
  mutate(vote = factor(vote, levels = c  ("no","abstain","yes")),
         vote = as.numeric(vote),
         rcid = paste0("rcid_", rcid)) %>%
  pivot_wider(names_from = "rcid",values_from = "vote", values_fill = 2)


#conducting PCA
#create a recipe for PCA. 
#change the role of "country" column to "id" implying that it is treated as as identifier variable rather than a predictor in the analysis.
#Normalize all predictor variables
#use "step_pca" function to perform PCA.
#store the resulting PCA recipe in the "pca_prep" object.

pca_rec <- recipe(~ ., data = unvote_2)%>%
  update_role(country, new_role = "id")%>%
  step_normalize(all_predictors())%>%
  step_pca(all_predictors())
pca_prep <- prep(pca_rec)

#apply the PCA recipe to the "unvote_2" data frame using the /bake/ fn.
#use ggplot to generate a scatter plot and present PC1 and PC2 on the x and y axes
#label each point with the corresponding country name.
#use violet colour for points
#use /check_overlap and hjuhttp://127.0.0.1:23597/graphics/plot_zoom_png?width=1315&height=708st/ fn to adjust labels

bake(pca_prep, new_data = NULL)%>%
  ggplot(aes(PC1, PC2, label = country)) +
  geom_point(color = "violetred2", alpha = 0.7, size = 2) +
  geom_text(check_overlap = TRUE, hjust = "inward")

}
```


# Results 
PCA helps to identify patterns in high-dimensional data, and project them on lower-dimensional space as seen in the plot below.
{plot}
![PCA](https://github.com/user-attachments/assets/e2c61a04-9f43-41d8-87d3-07a11e95125e)

The plot above indicates the first two principal components (PC1 and PC2), indicating the voting patterns of different countries regarding the issue of Palestinian conflict. 
First and foremost, we can look at the outliers. United States, Israel, and Czechoslovakia seem to have voted significantly different from the rest of the countries which seem to belong to certain clusters. Such unique voting patterns may not be well represented by the first two principal components, i.e., PC1 and PC2. For Israel, it would be understandable considering that the voting impacts them directly. Israel and the United States seem not to be very far from each other on the plot, which could imply that they voted similarly on most issues. 
Finland, Luxemburg, Sweden, France, Portugal, United Kingdom, Greece among others seem to be clustered together at the far central bottom of the plot. This suggests that their voting patterns were similar in most of the presented issues. 
Niger, Morocco, Egypt, Mauritania, Burundi, Ethiopia, Lesotho, etc. are clustered to the far left of the plot. Interestingly, some countries such as Singapore, Laos, India, China, Nepal, etc. are also close this cluster. 
North Korea, Yemen, Dominica, Russia, etc. are all on the higher levels of PC2. 
These are just but a few insights that can be derived from this plot. Most African countries appearing in the far left of the plot, most European countries appearing in the bottom central part of plot, etc. However, there are outliers such as Namibia, Federal Republic of Germany, etc. that seem to go against regional block-clustering.
This analysis is just the starting point. However, we have gained insight on probable patterns and trends which can be very helpful with regards to further analysis.

