
Pedro Domingos's The Master Algorithm: How the Quest for the Ultimate Learning Machine Will Remake Our World


Algorithms use the trails of data we leave and run almost all facets of our lives. They find movies, jobs and dates, manage our investments and discover new drugs. Traditionally humans had to write step by step algorithms for computers to accomplish anything. But machine learning algorithms, also known as learners, figure out the algorithms on their own by making inferences from data. Pedro Domingo describes it as humans do not program computers, they program themselves. No one teaches the self driving car to drive, the car is equipped with a algorithm that learns based on the data it collects and observing what the driver does. The human beings are not completely out of the picture as they still have to guide which algorithm and what data to use.
Paradoxically as the algorithms provide new insights into human behavior, they themselves remain shrouded in mystery. Also, the algorithms are specialists rather than generalists. In other words, an algorithm that recommends what movies to watch will not learn how to drive a car. In this book, Pedro Domingo takes the reader on a journey to find the universal learner, a unified theory that makes sense of everything we know to date. The master algorithm is a learning algorithm that can derive all knowledge from the world from data and can be used across all domains. 
The book appeals to readers who do not have a background in big data and machine learning by giving a lay of the land without going into the intricacies. For the machine-learning expert, it challenges them to solve problems in new ways and stride towards finding the one general learning master algorithm.  Domingos suggests that we do not have to learn the master algorithm from scratch, instead we can learn from the five tribes of algorithms, and combine them into a general-purpose learning machine.

1.	Symbolists or Empiricists:
The first tribe, the symbolists or empiricists, believe that all problems can be solved as a system of equations. Their algorithms build sets of rules based on the data available. The challenge remains twofold, how do we guard against the combinatorial explosion of rules and secondly, how do we generalize the solution to answer questions regarding unseen data. Domingos notes, that unlike deduction which starts with a premise and looks for conclusions is not enough to find the missing rules.  He recommends using inverse deduction or induction, which looks at both premises and conclusions and works backwards, to fill in the missing rules.
For instance, to figure out the rules for how genes express themselves, we run a set of experiments and the results say: 
If the temperature is high, gene A is expressed.
If the temperature is high, genes B and D are not expressed.
If gene C is expressed, gene D is not.
We can use inverse deduction to fill the gap “If gene A is expressed and gene B is not, gene C is expressed”. We can create new experiments to test out the new rule and possibly use it for further inductive inferences. We can also apply these rules to new examples to predict whether the gene will be expressed or not.
The most popular algorithm among symbolists is the decision tree. Decision tree is a graph consisting of nodes and branches. At each node we split the data based on an attribute and follow the branch until all data at a node belongs to a class. The beauty of decision tree is its interpretability. Despite the popularity of Decision Trees, Domingos prefers using Inverse deduction as it is more conducive to incorporating knowledge without growing exponentially.

2.	Connectionists:
The second tribe are the Connectionists who prefer to simulate the brain with a computer. Jeff Hawkins in the 2004 book On Intelligence puts it as “ the brain is a feed forward hierarchical state machine with special properties that enables it to learn.
The perceptron of neural networks was modeled after a neuron.  An actual neuron fires an output signal only when the total strength of the input signals exceeds a certain threshold. We model this phenomenon in a perceptron by calculating the weighted sum of the inputs to represent the total strength of the input signals and applying a step function on the sum to determine its output. 
The connectionists master algorithm is back propagation that compares the system output with the desired output and uses that to learn the weights of the connections layer by layer. Its popularity has grown by leaps and bounds in recent years with the availability of data and compute capacity. The main argument against the neural networks is that it is  a black box and lacks the efficiency and generalizability of the human brain. 

3.	Evolutionaries:
The third tribe or Evolutionaries, believe that the mother of all learning is natural selection. In the 1970’s, Jon Holland introduced genetic algorithm by mimicking the evolution process “survival of the fittest”. The genetic algorithm starts with a random population and fitness function. In each iteration or generation, we mutate and cross over set of rules and then test them using the fitness function. With each generation the rules become fitter and stronger.    
For instance to develop a spam filter, we start with a set of words that can potentially identify spam. The fitness function is the percentage of emails classified correctly as spam. We start with simple rules, compare the results against the fitness function and improve the rules in each generation.

