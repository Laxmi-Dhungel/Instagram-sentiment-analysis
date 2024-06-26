**Country based instagram sentiments and its relation to ratings** 

**Summary**

This report includes analysis of Instagram data obtained from Kaggle (Kanchana Karunarathna, 2024). The data consists of 500 ratings and reviews posted by users from 5 different countries, the USA, Canada, the UK, Germany, and India. In this report, I analyzed the ratings and sentiments towards Instagram across these countries. Furthermore, I also investigated the relationship between sentiments and ratings. The results showed higher sentiment and ratings towards Instagram in the US and India respectively. The sentiment and ratings towards Instagram were lowest in Germany. The positive sentiment percentages were highest for all the countries (except Germany). Germany had the lowest percentages of positive sentiments. These countries used different Instagram versions. Most of the reviewers from India (100%) and the US (99%) used version 323 whereas most of the reviewers from Canada and Great Britian used version 322.1.0. The reviewers from Germany used versions 322.1.0 and 323 equally (50/50). The Instagram version used can be one of the confounding variables and could be one of the possible reasons for the discrepancy. There was a significant association between sentiments and ratings. The sentiments were higher for higher rating and there were higher percentages of positive sentiments for higher rating. There were some limitations to the study such as small sample size and presence of confounding variables. However, despite these limitations the findings of the study are significant as it demonstrates country-based differences in sentiments and ratings. The findings can be utilized as a foundation and further investigations are needed to understand the lower sentiment in some country such as Germany towards Instagram. Addressing these issues can help in generating positive sentiments towards Instagram worldwide. Additionally, although it seems logical that sentiment can determine ratings, proving it with data analysis adds validity.  


**Methodology**

