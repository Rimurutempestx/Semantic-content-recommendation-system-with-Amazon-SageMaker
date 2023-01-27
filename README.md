# Semantic-content-recommendation-system-with-Amazon-SageMaker
Built a semantic, content recommendation system that combines topic modeling and nearest neighbor techniques for information retrieval using Amazon SageMaker built-in algorithms for Neural Topic Model (NTM) and K-Nearest Neighbor (K-NN).



## Overview
"Information retrieval is the science of searching for information in a document, searching for documents themselves, or searching for metadata that describe data. This combines the techniques of topic modeling and nearest neighbor for information retrieval. This approach uses topic modeling to generate semantic distribution vectors representing the meaning of documents by topics, and then uses the nearest neighbor technique to index topic vectors to retrieve similar documents for a given input document based on topic similarity. By using Amazon SageMaker built-in algorithms, you do not need to label data and the information retrieval is based on semantic meaning similarity instead of simple string matching."

![image](https://user-images.githubusercontent.com/106786020/214730815-3beaae43-9960-445d-837a-07da83ae1072.png)



## Basic initial setup 
To start things off I just made a basic S3 bucket and configured all the settings for it. Then started off by making a SageMaker Notebook instance, this was my first time making a notebook instance in the almost five years that I've been using AWS. Everything was pretty straight forward it was almost like creating any regular instance, the only thing that caught my eye is that the notebook instance has a preconfigured Jupyter notebook server and a set of Anaconda libraries. I then created a new Jupyter notebook in JupyterLab and saved.



## Download and prepare dataset
I started by fetching the dataset which didn't take to long. I just imported some libraries and defined a few environment variables in my notebook environment (Fetch data set code file). Then I started by setting up the reproccessing data code, to process raw text data into machine readable numeric values. First, I used the APIs provided by scikit-learn to strip any headers, footers and quotes from the dataset. Then I defined the code in my Jupyter notebook (strip headers, footers, and quotes file).
