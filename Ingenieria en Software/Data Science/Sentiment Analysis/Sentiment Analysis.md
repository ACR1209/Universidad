A formal definition of a sentiment analysis problem would be: 
-   **Input**: - A document d - A fixed set of classes $C = {c1,c2,..,cn}$  
-   **Output**: A predicted class $c$ $\in$ C

So, a training set of n labeled documents looks like: _$(d1,c1), (d2,c2),...,(dn,cn)$_ and the ultimate output is a learned classifier. Where a document is a text to be able to classify (tweets, comments, movie reviews, etc. )

One crucial point you need to keep in mind while working in sentiment analysis is not all the words in a phrase convey the sentiment of the phrase. Words like "I", "Are", "Am", etc. do not contribute to conveying any kind of sentiments and hence, they are not relative in a sentiment classification context. Consider the problem of feature selection here. In feature selection, you try to figure out the most relevant features that relate the most to the _class label_. That same idea applies here as well. Therefore, only a handful of words in a phrase take part in this and identifying them and extracting them from the phrases prove to be challenging tasks. But don't worry, you will get to that.

Consider the following movie review to understand this better:

"_I love this movie! It's sweet, but with satirical humor. The dialogs are great and the adventure scenes are fun. It manages to be romantic and whimsical while laughing at the conventions of the fairy tale genre. I would recommend it to just about anyone. I have seen it several times and I'm always happy to see it again......._"

Yes, this is undoubtedly a review which carries positive sentiments regarding a particular movie. But what are those specific words which define this positivity?

Retake a look at the review.

"_I **love** this movie! It's **sweet**, but with **satirical** humor. The dialogs are **great** and the adventure scenes are **fun**. It manages to be **romantic** and **whimsical** while laughing at the conventions of the fairy tale genre. I would **recommend** it to just about anyone. I have seen it several times and I'm always **happy** to see it **again**......._"

You must have got the clear picture now. The bold words in the above piece of text are the most important words which construct the positive nature of the sentiment conveyed by the text.

## Using [[Naive Bayes Algorithm]] for Sentiment Analysis
For a document **d** and a class **c** we will have the following formular

$$P(c|d)=\frac{P(d|c)P(c)}{P(d)}$$
In this case the classes are comprised of two **positive or negative**

Note that the usage of [[Naive Bayes Algorithm]] helps to find which class is more likely to be getting the maximum posterior probability of all the classes for a given document and taking the biggest as the prediction:

![[Pasted image 20220618182650.png]]

>[!NOTE]
>In this case you can drop the denominator because the probability of the document ($P(d)$) doesn't help to calculate $P(c|d)$.

## Implementing Sentiment Analysis with [[Naive Bayes Algorithm]] in Python

	import nltk
	from nltk.corpus import movie_reviews
	import random
	
	documents = [(list(movie_reviews.words(fileid)), category)
	              for category in movie_reviews.categories()
	              for fileid in movie_reviews.fileids(category)]
	random.shuffle(documents)

	# Define the feature extractor
	
	all_words = nltk.FreqDist(w.lower() for w in movie_reviews.words())
	word_features = list(all_words)[:2000]
	
	  
	def document_features(document):
	    document_words = set(document)
	    features = {}
	    for word in word_features:
	        features['contains({})'.format(word)] = (word in document_words)
	    return features
	
	  
	
	# Train Naive Bayes classifier
	featuresetsDocument = [(document_features(d), c, " ".join(d)) for (d,c) in documents]
	featuresets = [(d, c) for (d,c,r) in featuresetsDocument]
	train_set, test_set = featuresets[100:], featuresets[:100]
	classifier = nltk.NaiveBayesClassifier.train(train_set)