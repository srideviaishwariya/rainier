# Natural Language Processing with Disaster Tweets

# Why is this important 

We all know about the "Boy who cried Wolf", and it's equivalent tweets such as "its shaking in San Francisco" which could mean its fun being in SF or an earthqauke.

In any disaster situation avaliabiltiy of the first responder could make the difference between life and death. Last year when there was severe weather system in Bayarea, crowd sourced tweets did a better job in giving updates on flood zones then any other medium. For a disaster management system supporting First-responders team its important to understand when a tweet signals an actual disaster.

I am using NLP(Natural Language Processing) to build a machine learning model to uncover valuable insights and connections in tweets. The goals are, 
- Uncover valuable insights about ongoing Disasters from Tweets 
- Simplify document processing workflows by extracting text, key phrases, and sentiment
- Classify documents(Tweets) and identify patterns

# Data Sources

I am using the disasters Tweets data from the "Natural Language Processing with Disaster Tweets" project in Kaggle. 
https://www.kaggle.com/competitions/nlp-getting-started/overview 

## Data Insights 

The csv is made up of the following 4 columns:
- id: a unique identifier of every tweet
- keyword: a particular keyword from the tweet (this can be blank)
- location: the location the tweet was sent from (this can be blank)
- text: the text of the tweet
- target: present only in the train data, and denotes if the tweet is about a real disaster (1) or not (0)

The Training dataset contains the target information while the test doesn't contain it. There are null values in keyword and location columns 

# Techniques

NLP is an exciting field with new tools released everyday for processing and understanding the semantic meaning of both written and spoken text. The following are the techniques used in this project,

## 1. Text Procesing 
In any NLP project, text preprocessing is one of the first steps before building the machine learning model. This step consists of cleaning and preparing text data before encoding them in the form of numeric vectors.

- Remove all irrelevant characters such as any non alphanumeric characters
- Removing stop words that are non-meaningful words like “the” and “and” from text data.
- Tokenize your text by separating it into individual words
- Remove words that are not relevant, such as “@” twitter mentions or urls
- Convert all characters to lowercase, in order to treat words such as “hello”, “Hello”, and “HELLO” the same
- Consider combining misspelled or alternately spelled words to a single representation (e.g. “cool”/”kewl”/”cooool”)
- Consider lemmatization (reduce words such as “am”, “are”, and “is” to a common form such as “be”)

I used NLTK(https://nltk.org/) library for text processing. 

## 2. Fill missing Keyword 

Given we have the Twitter text, filling the missing keyword is essentially extracting the keyword from the tweet. There are multiple tools available for it, 

- RAKE - Rapid Automatic Keyword Extraction (RAKE) is a well-known keyword extraction method which uses a list of stopwords and phrase delimiters to detect the most relevant words or phrases in a piece of text.
- YAKE - A light-weight unsupervised automatic keyword extraction method 
- BERT keyword extractor from hugging face https://huggingface.co/yanekyuk/bert-keyword-extractor.

I compared both YAKE and BERT and dcided to go with BERT through they both were giving very similiar Keyword results. 

An observation from the keyword generation, some of the keywords generated were not relevant and would require more fine-tuning or manual intervention to get the results that is required 

## 3. Understand the sentiment behind the tweets 
TBD

## 4. Create an Embed for the Text 
Machine Learning models take numerical values as input. Converting the string to a numerical vector is the first step in training a Model. For this purpose I explored the following tools,
- BERT Embeddings 
- Huggingface embed with various models 
- One-hot encoding (Bag of Words)

## 5. Visualise the Embeddings 
In order to see whether our embeddings are capturing information that is relevant to our problem (i.e. whether the tweets are about disasters or not), it is a good idea to visualize them and see if the classes look well separated. Since vocabularies are usually very large and visualizing data in 20,000 dimensions is impossible, techniques like PCA will help project the data down to two dimensions. This is plotted below.

## 6. Classification 
I am using the following tools for classification 
- KNN 
- Logistic regression 

## 7. Validation of the Results 
It is important to understand the accuracy of the model this is done using a Confusion Matrix. The goal here is to build a model with the following attributes, 

- Build predictive model with 75% accuracy
- Build predictive model with 75% recall
- Build predictive model with 75% precision

## 7. Get results for the Test Data and post to Kaggle 
TBD

# Expected Results

Build a model that could predict the validity of a tweet as a true indicator of an ongoing disaster. 

# References 
https://blog.insightdatascience.com/how-to-solve-90-of-nlp-problems-a-step-by-step-guide-fda605278e4e 
https://medium.com/analytics-vidhya/introduction-to-nlp-with-disaster-tweets-3b672a75748c
https://www.kaggle.com/code/alexia/kerasnlp-starter-notebook-disaster-tweets/notebook
https://www.kaggle.com/code/jessicaval/disaster-tweets-prediction-logreg-embeddings
https://huggingface.co/
https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270
https://www.nltk.org/
