# Classification of Emotions for Casual Text Messages
#### Capstone Project by Alyse Su
General Assembly DSI-16

<img src="../data/image/replika.png" style="width: 700px;"/>


Multi-class sentiment analysis in the social networks and microblogging websites have been a hot topic of study in recent years due to the rapid growth of these platforms and the plethora of insights that could be derived from them. Many studies over the years have attempted to build sentiment prediction models with data from these platforms. However, there still remains many challenges that researchers face: informal use of languages, abbreviations, sarcasm, dual meanings, local slangs and [stretched words](https://www.wired.com/story/whoooaaa-duuuuude-stretch-words/). (ie. 'heeeeeeeeeey!','terrrrrrrrible!').

Many studies that have been conducted have attempted to understand basic sentiments of messages and microblog posts (ie. Negative-Positive or Negative-Neutral-Positive), attempted applaudable results. However, we believe that having a deeper understanding behind the users' sentiments by breaking down the umbrella of emotions ('negative' and 'positive') into its sub-emotion types (ie. anger, disgust, love, anticipation), would be more useful for understanding the rationale behind the overarching emotion.
- For example: If the message of a user exhibits a negative sentiment behind, is he/she simply **disappointed**, or is he/she **angry** at the subject of interest?
    - Message 1: "I *really* don't like this food *at all*. I *won't* come back to this restaurant again". (Angry/Hate)
    - Message 2: "I don't like this food, *may not* come back to this restaurant again." (Disappointed)
<!-- ![image](../data/image/angry.jpg) -->
- As we observe from the example above, we can see that Message 1 shows that the user absolutely abhors the food from the restaurant and *will not* go back again. This shows that the user is downright upset and perhaps angry at the quality of food.
- However, Message 2 tends to be milder than Message 1 in its negative sentiment. It uses words like 'may not', which shows that user is perhaps disappointed, but not to the extent of being angry.

These subtle nuances may not be captured by a negative-positive sentiment analysis model. We believe that breaking down the nuances of casual chat messages would open up a realm of possibilities in the field of insight extractions.

# Business Case
As a data science lead within one of the world's most prominent social media platform providers, one of my key projects this year is to assist the broader software engineering team in building an artificial intelligence robot for **sentimental analysis of casual text messages** sent across our communications platform. More importantly, we aspire not to only provide a basic sentiment analysis (positive-negative scale), but extract the nuances behind these two classes of emotions. (Explained in introduction above).

Billions of messages are sent across daily through our communications platform worldwide. We believe that providing a value-added service for our users by allowing them to track their sentiments and emotions through text messages, would greatly enhance their user experience and increase user retention. Our communications platform has been facing rising competition from other prominent players over the years, mainly due to value-added services provided by competitors. Our team aspires to remain competitive and attractive to the wider audience through providing top-notch value-added services by integrating artificial intelligence into our application.

# Problem Statement
To create an emotion classification model for casual text messages sent through our social media platform.

The key emotions of interest are:
- Optimistic
- Anticipation
- Negativity
- Contempt
- Neutral

We will use a mix of quantitative and qualitative evaluation metrics to understand the success of our model:
- **Qualitative**:
    - We understand that text classification for casual conversations has its limitations, particularly regarding slangs, spelling mistakes, sarcasm, human intonation and more, we believe that qualitative evaluation plays a heavy part in determining the success of our model.
    - We will hence be conducting random samples of each predicted emotion classes to check if results, to the human interpretation, makes good sense.
    - We will evaluate the results by fitting our prediction model to actual chat conversations and check if the predicted emotions for each group of messages make sense.
- **Quantitative**: Accuracy, F1, Precision and Recall

# Dataset
As there are limitations on obtaining actual conversations exchanged by individuals that are open-source, due to the intimate nature of texts and privacy issues, we have overcome the shortcoming by using a close substitute: Tweet messages. Messages exchanged through the open architecture are generally informal and casual in nature. Hence, we believe that it is a good substitute for our use case.

##### Main Dataset
This dataset of 40K messages with 13 distinct labeled emotions were extracted from CrowdFlower, a data crowdsourcing platform. Annotation questionnaires were uploaded and annotators have consented to the CrowdFlower terms of agreement before receiving the task. Annotators were compensated for their manual labelling efforts. All annotation tasks were approved by the National Research Council Canada’s Institutional Review Board, which reviewed the
proposed methods to ensure that they were ethical.
Source: [Crowdflower](https://data.world/crowdflower/sentiment-analysis-in-text)

##### Supporting Dataset
Due to the heavy imbalance of the 'anger' class in our dataset after reclassification of our emotions into 5 main categories, I have decided to use an existing tweet dataset that were prepared by a team of students from SUTD for a similar project. This would serve as an additional support to training data.

The team has pulled the angry tweets from Twitter using the Twitter API. They have used the 'hashtag' function to filter for the various emotions, for example "#hate". It is believed that hashtags should be an appreciably good representation of the sentiment of the tweet. [tlkh-github](https://github.com/tlkh/text-emotion-classification)

# Executive Summary
Through diving into the tweets of the 13 original labels of emotions provided by the main dataset, we have recategorised them into 5 main emotion classes: Negativity, Contempt, Neutral, Optimistic and Anticipation.

Our model performed moderately well at classifying our test tweets based on quantitative metrics: Accuracy, F1, Precision and Recall. Our best performing model that was eventually selected for prediction purposes is our Logistic regression, which performed well in all four metrics compared to the other two models that were shortlisted for modelling.
![summary](../data/image/model_summary.png)

However, we note that the scores are not the biggest indicator of model success. We conducted deep analysis into our sampled tweets to understand the nature of misclassification, as well as test it with casual chat conversations to see our affinity with our models' predicted outcome.

![confusion](../data/image/confusion.png)
**Key Model Findings**
- Most of our misclassified tweets and casual text conversations were due to the mislabelling of data by manual annotators. This eventually diluted our model's performance.
    - In fact, for some of the misclassified messages, we instead, lean more towards model's predicted emotion class rather than the manual annotators' labels. However, we understand that understanding tonalities are a subjective matter altogether.
- Model did well in predicting the 'Negativity' class, with a 71% recall (71% of Actual Negativity Tweets are correctly classified).
- Moreover, the classification of tweets in "Contempt" class is also noteworthy with 83% precision. There is a lower score for recall (46%) with most misclassified tweets to predicted to be in "Negativity" class (37%) instead.
- A huge bulk of "Neutral" tweets were misclassified as "Negativity". However, upon further inspections, words that typically carry a sense of 'negativity' with them may be used in other context, that may appear to be neutral. Hence, our model was not able to pick up the nuances in how words are used in different contexts.

**Testing of Data on Casual Chat Conversations**
- From a qualitative evaluation standpoint, our model has predicted the tonalities of our casual chat messages fairly well.
- One of the key flaws in our model was the inability for it to understand contextual meaning of certain words, ie. "sick".
- Another key aspect was the inability to differentiate the same words with different spellings: 'hahahaha','haahaa' etc. as well as stretched words "tireedddddddd" vs. 'tired'.
- "Negativity" class tended to be a catch-all for misclassified classes. Even during our messages tested, many messages that appears to be "neutral" or "anticipatory" were misclassified into "negativity" class.
- In general, our model has performed really well for "Optimistic","Neutral","Anticipation" and "Contempt", as we observe from sampled data.

# Content
- Notebook 1: Data Cleaning and Preprocessing
- Notebook 2: Modelling and Evaluation
- Notebook 3: Fitting Model into Casual Chat Conversations

# Limitations
#### Overall:
- Overarching this project was the limitation of obtaining approved, open-source chat conversations (from Whatsapp, Telegram) for us to build the most accurate model.
    - Even if we have obtained chat conversations, there is an additional, costly, barrier that we have to overcome: labelling the emotions and labelling them *accurately*.
- We have chosen to use tweet dataset as a replacement for actual chat conversations due to the nature of tweets, to be highly casual and conversational in nature, which is a good substitute in predicting emotions in chat conversations.

#### Modelling
- The main limitation of our model was the use of mislabelled data from the manual annotators. There are a large bulk of misclassified data (based on our model) where we lean more towards agreeing with model's prediction instead of the actual labels.
- Natural Language Processing on Casual Chat Conversations tend to have many limitations attached, and is not a straightforward topic:
    - One of the key flaws in our model was the inability for it to understand contextual meaning of certain words, ie. "sick".
    - Another key aspect was the inability to differentiate the same words with different spellings: 'hahahaha','haahaa' etc. as well as stretched words "tireedddddddd" vs. 'tired'.
    - Another area of concern was the potentials to have spelling mistakes and underweighting these words in our model, ie. "goodmorning" (one word) vs. 'good morning' (two words); 'chillin' vs. 'chilling'.

# Areas of Improvement & Next Steps
With our first attempt at building an emotion classification prototype for our communication platform, there are certainly areas of improvements and key learning points that we can takeaway from this attempt.

For the second iteration, we will be suggesting improvements as following:
- To scrape Twitter by filtering hashtags to obtain more relevant content. We would also like to increase the number of tweets in our dataset and ensure a balanced dataset for each emotion class before we start modelling.
- Conduct deep cleansing of our data:
    - Take into account 'stretched words' and their effect on our predictive capabilities. This can be done by filtering for letters that appear consequetively more than 3 times (ie. 'tweeeets'). We can capture this information through another column in our dataframe.
    - Understand some of the commonly mispelled words, ie: 'ahaha', 'hahha' etc.
    - Using Symspell's library to correct the whole dataset to ensure words are correctly sent for model training.
- Conduct more sampling of data to see effectiveness of our model: Currently, our sample size is at 10 tweets.
- Finally, as we attempt to obtain more data from Twitter, we can also look into other emotion classes that are more specific, ie "Disgust", "Horror" or "Fear" that were absent from our current model.

# In a nutshell
Our team believes that this current prototype, as a minimum viable product, suffices the needs of the team for further development of this value-added service. The current model has fared moderately well on test data (actual chat conversations), and is able to predict casual tonalities well.

We will be continuing our efforts to develop a better model with the suggested steps detailed above. Concurrently, we hope to collaborate with the software engineering team in implementation of this new function within our communications platform.
