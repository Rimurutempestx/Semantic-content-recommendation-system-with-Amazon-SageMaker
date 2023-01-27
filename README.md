# Semantic-content-recommendation-system-with-Amazon-SageMaker
Built a semantic, content recommendation system that combines topic modeling and nearest neighbor techniques for information retrieval using Amazon SageMaker built-in algorithms for Neural Topic Model (NTM) and K-Nearest Neighbor (K-NN).



## Overview
"Information retrieval is the science of searching for information in a document, searching for documents themselves, or searching for metadata that describe data. This combines the techniques of topic modeling and nearest neighbor for information retrieval. This approach uses topic modeling to generate semantic distribution vectors representing the meaning of documents by topics, and then uses the nearest neighbor technique to index topic vectors to retrieve similar documents for a given input document based on topic similarity. By using Amazon SageMaker built-in algorithms, you do not need to label data and the information retrieval is based on semantic meaning similarity instead of simple string matching."

![image](https://user-images.githubusercontent.com/106786020/214730815-3beaae43-9960-445d-837a-07da83ae1072.png)



## Basic initial setup 
To start things off I just made a basic S3 bucket and configured all the settings for it. Then started off by making a SageMaker Notebook instance, this was my first time making a notebook instance in the almost five years that I've been using AWS. Everything was pretty straight forward it was almost like creating any regular instance, the only thing that caught my eye is that the notebook instance has a preconfigured Jupyter notebook server and a set of Anaconda libraries. I then created a new Jupyter notebook in JupyterLab and saved.



## Download and prepare dataset
I started by fetching the dataset which didn't take to long. I just imported some libraries and defined a few environment variables in my notebook environment (Fetch data set code file). Then I started by setting up the reproccessing data code, to process raw text data into machine readable numeric values. First, I used the APIs provided by scikit-learn to strip any headers, footers and quotes from the dataset. Then I defined the code in my Jupyter notebook (strip headers, footers, and quotes file). After seeing the data was simply play text paragraphs after running the code. In order for this to be machine readable, I needed to "tokenize” this data to numeric format by assigning a “token” to each word in the sentence. Then I limited the total number of tokens to 2000 by first counting the most frequent tokens and only retaining the top 2000. "This limiting is in place because less frequent words will have a diminishing impact on the topic model and can be ignored. Then, for each of the documents you use a Bag of Words (BoW) model to convert the document into a vector which keeps track of the number of times each token appears in that training example.".


Then I used WordNetLemmatizer, a lemmatizer from the nltk package, and used CountVectorizer in scikit-learn to perform the token counting. WordNetLemmatizer uses nouns as the parts of speech (POS) for lemmatizing words into lemmas. Lemmatization aims to return actual words whereas stemming, another preprocessing approach, can often return non-dictionary words or root stems which are often less useful in machine learning. In the list comprehension, I implemented a simple rule: only consider words that are longer than 2 characters, start with a letter and match the token_pattern (tokenizer define, token counting, limiting the vocab_size to 2000 file.). Then imported the CountVectorizer API (CountVectorizer API file). The CountVectorizer API uses three hyperparameters that can help with overfitting or underfitting while training a subsequent model. The first hyperparameter is max_features which you set to be the vocabulary size. As noted, a very large vocabulary consisting of infrequent words can add unnecessary noise to the data, which will cause you to train a poor model. The second and third hyperparameters are max_df and min_df. The min_df parameter ignores words that occur in less than min_df % documents and max_df ignores words that occur in more than max_df % of the documents. The parameter max_df ensures that extremely frequent words that are not captured by the stop words are removed. Generally, this approach is a good practice as the topic model is trying to identify topics by finding distinct groups of words that cluster together into topics. If a few words occur in all of the documents, these words will reduce the expressiveness of the model. Conversely, increasing the min_df parameter ensures that extremely rare words are not included, which reduces the tendency of the model to overfit.  To generate training and validation sets, you first shuffle the BOW vectors generated by the CountVectorizer API. While performing the shuffle, you keep track of the original index as well as the shuffled index. 


Next it was time to stage the training and validation datasets in S3. I started by converting the vectors to a sparse representation (Convert vectors to sparse file).
