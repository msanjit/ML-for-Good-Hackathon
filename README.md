# ML-for-Good-Hackathon
# Team Details 
  - **Name**: VCare(or Team 20)
  - **Team Members**:  Sanjit Mehta, Naveena Chandwani, Rohith Rathod

# Preprocessing of Data

- ### Information extraction: 
    By going through the conversation between Moderator and Parents from the given word document on Focus groups, we manually extracted questions and answers in the form of structure data(CSV file). Extracted CSV Data - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation)
    - ### Extracted Data Dictionary:
    
        | Column_name | Data_type   | Description |
        | ----------- | ----------- | ----------- |
        | focus_group_subtype      | Text       |Name of the Focus group(Eg: Media, Social, Gaming, Low PIU)
        | focus_group_subtype_id      | Integer       |Number given to each Focus group(Eg: 1,2,3,4...)
        | doc_no_within_subtype      | Integer       |Number given to each word document under Focus group(Eg: 1,2,3,4...)
        | question_id      | Integer       |Number given to each question asked by the Moderator to Parent(Eg: 1,2,3,4...)
        | question_text      | Text       |Question asked by the Moderator
        | parent_num      | Integer       |Number give to each parent(Eg: 1,2,3,4...)
        | parent_answer      | Text       |Answer given by the Parents

- ### Normalizing/Cleaning Data: 
    Following methods are used for Data preprocessing. Python Code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/Data_preprocessing.ipynb) 
    - Expand contraction
    - Case Handling
    - Remove punctuations
    - Remove words and digits containing digits
    - Remove stop word
    - Lemmatization
    - Remove Extra Spaces
# Sentiment Analysis

- ### Background
	- We have performed unsupervised sentiment analysis on Focus group dataset to classify parents response to the questions as Positive or Negative
	- The main idea behind this approach is that negative and positive words usually are surrounded by similar words. This means that if we would have movie reviews dataset, word ‘boring’ would be surrounded by the same words as word ‘tedious’, and usually such words would have somewhere close to the words such as ‘didn’t’ (like), which would also make word didn’t be similar to them. 
	- On the other hand, it would be unlikely to have happened, that word ‘tedious’ had more similar surrounding to word ‘exciting’, than to word ‘boring’. 
	- With such assumption, words could form clusters (based on similarity of their surrounding) of negative words that have similar surroundings, positive words that have similar surroundings, and some neutral words that end up between them (such as ‘movie’).
	- We used gensim’s implementation of word2vec algorithm with CBOW(Common Bag of words) architecture for this work.
- ### Input data
	- Extracted data in CSV format as described in Preprocessing of Data
	- Input CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation)
- ### Code Details
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/unsupervised_sentiment_analysis.ipynb) 
- ### Ouput data
	- We have added one new column(Column name: Sentiment) to the input data, which basically conveys the Sentiment of Parent(Positive/Negative) to the questions asked by the Moderator on Covid crisis
	- Output CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/outputs/focus_group_sentiment_output.csv)
- ### Resource
	- Blog - [Click Here](https://towardsdatascience.com/unsupervised-sentiment-analysis-a38bf1906483)
	- Github link - [Click Here](https://github.com/rafaljanwojcik/Unsupervised-Sentiment-Analysis)