|Iteration	|Word	|Rule 1	|Rule 2	|Fitness function check |
| ----------- | ----------- |----------- | ----------- |----------- | 
|1	|Free	|If email contains free it is spam	|If email contains free it is not spam 	|Rule 1 selected |
|1	|Easy	|If email contains easy it is spam	|If email contains easy it is spam	|Rule 2 selected |
|2	|Free and Easy	|If email contains free and easy it is spam	|If email contains free and not easy it is spam	|Rule 1 selected |

Genetic algorithms consider an entire set of hypotheses at each step and makes big jumps from one generation to another. This is in contrast with back propagation which starts with a single hypothesis and takes small deterministic steps until it reaches solution.
4.	 Baynesians:
 The fourth tribe or Bayesians start with a hypothesis and employ probabilistic inference algorithms on new evidence to update the hypothesis.  The master probabilistic inference algorithm used is the Bayes theorem. 
Bayes theorem states that 
P (T and D) = P(D|T)P(T) where P(D|T) signifies the probability of D given T. 
Suppose you take a mammogram to test for breast cancer and it comes back positive. We want to know what is the probability of having cancer given the test came back positive, i.e. P(disease|test). We know the sensitivity of the test i.e. P(test = 1|disease)
P(D|T)updated = (likelihood ratio) * Prior probability of P(D|T)
Likelihood ratio = P(T|D)/P(T)
P(T) is trickier. A positive test cane be both from patients that test positive and have the disease and patients that test positive but do not have the disease i.e. false positives.  So we take a weighted average of P(T|D) and P(T|~D). We take a weighted average as more people do not have disease P(~D) than those who have the disease P(D)
P(TD) = 73%, P/9T|~D) = 12%
P(D) = 1%
P(T) = 1/600* (0.73) + 699/700 *0.12 = 12.1 % approx.

Likelihood ratio = 73 percent/12.1 percent  = 6
Since the prior probability is 1/700, the updated probability = 6*1/700 = 1/116
Signifies that positive test at young age is most likely to be a false alarm.
Bayes inverse probability represents the simplest Bayesian network. 
Disease ->Test 
-	A -> B -> C,  B is the mediator
-	A <-B ->C, This is  fork where B is the confounder
-	A -> B <- C , is a collider
In Bayesian network we have to give the conditional probability of each node given its parents.
State of the art tool, Bonaparte was used to identify victims of the Malayasian jetliner crash The DNA of the victims could not be matched against a central database. Next best option is to match it against the dna of the relatives. The problem is harder as we have not have direct relatives like parent or siblings. To use indirect relations.
The contributions from the parents (allelles) have to be treated as hidden, unmeasurable variables. Part of Bonaparte’s job is to infer the probability of the cause. (victim’s gene of blue eyes comes from father, victim has genes for blue and black eyes, cousins on father’s side has blue eye genes, while cousins on mothers side has black eye genes). This is an inverse probability problem.
 

The challenge is how to handle the probabilities when the features are dependent on each other. To overcome this, the features are assumed to be independent and these models are called naïve Bayes models.
Naïve Bayes classifiers are used widely to classify spam. For instance, the word free and Viagara occur more often in spam emails and less often in legitimate emails. The algorithm assigns higher probability to these words and marks the emails containing them as spam.    
Bayes’ theorem incorporates multiple different variables into the development of a hypothesis and can be represented in the probabilistic graphical model called the Bayesian Networks. A Bayesian network works backwards, by looking at an event and suggesting possible reasons that led to it. For example, it can help determine whether diet or exercise help more with weight loss. The Bayesian networks are used for a wide range of tasks including prediction, anomaly detection, diagnostics, automated insight, reasoning, time series prediction and decision making under uncertainty.

