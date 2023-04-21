Hyperplane based classification, Bayesian classification and Artificial Neural Networks. IN this blog I decided to delve deeper into the Bayesian classifier.

Bayesian classification or Naïve Bayes classifier has been in use since the 1950s. It primarily was used to classify documents into various categories:
•	Spam or not spam
•	Politics, Sports or Others
It is simple, fast and with appropriate pre-processing as competitive as support vector machines and other complex algorithms. The classifier follows the principle of Bayes theorem. Naive Bayes is a simple technique for constructing classifiers: models that assign class labels to problem instances, represented as vectors of feature values. Here the features are considered to be independent of one another and have no correlation with one another. Hence the name “Naïve”. 

As per the Wikipedia article, in real world the Bayesian classifier uses the Maximum Likelihood to estimate the parameters.  The concept of Maximum likelihood gets a little confusing especially as sometimes it is used in place of probability. To clear the confusion on Maximum Likelihood, I again went to Wikipedia where I got the difference as 
“Probability in this context describes the plausibility of (random) observed data assumed to be described by a statistical model a parameter value of which is given, without reference to any observed data; whereas likelihood in this context describes the plausibility of a parameter value of the statistical model assumed to describe the observed data, given specific observed data. “

In short, the maximum likelihood is the method to get the best estimates of the model. The MLE considers the observed data whereas probability is more theoretical and does not consider observed data.

How do MLE and Bayesian play together. An example in Quora using coins got the concept cleared a bit.  
Say in a coin toss we get three heads in three flips. With pure MLE we may be prone to believe that the coin is a unfair or even two sided coin. 
With Bayesian reasoning, we take into account the fact that we actually know more than just that we got three heads in three flips. We also know that most coins are close to fair. To use Bayesian terminology, we have an idea of a prior probability distribution for the value of H. It is H = 0.5:  the typical coin is fair or close to it. That’s our starting point. Then when we get three heads in a row, we’re led to believe that the coin may be biased a bit towards heads (i.e., H is a bit greater than 0.5). The observed data shifts our prior idea a bit giving us a new distribution of estimates (a posterior probability distribution), but we don’t throw away our prior knowledge and go all the way to the MLE and conclude we’re dealing with a two-headed coin.

The mathematical representation of the formula is 
p(Ck|x) = p(x|Ck)*p(Ck)/p(x)  , Here Ck are 1….k classes from the dependent data x 
In simpler English

Posterior = prior * likelihood / evidence
Since the evidence is the same for all classes, we only use the numerator. We then use the chain and apply a function like Gaussian (if the data is continuous).
We then calculate the maximum probability for each of the classes and pick the one that has the maximum value.

The week’s highlight was the lecture on Artificial Neural Networks. It came as a surprise that the concept was introduced in the 1950’s. It is amazing how the artificial neural network is modeled after the human brain. Looking forward to learning more about them in the Artificial Intelligence Learning path. 

Some references: 
[https://machinelearningmastery.com/naive-bayes-for-machine-learning/](https://machinelearningmastery.com/naive-bayes-for-machine-learning/)
[https://en.wikipedia.org/wiki/Naive_Bayes_classifier](https://en.wikipedia.org/wiki/Naive_Bayes_classifier)
[https://www.quora.com/How-do-you-explain-maximum-likelihood-estimation-intuitively](https://www.quora.com/How-do-you-explain-maximum-likelihood-estimation-intuitively)
