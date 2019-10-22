# machine-learning-overview
A bird view over Machine Learning

## Meta learning
Humans have a remarkable ability to generalize, even with single observation of a class. On the other hand, deep neural networks require large number of training instances to generalize well, and overfits with few training instances.

Meta-learning, also known as “learning to learn”, intends to design models that can learn new skills or adapt to new environments rapidly with a few training examples. There are three common approaches: 

1) learn an efficient distance metric (metric-based); 

2) use (recurrent) network with external or internal memory (model-based); 

3) optimize the model parameters explicitly for fast learning (optimization-based).

So the question is: **How can we then learn a model that generalize well even with few training instances?**

Humans generalize well because we never learn from scratch. In a broader sense, meta-learning can refer to the learning of meta-information (e.g. hyperparameters or network structures). Kids who have seen cats and birds only a few times can quickly tell them apart. People who know how to ride a bike are likely to discover the way to ride a motorcycle fast with little or even no demonstration. Is it possible to design a machine learning model with similar properties — learning new concepts and skills fast with a few training examples? That’s essentially what meta-learning aims to solve.
