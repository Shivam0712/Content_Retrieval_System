# PracticalApplication_SentenceEncoding

Sentence Encoding helps to represent any sentence as a numerical vector, thus, making it possible to use mathematical operations on it.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/SentEnc.PNG)

The notable applications of sentence encoding are:
1. Text Classification (Sentiment Analysis).
2. Text Similarity Measurements. (Use of BERT in Google Search Engine).

But beyond, sentiment analysis and use in giant Search Engines, Sentence encoding hold immense potential to impact/increase the efficiency of business processes in medium and small size companies, specifically startups.

In this project, I have demonstrated a prototype that uses sentence encoding to develop a system for 'Automatic Job Description Filler'.

## Problem Description:

1. An Indian platform collects 'Job Descriptions' from employers, process it, and post it on website. One of the most time consuming and labor-intensive task in this process is to clean and process these job descriptions written by employers.

2. Currently, this process is done manually, where 6 to 8 people spend 8 hours a day. They clean these inputs, break them into sentences, finding similar sentences from previous published JD's, and finally compile it to make the publishable job description.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/IOJD.PNG)

**In this project, we have designed a system which cleans the input, forms sentences, and uses sentence encoding to extract similar sentences from the past published JD's.**

## Data Description

We have 2 datasets for solving this problem:

1. **Corpus:** Previous published Job Descriptions without the information of employers input. We extarct similar sentence from JD's in this corpus. **(Size: 400k JD's)**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/corpus.PNG)

2. **Input-Output Pair** Previous published Job Descriptions with the information of employers input. We will use these to build and validate our system. **(Size: 40k Pairs)**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Pair.PNG)

## Suggested System Design

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/SystemDesign.PNG)

## Text Cleaning and Forming Sentences
1. We remove undesirable characters, punctuations, and bulletins.
2. Use periods and the line brakes to decompose the text into sentences.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/TextClean.PNG)

## Sentence Encoding and Text Similarity
1. **Significance of Similarity:** We need to validate Sentence Encoding leads to meaningful representation vector and thus, the similarity calculated using it is significant and not random.
2. **Generate Sentence Pairs:** To develop and evaluate methods for extracting similar sentences we need to have a reference set of similar sentences pair.
3. **Evaluation:** We need to evaulate different methods for Sentence Encoding and select the best one.

### Significance of Similarity

1. We generate 2 paired sample sets: <br/>
  a. **Actual Pair:** We take actual pairs of input and final JD from Input-Output Pair dataset.<br/>
  b. **Random Pair:** We randomly pair the input JD's with final JD's in Input-Output Pair dataset.

2. We clean these samples, form sentences for each observation in both the sample sets.
3. We obatin sentence encoding using Google-Bert(Sentence Transformers Package in Python)(Link). For each JD(Input/Output/Both Sets), we calculate their embedding by averaging the encoding of their sentences.
4. For each pair we calculate the similarity using Cosine Similarity(Link) from Sklearn-package(Link).
5. On the sets of Similarity Score of Actual Pairs and Random Pairs, we conduct 2 sample t-test to test if the 2 sets are significantly different. 

