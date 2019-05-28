---
layout: post
title: nlp project
date: '2010-11-16 03:40:00'
tags:
- artifical_inteligence
---

Polarity Detection of movie reviews 
Introduction :- 
Today, very large amounts of information are available in on-line documents. As part of the effort to better organize this information for users, researchers have been actively investigating the problem of automatic text categorization. In Polarity detection in movie reviews, The basic problem is to classify a movie review as positive or negative. Some training data set is provided and we have to develop the best technique to classify them into their respective classes. This would be very useful in knowing the defects in a product. If a customer had decided to purchase a product and is willing to know only the defects of a product rather than concentrating on parts which emphasize it. This classification process would be very 
helpful. Similarly we have many other scenarios like ad generation which would depend on polarity detection. 

Proposed approach :- 
Data Set :- Data set used for this project would be 1400 movie reviews classified for 
their polarity. 
Preprocessing :- The given data may have some irrelevant and noisy things. Which can be eliminated by applying some techniques. These application of techniques would increase the accuracy. 
Part of Speech Tagging: Tagging Each words in the data set with its part of speech using Some standards like penntree bank or some other methods. These different combinations of part of speech tags, those more related to describing a sentiment for our further operation. as from general observation it is noted that Adjectives are the good features for polartiy detection. 
Stop words: Also known as noise words, are words which are of not much significance in context of categorization and sentiment analysis. Eg.: articles, conjunctions, etc. We need to remove all the stop words from our data set and produced a new data set. 

Stemming: Stemming is the process of changing a words to its root or base form, by removing inflexions ending from words in English.( porter stemmer algorithm) There are also few other preprocessing techniques like quote-weighting, html-tag filter and non-English review filter. which can be applied depending on the data present. As from previous experimental evaluation, it was discovered that the frequency and presence of a particular feature for polarity detection dint had much effect. So, I am not yet decided but thinking to consider only the presence of a particular feature. 

I am thinking to use the following lexical features to decide the polarity 
Combination of a word and its part-of-speech tag 
Bigram words 

Unigram words 

considering the words before adjective as collocation... because we have some word with negation before like agree and not agree.... 

part-of-speech tag 
I am still working on using some other lexical features. I would inform them as the project progress. 

Naive bayes :- 
One approach to text classification is to assign to agiven document 
d the class c∗ = arg maxc P (c | d).We derive the Naive Bayes (NB) classifier by first 
observing that by Bayes’ rule, 
P (c | d) = P (c)P (d | c) / P (d) 
where P (d) plays no role in selecting c∗ . To estimate the term P (d | c), Naive Bayes 
decomposes it by assuming the fi ’s are conditionally independent.