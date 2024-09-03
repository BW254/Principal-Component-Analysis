# Principal-Component-Analysis
## Background-
The conflict between Israel and Hamas has been ongoing for a very long time now. In 2021, Palestine moved a motion calling an end to Israel's occupation of Palestinian territories to the UN General Assembly. Of the 147 votes cast, 139 were in favour of this motion, 9 were against it, while 41 countries abstained from voting.

# The Problem
There were several questions placed before the member countries, with regards to this motion. A given country was free to vote in any way for each of the questions, i.e., either support or fail to support. Considering that there are over 100 countries, pronouncing themselves on more than one issue, it can be difficult to identify patterns in voting. 
Principal component analysis (PCA) is a machine learning dimensionality reduction technique that can come in handy in such a scenario. We can reduce noise and focus on only the important factors.
# Results 
PCA helps to identify patterns in high-dimensional data, and project them on lower-dimensional space as seen in the plot below.

{plot}

The plot above indicates the first two principal components (PC1 and PC2), indicating the voting patterns of different countries regarding the issue of Palestinian conflict. 
First and foremost, we can look at the outliers. United States, Israel, and Czechoslovakia seem to have voted significantly different from the rest of the countries which seem to belong to certain clusters. Such unique voting patterns may not be well represented by the first two principal components, i.e., PC1 and PC2. For Israel, it would be understandable considering that the voting impacts them directly. Israel and the United States seem not to be very far from each other on the plot, which could imply that they voted similarly on most issues. 
Finland, Luxemburg, Sweden, France, Portugal, United Kingdom, Greece among others seem to be clustered together at the far central bottom of the plot. This suggests that their voting patterns were similar in most of the presented issues. 
Niger, Morocco, Egypt, Mauritania, Burundi, Ethiopia, Lesotho, etc. are clustered to the far left of the plot. Interestingly, some countries such as Singapore, Laos, India, China, Nepal, etc. are also close this cluster. 
North Korea, Yemen, Dominica, Russia, etc. are all on the higher levels of PC2. 
These are just but a few insights that can be derived from this plot. Most African countries appearing in the far left of the plot, most European countries appearing in the bottom central part of plot, etc. However, there are outliers such as Namibia, Federal Republic of Germany, etc. that seem to go against regional block-clustering.
This analysis is just the starting point. However, we have gained insight on probable patterns and trends which can be very helpful with regards to further analysis.

