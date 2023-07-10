# Classification of tweets based on sentiment 
## Project Overview
In this project, I built a classification model to analyse tweets regarding different technological products in order to identify the sentiment expressed in them. To do so, I used natural language processing tools and experimented wtih different classifcation algorithms in an attempt to yield the best result. First, I took in large amounts of data about past tweets and experimented with different ways of preprocessing, then I built models that analyse the relationhsip betweem various characteristics of the text and the sentiment expressed such that it can identify the sentimnet of a given tweet. I iteratively modified on the features of the training data based on the results of the previous model until I arrived at a final model. 
## Business Problem
I am working with the advertising team of twitter, who works with various comapnies interested in curating advertisements of their products directed at twitter users. My goal is to build a model that can identify the sentiment expressed in a given tweet in order inform clients of what twitter users like and dislike about their products such that they can create better advertisements to promote their products. <br/>
In other words, I need a model that can accurately classify tweets such that twitter would be able to sort the tweets by postive or negative sentiments, and inform their clients about what users think about thier products. Since the goal is to help clients with advertising, in which the positive aspects of the product is emphasized, I will prioritize identifying postive sentiments.
## The Data
The data I will be using to train the model is from data.world, which contains almost 10,000 tweets that are labelled with their respective sentiments and product towards which the tweet was directed. There were three categories of sentiments: positve, negative, neutral, and unknown. Since the goal is to identify the sentiment, I dropped the 'unknown' entires as they would not provide useful information, and I focused on the columns containing the text and the sentiment since I want the model to be generalizable to tweets about products not included in the database.
## Methods
There were a lot of decisions to be made about how to preprocess the data. I started off simple with just taking into account the most common words in each category and created a baseline model based on that. To give a better guage of the kind of database I am working with, here are the graphs showing the distributions of the 10 most common words in tweets of each of the three categories, which is what my baseline model took into account. <br/>
![image](https://github.com/Beatrixwmh/phase-4-project/assets/108293459/d8002d10-f9b4-46fd-9b4a-447c65b3e8f5) 
![image](https://github.com/Beatrixwmh/phase-4-project/assets/108293459/e32856bc-11f6-4be7-836c-6a960d4220bb)
![image](https://github.com/Beatrixwmh/phase-4-project/assets/108293459/49882ce2-86a1-48ba-a289-449c815f9f93)

As apparent above, there were a lot of words they shared in common, which is not useful in helping the model differentiate between the three sentiments. I then tried removing words that were common to all three categories and added more features, like reducing every word to thier basic form and looking at the most common pairs of words in each category, viasaulizing the distrubtions and testing my new set of features with a new model every time to see if there was any improvement. <br/>
After many rounds of experimentation, I ended up with a set of features that encompasses infomration like the 500 most common single words and pairs of words respectively, and also the number of exclaimation marks in each tweet. <br/>
Moreover, since the data has very strong class imbalance, with roughly 60% of tweets being neutral, 30% being postitive, and only 6 % being negative, I used oversampling, which is a tool that repeatedly samples data from the minority classes randomly such that the model would learn more about the patterns in the minority class to better able to identify them. Moreover, since identifying postiive sentiment is more important than identifying the other two sentiments for the purposes of advertising, I ended up combining neutral and negative classes together and made a binary classification model in order to improve its accuracy. Lastly, I compared different classification models to one another to find the estimator that yielded the best results.
## The final model
My final model takes in features mentioned above, and is a support vector machine, which takes in the data points with thier corresponding features and finds the best line of seperation between the data points in order to classify them into one sentiment or the other. Shown below is an example of how the model classifies unseen data. <br/>
![image](https://github.com/Beatrixwmh/phase-4-project/assets/108293459/22ef41ab-1d0c-4534-8dfb-f2c527e8357e)
This model has an accuracy of around 72 %, meaning it identifies 72% of the data correctly. Moreover, it is able to recognize around 60% of positive tweets and 80% of non-positive tweets, in other words, if twitter were to use this model to sort tweets and find the ones expressing positive sentiments, it would be able to capture 60% of them.
## Recommendations
I would recommend the advertising team to use this model to assist them in looking for positive tweets to get a guage of what the twitter userbase likes about certain products. However, since the model still has a relatively low precision and misidentifies a neutral or negative sentiment for a positive one 40% of the time, I would advise them to use more sorting tools to further weed out true positives.
## Next Steps
To further improve this model, I could look into more features unique to each class and add it to the training data, like the amount of capitalizations or emoticons used in a tweet. Considering the many preprocessing steps required to prepare the data for the model, I could also work on building pipelines to streamline the process of implementation. <br/>
Moreover, I could work on expanding this model into a multi-class classifier by increasing the size of my database and obtaining more tweets with negative sentiments such that the model can also identify negative sentiments well. 
## For More Information
Please review our full analysis in the [github repository](https://github.com/Beatrixwmh/phase-4-project) or [my presentation].
For any additional questions, please contact Beatrix Wong, beatrix.wmh@hotmail.com

## Repository Structure
```
├── README.md                           <- The top-level README for reviewers of this project
├── ph_4_proj.ipynb                     <- Narrative documentation of analysis in Jupyter notebook
├── phase-4-presentation.pdf            <- PDF version of project presentation
├── sentiments.csv                      <- Both sourced externally and generated from code
└── images (.png)                       <- Both sourced externally and generated from code
```