5.	Analogizers:
The fifth tribe or Analogizers look for similarities between situations and infer other similarities. If two patients have same symptoms perhaps they have the same disease.
The two dominant approaches in this tribe are nearest neighbour and support vector machines. Domingos describes nearest neighbour as the simplest and fastest learning algorithm and there is no pre work to be done. The work starst when a new test example arrives. The aalgorithm compares it across all existing examples for similarity and the new example is classified into the same class as that of nearest neighbor. This algorithm is used extensively in recommender systems used by companies such as Netflix, Amazon etc. The nearest neighbor algorithm is especially prone to the curse of dimensionality especially as the number of features increases.  
Support vector machines classify examples by developing boundaries between the positive and negative examples, with a specified “margin” of safety between the examples. They do this by mapping the points into a hyper-dimensional space and developing boundaries that are straight lines. The examples along the margin are the “support vectors”. The SVMs got great success in handwritten digit recognition and text classification.
All these five tribes belong to the class of supervised learners. The unsupervised tribe of learners are the PCA, K Means clustering and Reinforcement learning. Reinforcement learning gained a lot of prominence when Deepmind’s computer program AlphaGo defeated a professional Go player by learning to play itself. Reinforcement learning is used in multiple fields to park car backwards, manage automated telephone dialogue, space shuttle cargo leading and much more.

Even though the learners in the book are quite disparate, some based on brain, some on evolution, some on abstract mathematical pronciples, they in fac have much in common. The challenge is to find the i=unfier like the Intenet unified the networks, the Graphical User Interface lets us edit documents, excel sheets using common language of menus, mouse clicks. Electricity is a great unifier.
Simple metalearning is bagging and boosting. These are not efficient ways to unif algorithms.
Mrkov logic networks as the represetation, posterior

Alchemy - Open Source AI (washington.edu)

> We did not learn how to fly by looking at words and flapping our wings

|Tribes	|Symbolists	|Connectionists	|Evolutionaries	|Bayesians	|Analogizers |
| ----------- | ----------- |----------- | ----------- |----------- | ----------- | 
|Learning	|Sequential steps	|Single hypothesis |	Multiple hypotheses	| |	
|Master Algorithm	|Inverse Deduction	|Back Propagation	|Genetic algorithm	|Bayes theorem and Bayesian networks	|Support Vector Machines|
|Inspiration	|Statistical	|Nature	Nature	|Statistical	|
					


References:

1.	[Master Algorithm](https://lamp.cse.fau.edu/~lkoester2015/Master-Algorithm/index.html) 
2.	[Pedro Domingos on Machine Learning and the Master Algorithm - Econlib](https://www.econtalk.org/pedro-domingos-on-machine-learning-and-the-master-algorithm/)
3.	[Neural Networks - Neuron](https://cs.stanford.edu/people/eroberts/courses/soco/projects/neural-networks/Neuron/index.html#:~:text=The%20perceptron%20is%20a%20mathematical%20model%20of%20a,axons%2C%20electrical%20signals%20are%20modulated%20in%20various%20amounts.)
4.	[Genetic Algorithm and its usage in neural network](https://theailearner.com/2018/11/08/genetic-algorithm-and-its-usage-in-neural-network/)
5.	[Bayesian Network - The Decision Lab](https://thedecisionlab.com/reference-guide/statistics/bayesian-network/#:~:text=Bayes%E2%80%99%20theorem%20incorporates%20multiple%20different%20variables%20into%20the,is%20that%20they%20must%20satisfy%20the%20Markov%20condition.)
6.	[Alchemy - Open Source AI](http://alchemy.cs.washington.edu/)
7. [What is Curse of Dimensionality? A Complete Guide | Built In](https://builtin.com/data-science/curse-dimensionality)
8.	[AlphaGo | DeepMind](https://deepmind.com/research/case-studies/alphago-the-story-so-far)
9.	[The Book of Why: The New Science of Cause and Effect: Pearl, Judea](https://www.amazon.com/Book-Why-Science-Cause-Effect/dp/046509760X)


