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

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Problem.PNG)

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
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Pairs.PNG)
  
2. The input and final Job Description's in the 'Input-Output Pair dataset', should be semantically similar to each other. Thus, the similarity between the encoding of these paired dataset should be significntly higher than the similairty between the encodings of the random pairs.

3. To check this we conduct the 2 sample t-test on the sets of Similarity Scores for Actual and Randomly pairedobservations.

4. We obatin sentence encoding using Google-Bert[(Sentence Transformers Package in Python)](https://pypi.org/project/sentence-transformers/). For each JD(Input/Output/Both Sets), we calculate their embedding by averaging the encoding of their sentences. For each pair we calculate the similarity using [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity) from [Sklearn-package](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html).
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/JDEncoding.PNG)


#### T-Test

**H0:** The similarity in Random pairs is same or less than the similarity in Actual pairs.
**Alpha:** 0.05

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/T-Test.png)

**Results:**
T-Statistics: 365.92841
P-Value: 0.0

The results of the T-Test signifies that the similarity in the set with actual pairs is significantly higher than that in the random pair set. Thus, we reject the Null Hypothesis.

**This signififes finding similarity using encoding is significant and reasonable.**

### Generate Sentence Pairs

1. So far, we have calculated similarity on Job Description level. But, ultimately we want to calculate similarity on sentences.
The problem is **Unlike Job Descriptions, we don't have pairs of similar sentences**. 
2. To create these sentence pairs we rely on the assumption that **in a given pair of input-output job description, for each sentence in the input, there lies a sentence in output which can be paired together.**
3. If the assumption is true, for any given input sentence the similarity with most similar sentence in output should be significantly higher than similarity with other senetences.
Thus, we plot the distribution of similarity score with the rank of similarity score.

For each input sentence, we rank the output sentences based on their similarity.
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/RankTable.PNG)

Next, we plot the distribution of similarity scores with the Rank.
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/RankBoxPlot.png)

4. The above plot shows the similarity of Rank1 sentences are significantly higher than that sentences with of other ranks.
Thus, we generate pairs of sentences using these Rank1 pairs.

5. For evaulation of our methods we eliminate sentence pairs with similarity 1 as they are exactly similar, and will act as noise in results. also we eliminate pairs(if any) with similarity less than a threshold(0.8).

### Methods for Sentence Encoding and Evaluation of their performances.

#### Methods:

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/Methods.PNG)


**1. [TF-IDF: Term Frequency-Inverse Document Frequency](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)**
 TFIDF maps how important a word is to a document in a collection or corpus. Using this it creates a vector for the document based on the words present in the document. In our case the sentence is document. We create vector with 1024 dimensions.

**2. Average of [Word2Vec](https://en.wikipedia.org/wiki/Word2vec)**
 Word2Vec maps each word to a high dimensional vector. In our case we average the vectors of words in the sentence to generate sentence vector. We have used the pretrained [Google Word2Vec model](https://mccormickml.com/2016/04/12/googles-pretrained-word2vec-model-in-python/)
 
**3. [InferSent](https://github.com/facebookresearch/InferSent)**
InferSent is a sentence embeddings method developed by Facebook Research Group, and provides semantic representations for English sentences. It is trained on natural language inference data and generalizes well to many different tasks.
Again we have used the pretrained model provided by the group.

**4. [Bert-Nli](https://ai.googleblog.com/2018/11/open-sourcing-bert-state-of-art-pre.html)**
Till recent times, Google Bert was the state-of-the art method for Natural Language Inference.
We use the pretrained model provided in the [Sentence-Transformer](https://pypi.org/project/sentence-transformers/) python package.

**Please Note: We have not trained any of the above-mentioned methods on our datasets. All results are produced using the pretrained weights.**

#### Evaluation:

In our system, for each input sentence, we have to provide suggestion of top-n similar sentences. Ranking might or might not be important for these suggestion. Based on this criteria we use 2 evaulation metric.

**Please note: For the top-n suggestions based on similarity with input sentence, the relevance for evaluation is calculated using the similarity of the suggestion with the paired output sentence.**

**1. [Cumulative Gain](https://en.wikipedia.org/wiki/Discounted_cumulative_gain)**
It is based on the assumption, rank of suggestion is not important.</br>
It provide the sum of releveances of all suggestions.</br>
Cutoff value(n) of 1,5, & 10 is used.</br>
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/CG.PNG)

**2. [Normalized Discounted Cumulative Gain](https://en.wikipedia.org/wiki/Discounted_cumulative_gain)**
It is based on the assumption, rank of suggestion is important.</br>
NDCG varies between 0 to 1, with 1 being the best performance.</br>
Cutoff value(n) of 1,5, & 10 is used.</br>
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/DCG.PNG)
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/IDCG.PNG)
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/NDCG.PNG)

### Results

#### Cumulative Gain Results
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/cg_results.png)

#### Normalized Cumulative Gain Results
![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/ndcg_results.png)

### Final Example

**Input:**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/FinalInput.PNG)

**Output:**

![Image description](https://github.com/Shivam0712/PracticalApplication_SentenceEncoding/blob/master/Images/FinalOutput.png)

### Conclusion


 
