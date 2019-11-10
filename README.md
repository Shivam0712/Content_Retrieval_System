# PracticalApplication_SentenceEncoding

The past few years have been revolutionary time for Natural Language Processing, specifically Language Modelling. Several groundbreaking research works have been published, with each pushing the state-of-art at an astonishing pace.

Sentence Encoding is a critical use case of the Natural Language Understanding model.
It helps to represent any sentence as a numerical vector, thus, making it possible to use mathematical operations on it.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/SentEnc.PNG)

The notable applications of sentence encoding are:
1. Text Classification, which has a widespread utilization for sentiment analysis.
2. Text Similarity measurements. Google recently announced that they would be using BERT in their search engine. Up to some extent, this will utilize the application of text similarity.

But beyond, text classification and applications by big giants like Google, Natural Language Models and Sentence encoding hold immense potential to impact/increase the efficiency of business processes in medium and small size companies, specifically startups.

In this project, I have demonstrated how the sentence encoding has helped to develop a system for 'Automatic Job Description Filler' for a job aggregator platform in India.

## Problem Description:

The company collects 'Job Descriptions' from employers, clean and process it, and finally post it on their website, from where the users can access these job vacancies. 

One of the most time consuming and labor-intensive task in this process is to clean and process these job descriptions written by employer.

Currently, this process is done manually, where 6 to 8 people spend 8 hours a day. They clean these inputs, break them into sentences, finding similar sentences from previous published JD's, and finally compile it to make the publishable job description.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/IOJD.PNG)

We want to develop a system to automate all steps before compilation.  Thus, the system should be capable of cleaning the input, forming sentences, extracting similar sentences from the repository, and provide all this information to the admin for final check and compilation.

## Data Description

We have 2 datasets for solving this problem:

1. **Corpus:** Previous published Job Descriptions without the information of employers input. We need to extarct similar sentence from this corpus.(Size: 400k JD's)

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/corpus.PNG)

2. **Input-Output Pair** Previous published Job Descriptions with the information of employers input. We will use this to build and validate our system.(Size: 40k Pairs)
few examples image

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Pair.PNG)

## Suggested System Design
