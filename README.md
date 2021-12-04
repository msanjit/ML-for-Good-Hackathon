# ML-for-Good-Hackathon
# Team Details: 
  - Name: VCare(or Team 20)
  - Team Members:  Sanjit Mehta, Naveena Chandwani, Rohith Rathod

# Preprocessing of Data

- ### Information extraction: 
    By going through the conversation between Moderator and Parents from the given word document on Focus groups, we manually extracted questions and answers in the form of structure data(CSV file). Extracted Data - [link](https://github.com/msanjit/ML-for-Good-Hackathon/tree/main/vcare/data_preparation)
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
    Following are the Data preprocessing methods followed. Code - [link](https://github.com/msanjit/ML-for-Good-Hackathon/blob/main/vcare/notebooks/Data_preprocessing.ipynb) 
    - Expand contraction
    - Case Handling
    - Remove punctuations
    - Remove words and digits containing digits
    - Remove stop word
    - Lemmatization
    - Remove Extra Spaces
