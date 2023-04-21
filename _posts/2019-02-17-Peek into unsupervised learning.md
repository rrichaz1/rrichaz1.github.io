In supervised learning the algorithms learn from data that has labels. The algorithm learns to derive the relationship between the independent and dependent variables and then can use the learning to predict the outcomes from unseen data. 
In unsupervised learning there are no labels to learn from. There is only data. The machine learning algorithms look for patterns in data and try to come up conclusion. This in many ways to how humans process information. The human brain has an immense capacity to conjure patterns for instance animals in the cloud, old woman in the moon. Sometimes these patterns make sense and sometimes they don’t.  This was part of the OSDS visualization lecture. This lecture covered the Gestalt Principles that describe how humans perceive group. These are:
1.	Proximity
2.	Similarity
3.	Common fate
4.	Continuity
5.	Closure
The classification algorithms conceptually follow the same principle. Elements having n features can be grouped into k features. That is why they are sometimes used during data processing stage to reduce the dimensionality of data. The lower dimension data is then fed to other machine learning algorithms.

The various clustering methods are:
1.	Top down or bottom up
a.	Top down – start with all the data in 1 cluster and then keep splitting until you reach k clusters
b.	Bottom Up – Each data point is its own cluster and we combine the points to form clusters until we reach k clusters
2.	Hierarchical vs Partitioning
3.	Graph vs Distance
4.	Model Based


Supervised learning is easier in the sense that we have a known result. If our computed result matches the actual result, the better the algorithm. In case of unsupervised learning, how do we measure whether the algorithm is good or not. For clustering, we measure:
1.	Compactness or Intra cluster distance
2.	Separateness or Inter cluster distance
Just like bias-variance tradeoff in supervised learning, there is compactness-separateness trade off in clustering. 

K Means algorithm is one of the most popular algorithms and relatively easy to comprehend:
1.	Determine the k, i.e. the number of clusters
2.	Initialize the center of the clusters
3.	Attribute the closest cluster to each data point
4.	Set the position of each cluster to the mean of all data points belonging to that cluster
5.	Repeat steps 3-4 until convergence
The algorithm stops when the assignments do not change from one iteration to the next. 
With K Means clustering, we have to select the value of k beforehand. This limitation is not there for Hierarchical clustering. We define a measure of dissimilarity usually a Euclidean distance. The bottom up approach takes each element as a cluster and then tries to group the nearest clusters together. It goes on iteratively until all the elements are clustered. 
The concept of height of the dendrogram was a little difficult to apprehend. I found some examples using mtcars dataset. I took a subset of the data only brands starting with letter M and only used one independent variable, mpg. Used the dist function in R to get a row by column representation of the distances. Then I compared it to dendrogram created by plotting the output of hclust function. Looking at the distribution data side by side with the plot was a great help in understanding the dendrogram.


Some references:
[http://www.onmyphd.com/?p=k-means.clustering](http://www.onmyphd.com/?p=k-means.clustering)
[https://rpubs.com/gaston/dendrograms](https://rpubs.com/gaston/dendrograms)
Book: An Introduction To Statistical Learning with Applications in R

