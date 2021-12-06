# ML-for-Good-Hackathon
# Team Details 
  - **Name**: VCare(or Team 20)
  - **Team Members**:  Sanjit Mehta, Naveena Chandwani, Rohith Rathod

### The NLP tasks performed are as follows-
#### 1] NLP Pre-processing pipeline
#### 2] Clustering and Sentiment analysis on Unstructured data
#### 3] Conversational summarization
#### 4] Emotion analysis
#### 5] Agglomerative and K-Means Clustering on Structured data
#### 6] Identifying outliers in data and feature creation followed by Predictive analytics on Structured data


# Ideas-
## 1] FocusGroups data related work -
### This data captures conversations wherein different questions/answers about pre-pandemic, pandemic, post-pandemic/return-to-school/work and group-specific situations have been discussed.  
- The 4 groups are-
1] Gaming_Group
2] Social_Group
3] LowPIU_Group
4] Media_Group

### Our work involves performing various tasks to gain insights and derive meaning from these conversations in order to help the survey participants better and also to be able to understand the pattern among similar groups in the future


# Preprocessing of Data

- ### Information extraction: 
    By going through the conversation between Moderator and Parents from the given word document on Focus groups, we manually extracted questions and answers in the form of structure data(CSV file). Extracted CSV Data - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation)
	Later rules can be built to detect patterns based on length of the questions asked by the moderator, regex for  parent number, etc. and creation of such a structured file can be automated
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
	

# Conversational summarization

- ### End goal
	- Forming a sub-convo for each question asked by moderator and the various answers given by the parents.
	- Running a summarizer to capture the info from each such sub-convo.
	- This will be very useful to filter out the unnecessary text at the beginning and end of each conversation and to focus on the important text for analysing the survey responses.	
- ### Input data	
	- Input CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation/focus_groups_convos.csv)
- ### Code Details
    - Both Abstractive and Extractive Summarization have been tried
	- Abstractive summarization using Transformer's T5 model
	- Extractive Implementation includes aggregating data at a question level and running through 3 pre-trained models-
	BERT, XLNET, GPT2
	- Based on preliminary runs and results for Extractive Summarization, individual models gave average results and each missed important aspects.
	- All of them had some common content. So the idea here is to use an Ensemble model like technique to combine the results from each of these individual 'weak' models
	and to aggregate them to in such a way that more variation is captured
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/T5_for_summarization_naveenac.ipynb)
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/pre_trained_models_summaries_for_sub_convos.ipynb)
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/BERT_GPT2_XLNET_for_summarization_naveenac.ipynb)
- ### Ouput data	
	- Output CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/outputs/)
- ### Resource
	- https://huggingface.co/docs/transformers/main_classes/pipelines#transformers.SummarizationPipeline	


# Emotion Analysis

- ### End goal
	- Emotion analysis for text (per group per question per parent's response)
	- This can then be aggregated-
		1] at a parent level - to obtain the various emotions felt by each parent
		2] at a question level - to obtain the various emotions experienced by parents for each question asked by the moderator
		3] at a group level - by combining all the emotions across all questions
	- Emotion labels-
	['serenity', 'joy', 'disgust', 'anxious', 'optimism', 'vigilance', 'sad', 'fear']
	Thus, this will help in capturing a wide range of emotions and varying degrees of an emotion (based on Plutchik's wheel of emotion)
- ### Input data	
	- Input CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation/focus_groups_convos_emotion_analysis.csv)
	- Input CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation/focus_groups_convos_emotion_analysis_test.csv)
- ### Code Details
	- Fine-tuning pre-trained BERT for Sequence Classification model using Torch and Trainer Class
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/emotions_analysis.ipynb)
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/emotions_analysis_test.ipynb)


## 2] ProlificAcademic data related work -
- ### This section uses Structured data based on surveys conducted on adults and parents during different periods of the pandemic such as April 2020, May 2020, November 2020, 	  April 2021. 

# Agglomerative and K-Means Clustering
- ### This was performed to identify common groups of individuals and correlations

# Predictive Analytics-
- ### Unifying the various datasets
- ### Identifying outliers in data and feature creation 
- ### Predictive analytics using GradientBoosting to look out for markers for more worry, role of substance abuse, etc.
- - ### Input data	
	- Input CSV file - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/tree/master/Data/ProlificAcademic)
- ### Code Details	
	- Jupyter notebook link for Python source code - [Click Here](https://github.com/msanjit/ML-for-Good-Hackathon/blob/master/vcare/notebooks/crisis_prolific_analysis_v1.ipynb)
