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

Examples
- people died heat wave far
    - Keyword from BERT - [{'entity': 'B-KEY', 'score': 0.9998497, 'index': 3, 'word': 'heat', 'start': 12, 'end': 16}, {'entity': 'I-KEY', 'score': 0.9999114, 'index': 4, 'word': 'wave', 'start': 17, 'end': 21}]
    - Keyword from YAKE - [('people', 0.15831692877998726)]
- haha south tampa flooded hah wait second live south tampa am gon na am gon na fuck
    - Keyword from BERT - []
    - Keyword from YAKE - [('gon', 0.07571113878390312)]

The keyword generation needs to be modified to detect the disaster words as keywords. Currently both the models are not giving relevant keyword in both the cases and could be detrimental to analysis

## 3. Understand the sentiment behind the tweets 

Used the Huggingface sentiment analyser.

Example 
- giant cranes holding bridge collapse nearby homes
    - Sentiment - [{'label': 'NEGATIVE', 'score': 0.9995463490486145}]
- control wild fires california northern part state troubling
    - Setiment - [{'label': 'NEGATIVE', 'score': 0.9941936135292053}]

A KNN classification to determine if the sentiment and the score are a good indicator of the prediction for disaster yields an accuracy score of 56% which makes sentiment a poor indicator of an incident in this dataset. 

## 4. Create an Embed for the Text and use Classification algorithm
Machine Learning models take numerical values as input. Converting the string to a numerical vector is the first step in training a Model. For this purpose I explored the following tools,
- Using CountVectorizer to create a bag of words representation of text (vector dimensions = 900).
    - Test set Accuracy Score:  0.7751605995717344
    - Training set Accuracy Score:  0.8421710408855562
    - Recall Score:  0.7353187919463087
    - Average Precision Score:  0.7552376374376963
- Using TF-IDF (term frequency-inverse document frequency) (vector dimensions = 900).
    - Test set Accuracy Score:  0.7794432548179872
    - Training set Accuracy Score:  0.8289591144438493
    - Recall Score:  0.7135067114093959
    - Average Precision Score:  0.7361504637616629
- Using Word2Vec
This was a good learning exercise and covered 
    - Learning to train a model 
    - Learning to create an embedding vector 
    - Using KNN for training with ember vector 
        - Solving for the problem with the 2D array size mismatch 
    - Overall the scores from the Word2Vec did not look promising. Retraining with a different model could produce better results 
        - Test set Accuracy Score:  0.5728051391862955
        - Training set Accuracy Score:  0.5743617211212283
        - Recall Score:  0.0
        - Average Precision Score:  0.42563827887877165

I am using the following tools for classification 
- KNN 
- Logistic regression 


## 7. Validation of the Results 
It is important to understand the accuracy of the model this is done using a Confusion Matrix. The goal here is to build a model with the following attributes, 
- Build predictive model with 75% accuracy
- Build predictive model with 75% recall
- Build predictive model with 75% precision

The Bag of Words and TF-IDF yeilded results which was more the then scores we had planned for the Model. 

# Addtional Exploration 
## 1. Retrieval Augmented Generation (RAG) Architecture 

There are two code snippets for RAG model implementation using Huggingface and Langchain. I couldn't get the results in Langchain due to 429 errors from OpenAPI. 
(additional inforomation explainging the architecture and usage is in the Jupyter notebook)

## 2. Retrieval-Augmented Generation vs. Semantic Search

The Example uses FAISS(Facebook AI Similarity Search) to build the semantic search
(additional inforomation explainging the architecture and usage is in the Jupyter notebook)

## 3. BERT Embedding 
The Example uses pytorch with BERT
(additional inforomation explainging the architecture and usage is in the Jupyter notebook)

# Expected Results

Use the Capstone project to explore the world of NLP!! :D   

# References 
- https://blog.insightdatascience.com/how-to-solve-90-of-nlp-problems-a-step-by-step-guide-fda605278e4e 
- https://medium.com/analytics-vidhya/introduction-to-nlp-with-disaster-tweets-3b672a75748c
- https://www.kaggle.com/code/alexia/kerasnlp-starter-notebook-disaster-tweets/notebook
- https://www.kaggle.com/code/jessicaval/disaster-tweets-prediction-logreg-embeddings
- https://huggingface.co/
- https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270
- https://www.nltk.org/
- https://patil-aakanksha.medium.com/top-5-pre-trained-word-embeddings-20de114bc26
- https://www.kaggle.com/code/pierremegret/gensim-word2vec-tutorial 
- https://www.analyticsvidhya.com/blog/2022/01/embedding-techniques-on-text-data-using-knn/
- https://arxiv.org/abs/2005.11401
- https://docs.aws.amazon.com/sagemaker/latest/dg/jumpstart-foundation-models-customize-rag.html 
- https://www.singlestore.com/blog/a-guide-to-retrieval-augmented-generation-rag/
- https://huggingface.co/docs/transformers/model_doc/rag