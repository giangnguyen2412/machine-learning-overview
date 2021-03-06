# machine-learning-overview
A bird view over Machine Learning

## Bayesian machine learning
Uncertainty comes from many sources (inherent uncertainty from future forecase, uncertainty from insufficient observation, or data ambiguity).
Conventional deep learning only seeks an optimal point of parameters while Bayesian machine learning assumes that the parameters follow some distributions (variance and mean model the uncertainty of the distribution), and is interested in finding the most likely distributions given the data. 

## Meta learning
Humans have a remarkable ability to generalize, even with single observation of a class. On the other hand, deep neural networks require large number of training instances to generalize well, and overfits with few training instances.

Meta-learning, also known as “learning to learn”, intends to design models that can learn new skills or adapt to new environments rapidly with a few training examples. There are three common approaches: 

1) learn an efficient distance metric (metric-based); 

2) use (recurrent) network with external or internal memory (model-based); 

3) optimize the model parameters explicitly for fast learning (optimization-based).

So the question is: **How can we then learn a model that generalize well even with few training instances?**

Humans generalize well because we never learn from scratch. In a broader sense, meta-learning can refer to the learning of meta-information (e.g. hyperparameters or network structures). Kids who have seen cats and birds only a few times can quickly tell them apart. People who know how to ride a bike are likely to discover the way to ride a motorcycle fast with little or even no demonstration. Is it possible to design a machine learning model with similar properties — learning new concepts and skills fast with a few training examples? That’s essentially what meta-learning aims to solve.

## Interpretable Machine Learning
Existing work on interpreting models approach the problem
from two directions.

The first line of work computes the
gradient of the output of the correct class with respect to the
input vector for the given model, and uses it as a saliency
map for masking the input.

Another line
of research approximates the model to be interpreted via
a locally additive model in order to explain the difference
between the model output and some “reference” output in
terms of the difference between the input and some “reference” input

## Continual learning
### Contemporary problems
In machine learning, one of the most basic paradigms is
to clearly distinguish between a training and testing phase.
Once a model is trained and validated, it switches to a test
mode: the model gets frozen and deployed for inference
on previously unseen data, without ever making changes to
the model parameters again. This setup assumes a static
world, with no distribution shifts over time. Further, it assumes a static task specification, so no new requirements in
terms of output (e.g. novel category labels) or new tasks
added over time. Such strong division between training and
testing makes it easier to develop novel machine learning
algorithms, yet is also very restrictive.

Inspired by biological systems, the field of incremental
learning, also referred to as continual learning or lifelong
learning, aims at breaking this strong barrier
between the training and testing phase. The goal is to develop algorithms that do not stop learning, but rather keep
updating the model parameters over time. This holds the
promise of a system that gradually accumulates knowledge,
reaching increasingly better accuracy and better coverage as
time passes. However, it is practically not possible to store
all previous data - be it due to storage constraints or for privacy reasons. Yet updating parameters based only on recent
data introduces a bias towards that data and a phenomenon
known as catastrophic interference, in other words degrading performance on older data.

To make progress in this direction, several works have
opted for a specific experimental setup, consisting of a sequence of distinct tasks, learned one after the other. Each
time, only the data for the ‘current’ task is available for
training. We refer to this as task-based sequential learning.
Training a shared model one task at a time has led to significant progress and new insights towards continual learning,
such as different strategies for preserving the knowledge of
previous tasks. However, the methods developed in this specific setup all too often depend on knowing the task boundaries. These boundaries indicate good
moments to consolidate knowledge, namely after learning a
task. Moreover, data can be shuffled within a task so as to
guarantee i.i.d. data. In an online setting, on the other hand,
data needs to be processed in a streaming fashion and data
distributions might change gradually.

## Generative Adversaral Networks - GAN
https://towardsdatascience.com/overview-of-gans-generative-adversarial-networks-part-i-ac78ec775e31
https://towardsdatascience.com/generative-adversarial-networks-part-ii-6212f7755c1f
In training a GAN, we expect the distribution captured by the generator will be the same with the distribution of the real data. When these two distributions are same, this means the generator has converged. To determine whether these two distributions are similar, we use KL divgence which measures how one probability distribution p diverges from another distribution q.
### DC GAN  (Deep Convolutional Generative Adversarial Networks)
Which is basically a all-convolutional network version of original GAN. DCGAN demonstrated that GANs can learn distributed representations that disentangle the concept of gender from concept of wearing glasses. 
(man with glasses) - (man without glasses) + (woman without classes) = woman with glasses

