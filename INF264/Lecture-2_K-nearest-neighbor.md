
# Basic Concepts and k-Nearest Neighbors
[Complete guide to k-nearest-neighbor](https://kevinzakka.github.io/2016/07/13/k-nearest-neighbor/)

## Terminology

**Task**: Is what the end user actually wants to do

**Model**: Is a (hopefully good) solution to the task

**Model family**(or hypothesis space): is a set of models from
which the model is chosen

**Data**(or experience): Consists of oxjects in the domain the user 
is interested, with possibly some additional information

**Machine Learning Algorithm**: produces a model based on data

**Features**: are used to represent objects

## Supervised learning

- Task: predict labels of new, unseen objects
- Performance measure: (typically) prediction accuracy or error
- Experience: object-label pairs
- Classification: predict categorical labels
- Regression: predict real-valued labels

## Classification

- Different values of labels are typically calles **classes**
The model that predicts the label is called a **classifier**

--Insert flow chart from slides--

Training data -> Learning algorithm -> (New object->)Classifier -> Label

## Classification examples

- Given an image of a handwritten digit, classify it as one of the 10 digits (0-9)
- Given symptoms and test results of a patient, predict the most likely diagnosis
- Given an emails message, decide whether it is spam or not

## Regression

- Labels are continuous
- The model that predicts label is called a **regressor**
- Examples: 
    - Given historical data and economic indicators, predict the 
    stock price in the future
    - Given past buying behaviour, predict future sales of a product


## Exercise (Exam question H21)

Suppose you are a consultant who is hired to develop machine
learning -based solutions. Read the description given by your client
below. Identify a machine learning problem using **Mitchell’s
definition of well-defined machine learning problems.** In other
words, what are the task, experience and performance measure?

**Customer:** ”We think it is old-fashioned to require employees to
carry key cards. We want to replace locks that are opened with
cards with a ML-based system that uses cameras and opens doors
automatically when an authorized person arrives (and naturally
keeps the door locked if the person is not authorized to enter the
area).”


## The ultimate goal of machine learning 

### Generalization
Make predictions about examples that you have not seen

An engineer, a physicist, and a mathematician are on a
train in Scotland, and they see a black sheep. The engineer
says ”look: all sheep in Scotland are black.” The physicist
says ”no, some sheep in Scotland are black.” The mathematician is irritated with them and replies: ”you have it
all wrong: there is at least one sheep in Scotland, and it
is black on at least one side.”, a physicist, and a mathematician a"


- Which one is right?

## Exercise 

- There is an unknown function f(x)
- We have observed that f(1) = 2, f(2) = 4, f(4) = 8, and f(5) = 10
- Task: Figure out what f is

--Missing graph from slides--

- Using your estimate of f, what is your prediction for f(3)?

### One option

f(x) = 2x
--picture of graph--

### Another option

f (x) = −3.10187065 sin x − 3.17684994 cos x +2.03141401 sin 2x − 10.76407068 cos 2x
--picture of graph--

- Why did you choose the first option?

## Inductive bias

- **Induction**: from specific cases to general rules
- The inductive bias of a learning algorithm is the set of 
assumptions that the learner uses to predict outputs given inputs
that it has not encountered (Mithcell)
- A model without inductive bias can memorize training data 
but it cannot generalize
    - No basis for preffering one label over another on unseen data
- Note: your predictions depend crucially on your assumptions

### Examples of inductive bias

- y varies linearly in x
- Simple models are better than complex ones (Ockham's razor)
- Similar objects have similar labels
- ...


## Evaluating generalization

- If we have two models that predict correctly all the training
points then how can we figure out which one is better? 
- Solution: Use validation data to get an estimate for
performance on unseen data
    - Partition your data into two sets (training and validation sets)
    BEFORE you take a look on it
    - Use the training set to train your models
    - Use the trained models to make predictions about examples in the validation set
    - Compare predicted labels to true labels and compute your performance measure
    - Choose the model with better performance on the validation set
- If we want to get an unbiased estimate of the generalization
performance of the selected model then we have to partition the 
data into three parts: training, validation and test sets
    - And this has to happen BEFORE we take a look on it 
- Terminology
    - **Validation data**: Unseen data that is used to select a model
    - **Test data**: Unseen data that is used to evaluate performance of the selected model
- More about model selection and evaluation  on Lecture 6


## k-Nearest Neigh: basic idea

- **Inductive bias**: similar objects have similar labels
- Possibly the simplest possible classifier:
    - Find k points that are most similar to the test point
    - Let them vote for the class label
- k is a parameter chosen by the modeller

### Selecting k

- In the example above, different values of k lead to different predictions
- Large k reduces the effect of noise; small k increases flexibility
- For binary classification, an odd k avoids ties
- Too small k may lead to Overfitting
- Solution: Use validation data to select the best k


### Overfitting

- Definition: A model performs well on training dat but generalizes poorly
- Potential causes
    - Noise (irrelevant information or randomness in data)
    - Too flexible (complex) model
    - Too little data

### Distance measures

- We can use the k nearest neighbors if we can compute the 
similarity (or dissimilarity) between objects
- Often, objects are represented by vectors in some space and their 
dissimilarity is measured by their distance
- Common distance measures: 
    - Euclidian distance: d(x,z) = $\sqrt{\sum_i{(x_i - z_i)^2}}$
    - Manhattan distance: d(x,z) = $\sum_i|x_i - z_i|$
    - $L_p$ - norm: $||x - z||_p$ = $(\sum_i|x_i - z_i|^p)^\frac{1}{p}$
- Sometimes it is better to use domain-specific distance measures
- Note: choosing a different distance measure will affect the results

### Pros and cons

- Pros 
    - No assumptions about data
    - Simple
    - Often good accuracy
    - Versatile (can be used in both classification and regression)
    - With enough training points, can approximate any decision
    boundry (universal approximation theorem)

- Cons 
    - High memory requirement
    - Prediction stage can be slow
    - Sensitive to irrelevant features and the scale of the data
    - Curse of dimensionality (more later)
    
### Summary

- To be able to generalize, we need to add inductive bias
- k-nearest neighbors is a simple classifier in which the k most
similar object vote for the class label of a given object
- Despite of being simple, k-nearest neighbor algorithm can give good results

### Implementation details

- Scalability
    - Classifying a point can require computing n distances between 
    d-dimensional objects
    - Can be prohibiting for large n or d
    - Remedy: use specialized data structures to store data
        - For example, kd-tree

### Variants

- Majority vote
- Distance-weighted vote
    - Inverse of the distance
    - Inverse of the square of distance

### Nearest neighbor regression 

- Nearest neighbor method is easy to extend to regression problems
- Instead of voting for the class of the test point,
the continous predictions from the neightbors are combined
- Possible combination methods: 
    - Averaging
    - Local linear regression