The data was analyzed using python in spyder (https://www.spyder-ide.org/). 
The python data analysis tools and library used were pandas (1.5.3), nltk(3.8.1), numpy (1.24.4), matplotlib (3.5.2), pingouin (0.5.4), seaborn(0.13.2), scipy (1.9.1) and statsmodels (0.13.2).
The overall code used for the data cleaning and analysis is provided here. (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Overall_code)

The code specific to particular analysis are provided as separate file as well.

**Data cleaning and validation**

The data cleaning and validation steps are summarized in figure 1. The data cleaning and validation steps included investigating data types, unique values, duplicates, and missing values. Most of the columns were object data types except columns “appleID”, “id”, “score” which were int64.  I changed the columns “country” and “version” to category data type and “date” column to datetime format. Further, I checked unique values for columns “country”, “score”, and “version”. The unique values for each of these columns looked okay. There were no duplicates and missing values. I also checked for other possible forms of missing values (“NAN", "na", "n/a", "-", "--", "nan") but they were not present in any of the columns. I created additional columns “day_of_week”, “hour” and “day_part” based on date column. The idea of generating these columns was to investigate if the day of week and day part plays any role in determining reviewer’s sentiments and their ratings. The day of the week and hours were obtained by using functions dt.day_name() and dt.hour respectively. The day_part column was created based on hour column. It included groups such as Midnight-Early Morning (0 -6 hr), Morning (6-12 hr) , Afternoon (12-18 hr), Night (18-23 hr; inclusive for both). The code for data cleaning and validation is provided as a separate file (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Data%20cleaning%20validation). 

**Limitation**

Despite creating columns days of the week and day_part, I was not able to use these for analysis as there was no clear information regarding time zone of the posted reviews and days can vary among these countries. I filtered data for USA to investigate if there is any pattern in review and sentiments based on days in column “day_of_week”. However, the day for all the reviews from USA was Wednesday (2024, 3, 20). Hence, analyzing the impact of the day part on sentiments and ratings was also dissolved as it would not represent its actual impact.

 

![data cleaning and validation](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/4e43ec4b-f4d7-40d9-a60c-430deba4f9c5)

Figure 1. The summary of data cleaning and validation steps. The data was investigated for data types, unique values, duplicates, and missing values. Most of the columns were object data types except columns appleID, id, score which were int64. The columns country and version were converted to category data type. The column date was converted to datetime format. The unique values for columns country, score and version were investigated. The unique values for country were ['CA', 'DE', 'GB', 'IN', 'US'], the unique values for score were [1 4 3 2 5] and the unique values for version were ['313.0.0', '322.0.0', '322.1.0', '323.0.0']. There were no duplicates and missing values. The presence of other possible forms of missing values ["NAN", "na", "n/a", "-", "--", "nan"] were also investigated. Additional columns “day_of_week", “hour” and “day_part” were created. The “day_of_week" columns included days from Monday to Sunday, “hour” column included hour the review was posted and “day_part” column included groups Midnight-Early Morning, Morning, Afternoon and Night based on hour column.

**NLTK Sentiment Analysis**

The NLTK (natural language toolkit) sentiment analysis was performed based on sentiment analysis tutorial by Moez Ali from Datacamp (Ali, 2023). The NLTK was installed and imported. The toolkit requires other data such as pre-trained models, corpora and other resources which were also downloaded using nltk.download (‘all’). The text needs to be preprocessed before performing sentiment analysis. The preprocessing steps were tokenization, removing stop words and lemmatization. The tokenization breaks text into individual words and removing stops words includes removal of common and irrelevant words such as ‘and’, ‘the’, etc. The lemmatization reduces the words into it’s base form. After preprocessing the text SentimentIntesityAnalyzer from nltk sentiment vader library was initialized. The polarity_scores method of the analyzer object was used to get the sentiment scores. The method takes text as an input and provides sentiment scores that contains a dictionary which contains scores for positive, negative, neutral, and overall (compound) sentiments. This information was stored in a new column named “scores”.  Additional new columns sentiment and sentiment_score was generated to store the overall sentiment and score (compound) respectively. The overall sentiment was determined based on compound sentiment score. The sentiment was considered positive if the compound sentiment score was greater than 0, negative if the compound sentiment score was lesser than 0 and neutral if the compound sentiment score was equal to 0. Similarly, the sentiment_score column had the values of compound sentiment score. The code for sentiment analysis is provided in a separate file named sentiment analysis (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/sentiment%20analysis).

**Statistical analysis**

The pairwise tukeyhsd test was used to determine the statistically significant difference in average scores and sentiments between countries. The test was also used to determine significant difference in sentiments for different review scores. Further, chisquare test was used to test the association between review scores (Rating) and sentiments. The chisquare test was performed using pingouin and the post hoc test was adapted from Chi-square (and post-hoc) tests in Python by neuhofmo (https://neuhofmo.github.io/chi-square-and-post-hoc-in-python/). 

**Results**

**Review based on country**

The average rating for Instagram for each country was computed. The highest average rating was given by India (2.60) whereas the lowest average rating was given by Germany (Figure 2). The average rating given by Germany was significantly lower than rating given by India and US (Tukeyhsd, sig (p<=0.05)). Further, the review scores for each country were counted. Most countries gave a score of 1 followed by 5 (except Germany) (Figure 3). (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Review_country_wise)

![Average_rating-country](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/48cff7e8-11ae-4e2f-bb14-77a5f0e4bf70)

Figure 2. The average rating given by each country. The highest average rating was given by India whereas the lowest average rating was given by Germany. The average rating given by Germany was significantly lower than average ratings given by India and USA (pairwise tukeyhsd, sig (P<=0.05)). (CA: Canada, DE: Germany, GB: Great Britian, IN: India, US: USA). 

![review_score_count](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/abde21b1-d2a5-4768-8d22-9701bd7dcdbe)

Figure 3. Count of review scores (Rating) for each country. Most of the people in all the countries gave ratings of 1 followed by 5 (except Germany).

**Sentiments based on country**

The sentiment scores were obtained using Python NLTK (natural language toolkit) described in methodology section. The US had the highest sentiment score (0.19) whereas Germany had the lowest sentiment score (0.2) (Figure 4). The sentiment score for Germany was significantly lower than sentiment score for any other country. The sentiment scores were divided into positive (>0), neutral (=0) and negative (<0) based on the compound scores obtained from sentiment analyzer. The positive, neutral, and negative sentiments for each country were counted. For all countries (except Germany), there was highest number of positive sentiment whereas Germany had the lowest number of positive sentiments (Figure 5). Among all countries, the US had the highest number of positive sentiment count and Germany had the highest number of neutral and negative sentiment count. (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Sentiments_country) 

![average_sentiments_country](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/e1b95726-85c5-4c1c-b78f-fe90d598616f)

Figure 4. The average sentiment score for each country. The average sentiment score was highest for USA whereas it was lowest for Germany. The sentiment score for Germany was significantly lower than sentiment scores for any other country (pairwise tukeyhsd, sig (p<=0.05). 

![sentiments_country](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/a841a394-60fa-433f-94c9-1b64b5605132)

Figure 5. The count of sentiments (positive, neutral, and negative) in each country. Most of the country (except Germany) had the highest number of positive sentiments. Germany had the highest number of neutral and negative sentiments. The count of positive sentiments for Germany was lower than the count of neutral and negative sentiments.  

**Instagram version used by each country**

The Instagram version used by each country was counted. The US and India mainly used the latest nstagram version 323 whereas most reviewers from Canada and Great Britian used version 322.1.0 (Figure 6). Reviewers from Germany used 322.1.0 and 323 equally (50/50). (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Countplot_version)

![count_instagram_version](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/b346077b-ed39-4c88-b15b-1d134964b639)

Figure 6. Count of Instagram versions used in each country. All (100/100) of the reviewers from India used latest Instagram version 323.0.0 whereas 99/100 of the reviewers from USA used the same version. Higher number of reviewers from Canada (67%) and Great Britian (63%) used Instagram version 322.1.0. The reviewers from Germany used versions 322.1.0 and 323.0.0 equally (50/50). 

**Relationship between sentiment score and review score (Rating)**

The average sentiment score for each review score was determined. The average sentiment score was highest for the review score 5 whereas it was lowest for the review score 1 (Figure 7). The average sentiment score for review score 1 was significantly lower than review score 4 and 5. Similarly, the average sentiment score for review scores 2 and 3 was significantly lower than review score 5. There was a low positive correlation between review score and sentiment score (0.37). The relative percentages of sentiments for each review scores showed that percentages of negative sentiments (40%) were highest in review score 1, percentages of neutral sentiments were highest in review score 2 (37%) and 4 (51.5%), and the percentages of positive sentiments was highest in review score 3 (46%) and 5(70%) (Figure 8). The review score 5, 4 and 1 had the highest percentages of positive, neutral and negative scores respectively. The Chi-squared independence tests showed a significant assocation between review scores (Ratings) with sentiment. A post hoc analysis was performed comparing sentiments between each review score (Rating) pairs. The p-values were corrected for multiple comaprisons using FDR correction. The results showed that sentiments of reviewers who gave review scores (Rating) 1,2 and 3 significantly differed than the sentiments of reviewers who gave review scores (Rating) 4 and 5. Further, there was also a significant difference in sentiments between reviewers who gave ratings 4 and 5. (https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/blob/main/Relationship_sentiment_review)

![review_score_sentiment_score](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/f5d41879-aa8c-4c96-a972-f6abec1ee2b8)

Figure 7. The bar graph showing the average sentiment scores for each review score (Rating). Rating 5 had the highest sentiment scores whereas rating 1 had the lowest sentiment score. The sentiment scores for ratings 1,2 and 3 were significantly lower than sentiment scores for rating 5. The sentiment score for rating 1 was also significantly lower than sentiment score for rating 4. 

![RP_review_sentiments](https://github.com/Laxmi-Dhungel/Instagram-sentiment-analysis/assets/154451345/2df975cf-30dc-4d8d-84ec-2536307951ff)

Figure 8. Relative percentages of sentiments for each review scores. The positive sentiment was highest for rating 5 whereas it was lowest for rating 2. The negative sentiment was highest for rating 1 whereas it was lowest for rating 4. The highest percentages of sentiments for ratings 1,2,3,4 and 5 were negative, neutral, positive, neutral and positve respectively. The chisquare test showed a significant association between review score (Rating) and sentiments (p<0.05). The sentiments of reviewers who gave ratings 1,2 and 3 significantly differed than the sentiments of reviewers who gave ratings 4 and 5 (Separated by red line). Further, there was also a significant difference in sentiments between reviewers who gave ratings 4 and 5.  

**Conclusion**

The results showed country-based differences in ratings and sentiment score. The US and India had higher sentiment score and ratings respectively towards Instagram whereas Germany had lowest sentiment score and ratings. The relative percentages of sentiments for each countries showed that all the countries (Except Germany), had highest percentages of positive sentiments. Germany had the highest percentages of neutral sentiment and the lowest percentages of positive sentiments. The exact reason for negative sentiments and rating towards Instagram in Germany is not clear. According to Frobes, Germans are sensitive towards their privacy and its monetization and the country has the highest percentage gaps between total internet users (93%) and social meida users (51%) (Forbes, 2024). The Instagram version used by each country was investigated. Different Instagram versions may have different features which can also contribute to the sentiment and ratings. Most of the reviewers in the study from the US (99%) and India (100%) used the latest version 323 whereas most of the reviewers from Canada and Great Britian used version322.1.0. Reviewers from Germany used versions 322.1.0 and 323 equally (50/50). The Instagram version could be the confounding variable and one of the possible reasons for positive sentiments and higher ratings seen in the US and India. However, further study with large data sets, uniform sample size and addressing of confounding variables are needed to confirm any of these findings. Moreover, the relationship between sentiment score and ratings was investigated. The sentiment score was higher for higher rating. There were higher percentages of positive sentiments for higher ratings. The chi square test of independence showed a significant association between sentiments and ratings. However, there are some limitations to this study such as small sample size, chances of bias due to limited time frame and confounding variables. Despite these limitations, the results are significant as it demonstrates that sentiments towards Instagram can vary based on country. The findings can be utilized as a foundation and further investigations are needed to understand the lower sentiment in Germany towards Instagram. Addressing these issues can help in generating positive sentiments towards Instagram worldwide. Further, there was a significant association between sentiments and ratings. Although it seems logical that positive sentiment will result in higher ratings and negative sentiment will result in lower ratings, proving it with data analysis adds validity.  

**Recommendation**

1. Investigate reasons for lower sentiment and ratings in some country such as Germany. Adressing the issue will help generating the positive sentiments towards Instagram worldwide.

2. Further analysis with large data set and adressing confounding variables is needed to provide better insights. 

**References**

1. Ali, M. (2023). NLTK Sentiment Analysis Tutorial for Beginners. Retrieved from https://www.datacamp.com/tutorial/text-analytics-beginners-nltk
2. Kanchana Karunarathna. (2024). Instagram Ratings &amp; Reviews: Appstore. https://doi.org/10.34740/KAGGLE/DSV/7916478
3. Hutto, C.J. & Gilbert, E.E. (2014). VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text. Eighth International Conference on Weblogs and Social Media (ICWSM-14). Ann Arbor, MI, June 2014.

4. Study Shows Half Of Germans Don’t Use Social Media. Forbes, 2024. https://www.forbes.com/sites/petersuciu/2024/03/07/half-of-germans-dont-use-social-media-use-among-africans-on-the-rise/?sh=2d9514d62977