But how should we change the noise if we want to generate images of men with glasses?

GAN uses a simple factored continuous input noise vector z while imposing no restrictions on how the generator may use this noise.

### Info GAN
InfoGAN tackles the problem by proposing to decompose the input noise vector into two parts:

- z, which is treated as source of incompressible noise
- c, which is a latent code that targets the salient structured semantic features of
the data distribution.

### GAN vs VAE
One problem with VAE is that for having a good approximation of p(x) (where p(x) is the distribution of the images), you need to remember all details in the latent space z. And in the simple framework of the VAE, the approximation of the posterior pθ(z|x) is usually over simplified, because we can’t parametrize complex distribution (it is often a unimodal distribution like an isotropic gaussian).

## Paper review
### Knowledge Distillation
- <a name="todo"></a> Distilling the Knowledge in a Neural Network - Geoffrey Hinton & Oriol Vinyals (**2015**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/distillation.md) 
- <a name="todo"></a> Learning from a Teacher using Unlabeled Data - Gaurav Menghani & Sujith Ravi (**2019**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/distillation2.md) 
- <a name="todo"></a> Deep Mutual Learning - DML - Ying Zhange et al. (**2017**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/dml.md)
### Self-training
- <a name="todo"></a> Self-training with Noisy Student improves ImageNet classification - Quizhe Xie et al. (**2019**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/self_training.md) 
### Weakly-supervised Object Localization

- <a name="todo"></a> Perturbations on the Perceptual Ball - (**2019**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/perc_ball.md) 

- <a name="todo"></a> Learning Deep Features for Discriminative Localization - (**2016**) - [review ](https://github.com/luulinh90s/paper-review-continual-learning/blob/master/CAM.md) 

## Common knowledge
### Why Batch normalization works?
Assume we have a model y = Wx + b
When we want to upadte W, we need to use derivative dy = dW.x while x is out input

Apparently, x will affects the derivative value directly. So, If the values of X is not normalized, the gradient value could be fluctuated, thus exacerbating the optimization process.

### Difference betwwen bias and variance
Bias is the difference between the model's prediction and the grouth truth. The large bias meaning the model can not capture the distribution of data or underfitting.
Variance is the difference amongst model prediction itself. Usually, if we have large variance, meaning the model try to fit the data, or overfitting.
We expect our model to achieve low bias and low variance
### In classification task, is accuracy reliable?
If there is an imbalance in dataset, the accuracy score makes no sense in practice. For example, if we train a model of 9M images of cats and 1k images of dog. Apparently, the model will highly classify cats correctly with overall accuracy is about ~ 100%. But in practice, this model will surely fail.
To tackle this problem, using Confusion Matrix will help.
### How back-propagation works?
1. Forward propagation to have the loss (discrepancy of output and GT)
2. Compute derivative for each layer the a network then use optimizer to to perform gradient descent to update the weight.
3. Backprop uses chain rule to compute the gradient value from the deeeper layer to the shallower layer.
### Meaning of activation function
1. They determine when a neuron should be activated or deactivated
2. While tanh or sigmoid has saturation regions, RELU doesnt have. Saturation happens when we change the value of input but the output becomes saturated.
3. If saturation occurs, the gradient will be zero because the output is not changed, so the network can not learn.
### Hyper-parameters vs parameters
- Parameters are values of model generated from the training process to help model the distribution of data.
- Hyperparameters are the values that are frequently chosen by people such as learning rates, numbers of hidden layers, activation fuction, momentum v.v...
### When the input image size is doubled, how many times does the number of CNN parameters increase? Why?
No change, because the number of CNN params only depends on number and size of filters.
### Dealing with data imbalance?
1. Using proper evaluation metric such as Confusion matrix or ROC
2. Ensemble many models. Such as 1000 images of cat and 100 images of dog. We will train 10 models with 100 images of cat and 100 images of dog then ensemble these 10 models to get the only model.
3. PEnalize the richer classes by loss function.
### My memory blew up when I compute distance b/w two tensors!

- Symptom: I have 2 tensors with the size of 100352. When I call this function to compute the distance b/w them like this: `distance_dict[path] = torch.dist(embedding, feature_vector)` in a `for` loop, my CPU exploded. 

- Solution: You need to check if these two tensors are needing differentiation or not. If they do, the problem comes from the gradient of these tensors. You can use `distance_dict[path] = torch.dist(embedding.detach(), feature_vector.detach()` to get rid of this problem :)
