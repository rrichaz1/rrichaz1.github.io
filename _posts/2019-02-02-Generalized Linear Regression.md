The General Linear regression assumes that the residuals are normally distributed. This concept is a little hard to wrap around as we often think that the independent variables are assumed to be normally distributed. Although the error term and residual are often used synonymously, there is an important formal difference. An error term is generally unobservable and a residual is observable, making it much easier to quantify. 

When the residuals are not normally distributed, Generalized Linear models are used. The GLM generalizes linear regression by allowing the linear model to be related to the response variable via a link function. One of the link functions is a logistic function which is used to predict a categorical dependent variable. The most common usage of logistic regression is used to predict binary 0 or 1 outputs.

Logistic Regression is a great way to lead into classification realm of statistical learning. Like Linear regression, we optimize the classification algorithms by reducing the error. The error is reduced by simple classifier that assigns each observation to the most likely class,
given its predictor values. This is the Bayes classifier. 

In real world, we do not know the value of dependent variable given certain values of independent variables. To overcome this, classifiers try to estimate the conditional distribution of the data. One such classifier is the K-nearest neighbors (KNN). The KNN algorithm assumes that similar things exist in close proximity. The question how do we define proximity or distance.

In order to classify, we figure out the distance between two elements of a set. The next question is how do we calculate the distance using the features of an element and what features to use.
 If we use all the features then the algorithm will be slow. We use expert or apriori knowledge to select the features. Now to calculate the distance:
1.	For quantitative data we use distance functions like Euclidean, Maximum, Manhattan etc.
2.	For qualitative data, we use the Jaccard index, also known as Intersection Over Union. 

An example of Jaccard Similarity Coefficient from Wikipedia:

Given two objects, A and B, each with n binary attributes, the Jaccard coefficient is a useful measure of the overlap that A and B share with their attributes. Each attribute of A and B can either be 0 or 1. The total number of each combination of attributes for both A and B are specified as follows:
M11: represents the total number of attributes where A and B both have a value of 1.
M01: represents the total number of attributes where the attribute of A is 0 and the attribute of B is 1.
M10: represents the total number of attributes where the attribute of A is 1 and the attribute of B is 0.
M00: represents the total number of attributes where A and B both have a value of 0.

The Jaccard similarity coefficient, J, is given as  M11/(M01+M10+M11)

Once we figure out the distance function, we select a value of k i.e the number of nearest neighbors we will look for. The algorithm will do the following, for each data point:
1.	Based on the distance, figure out the k nearest neighbors.
2.	Predict the class of the data point by using a voting mechanism.
A drawback of KNN is that it will consider the point as a neighbor even if it is too far. To overcome this, we consider the density of points in an area. The density-based classification also performs better for large data sets.
The tree based algorithms remove the requirement for a distance function. We partition the data set into partitions based on mean for regression and votes for classification. The tree based classification can cause overfitting. To overcome overfitting we use bootstrapping.

References:
[https://www.statisticshowto.datasciencecentral.com/jaccard-index/](https://www.statisticshowto.datasciencecentral.com/jaccard-index/)
[https://en.wikipedia.org/wiki/Jaccard_index](https://en.wikipedia.org/wiki/Jaccard_index)
[https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4978658/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4978658/)
[https://machinelearningmastery.com/a-gentle-introduction-to-the-bootstrap-method/](https://machinelearningmastery.com/a-gentle-introduction-to-the-bootstrap-method/)

Book: An Introduction to Statistical Learning with R
