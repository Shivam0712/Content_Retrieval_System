# PracticalApplication_SentenceEncoding

Sentence Encoding helps to represent any sentence as a numerical vector, thus, making it possible to use mathematical operations on it.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/SentEnc.PNG)

The notable applications of sentence encoding are:
1. Text Classification (Sentiment Analysis).
2. Text Similarity Measurements. (Use of BERT in Google Search Engine).

But beyond, sentiment analysis and use in giant Search Engines, Sentence encoding hold immense potential to impact/increase the efficiency of business processes in medium and small size companies, specifically startups.

In this project, I have demonstrated a prototype that uses sentence encoding to develop a system for 'Automatic Job Description Filler'.

## Problem Description:

1. To develop 'Automatic Job Description Filler' for a Indian platform which collects 'Job Descriptions' from employers, process it, and finally post it on their website.

2. One of the most time consuming and labor-intensive task in this process is to clean and process these job descriptions written by employer.

3. Currently, this process is done manually, where 6 to 8 people spend 8 hours a day. They clean these inputs, break them into sentences, finding similar sentences from previous published JD's, and finally compile it to make the publishable job description.

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/IOJD.PNG)

4. Our system will automate the labor-intensive task. The system will clean the input, form sentences, extracting similar sentences from past, and provide all this information to the admin for final check and compilation.

## Data Description

We have 2 datasets for solving this problem:

1. **Corpus:** Previous published Job Descriptions without the information of employers input. We need to extarct similar sentence from this corpus. **(Size: 400k JD's)**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/corpus.PNG)

2. **Input-Output Pair** Previous published Job Descriptions with the information of employers input. We will use this to build and validate our system. **(Size: 40k Pairs)**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Pair.PNG)

## Suggested System Design
