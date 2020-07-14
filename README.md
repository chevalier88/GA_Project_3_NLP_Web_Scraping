# Can The Wisdom of Reddit's Crowd Help Us Clarify the Difference Between Data Science and Analytics?
by Graham Lim

## Please Note
**It is strongly recommended that this project is accessed using Jupyter Notebooks and NOT Jupyter Labs. 

This is because we will use custom interactive plots for our numerical data. **You'll be able to zoom in and mouse over the distributions to see value counts.**

**For the visualizations to work, please install the libraries at your command line/terminal using:**
- pip install plotly
- pip install cufflinks
- pip install squarify
    
## Problem Statement
Can we create a Natural Language Processing model utilizing either Multinomial Bayes or Support Vector Machines to:
- accurately predict whether a reddit post is from r/DataScience or r/Analytics, and
- use the better performing model's keywords to distinguish what conceptual and technical differences exist between Data Science vs Analytics through keyword analysis of the two subreddits,
- in order to make concrete educational or professional recommendations to students and professionals interested in either topic?

We evaluate success on predictive model accuracy for the first requirement, and quality and uniqueness of distinct keywords to fulfill the other two requirements.The stakeholders who care are our fellow data science peers, students, as well as professionals considering to improve their own skillsets.

## Executive Summary
The short answer is that we can make a very accurate predictive model using Multinomial Bayes (MNB) and TFIDF to address the first part of our problem statement, but it won't generate enough unique keywords for us. This means accurate MNB modeling alone doesn't provide meaningful insight concerning the differences between Data Science and Analytics. However, we were able to answer the full problem statement by using a secondary model based on TFIDF SVM focusing on post titles only.

After scraping from Reddit's API, cleaning, exploratory data analysis (with custom functions creating multiple visualizations) and textual pre-processing, we created a Natural Language Processing model using as a baseline unoptimized Multinomial Naive Bayes model with a score of >0.86. We beat that score using a TFIDF MNB Model. We achieved superior predictive accuracy, but realized that accuracy and deriving unique and informative keywords are mutually exclusive.

To that end, we re-evaluated our models, and settled on a TFIDF SVM model that only looks at post titles, not post content. It took a small hit on accuracy compared to the primary model, but were rewarded with better keywords to achieve the objective of education pointers. 

It's important to note that the baseline score was still beaten even by our less accurate secondary model. This secondary model thus addresses all parts of our problem statement.

We took external research on those distinct keywords found from our secondary model to draw some key differences to help answer what the difference is between Analytics and Data Science, and even uncovered a trending focus on COVID in data science. We followed this with practical recommendations to both students and professionals.

## Methodology
- [Web Scraping](https://git.generalassemb.ly/chevalier88/DSI15-Clone/blob/master/project_3/code/1.Web_Scraping.ipynb)
    - Reddit API Json File Scraping into Pandas Dataframe (scraped in June 2020)
    
- [Cleaning, Feature Engineering and EDA Part I](https://git.generalassemb.ly/chevalier88/DSI15-Clone/blob/master/project_3/code/2.Cleaning_Feat_Eng_and_EDA_Part_I.ipynb)
    - Data cleaning, dropping unwanted or null data
    - Missing data imputation 
    - Summary Statistics and Distributions
    - Numerical EDA and Visualizations using Plotly 

- [Feature Engineering and EDA Preprocessing Part II](https://git.generalassemb.ly/chevalier88/DSI15-Clone/blob/master/project_3/code/3.Feat_Eng_and_EDA_Part_II.ipynb)
    - Textual Preprocessing with Lemmatization, Punctuation Removal, Lower-Casing, Stop-Words Removal
    - In depth analysis for keyword features using custom Plotly and Squarify visualizations

- [Modelling, Evaluations and Findings](https://git.generalassemb.ly/chevalier88/DSI15-Clone/blob/master/project_3/code/4.%20Modelling_Evaluations_Findings.ipynb)
    - Unoptimized Multinomial Naive Bayes baseline scoring
    - Modelling Multinomial Naive Bayes and SVM with TFIDF using Pipelines and GridSearchCV
    - Evaluating Models against Problem Statement with more visualizations
    - Findings, Recommendations, Summary and Future Steps

## Data Files
- [Datasets](https://git.generalassemb.ly/chevalier88/DSI15-Clone/tree/master/project_3/data)

## Data Dictionary
|Feature|Type|Description|
|---|---|---|
|**title**|object|Original title of subreddit post|
|**selftext**|object|Original text of subreddit post|
|**score**|integer|Score of subreddit post at time of scraping|
|**url**|object|URL of subreddit post|
|**link_flair_text**|object|Category of subreddit post|
|**num_comments**|float|Total number of comments of subreddit post at time of scraping|
|**cleaned_text**|object|Text of subreddit post after pre-processing|
|**cleaned_title**|object|Title of subreddit post after pre-processing|
|**all_words_clean**|object|Combined title and text of subreddit post after pre-processing|
|**subreddit_datascience**|binary number|Whether post is in r/datascience ("1") or r/analytics ("0")|

## Conclusion and Recommendations
After re-picking our model, we still find that the top words in post titles are identical to those we already identified briefly in EDA using general word vectorizing. 
- /r/analytics: very specific unique words like `google analytics`, and `business analytics` appear frequently, as well as `website`.
- /r/datascience: Words like `python`, `machine learning` (`ml`), and even `covid`. 

We drew multiple inferences around these keywords, before recommending specific software tools, a Kaggle competition and educational courses to answer the problem statement. We conclude with some steps for the future to make this project even better.

## External Resources
https://www.datacamp.com/community/tutorials/svm-classification-scikit-learn-python
https://python-graph-gallery.com/200-basic-treemap-with-python/
http://w3techs.com/technologies/overview/traffic_analysis/all
https://analytics.google.com/analytics/academy/
https://en.wikipedia.org/wiki/Business_analytics
https://www.mygreatlearning.com/blog/difference-between-data-science-business-analytics/#:~:text=Data%20Science%20vs%20Business%20Analytics%2C%20often,interchangeably%2C%20are%20very%20different%20domains.&text=Simply%20put%2C%20Data%20science%20is,business%20decisions%20for%20the%20company
https://towardsdatascience.com/data-science-for-decision-makers-7248beddf948
https://medium.com/@springboard_ind/data-science-vs-data-analytics-how-to-decide-which-one-is-right-for-you-41e7bdec080e#:~:text=It%20uses%20existing%20information%20to,needed%20answering%20to%20drive%20innovation
https://www.orange-business.com/en/blogs/ai-and-data-science-tool-battle-covid-19
https://trends.google.com/trends/story/US_cu_4Rjdh3ABAABMHM_en
https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge
