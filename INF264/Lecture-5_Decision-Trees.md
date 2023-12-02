# Decision Trees

## Learning goals

- After finishing this module, a student can 
    - explain basic principles and properties of decision trees 
    - simulate learning and pruning algorithms for decision trees 
    - apply decision tree algorithmns in practice 


## Agenda 

- Prediction using decision trees 
- Learning decision trees using ID3 algorithm 
- Pruning decsion trees to avoid overfitting 

## Decsion tree 

-- Insert image from slide --

### Structure 

- Inner nodes are associated with a test 
    - Usually, the test involves only one feature 
    - Outgoing edges correspond to possible test results 
- A child is selected based on the test result 
- Leaf nodes make a prediction 
    - Classification: assign a class label to an object 
    - Regression: assign a numerical value 
    - Predictions can be also probabalistic


### Example 

-- Insert image from slide --


## Expressiveness 

- Decision trees can approximate any function of the input features with arbitrary precision 
- If there are no duplicates with different class labels, there is a consistent decision tree for every training set with one path to a leaf for each data point
    - Can be large 
    - Probably does not generalize well
- Prefer more compact decision trees (Ockham's razor)
- Finding an optimal decision tree (the one that minimizes the expected number of tests) is NP-hard


## Learning 

- Trees are typically learned using greedy heuristics 
    - Start with an empty tree 
    - Greedily, select a feature to split 
    - Recurse 
- Note: Let us have a data set *D*. If we split a feature $x_i \in \{0,1\}$ 
    then we will have two data sets $D_0$ and $D_1$ where all data points in $D_0$ have $x_i = 0$ and all data points in $D_1$ have $x_i = 1$

## Which feature to split?

- Typically, one wants to divide the space into "pure" parts
- In other words, one wants to reduce uncertainty 
- That is, choose the feature which gives highest information gain

-- Insert image from slide --

## Entropy

- Entropy measures average information content that is obtained from a stochastic information source
- More uncertainty -> more information content 
- Entropy of a random variable X is 
$$ H(x) = - \sum_i{P(x=x_i)\log_2{(P(x=x_i))}}$$


-- Insert image from slide --


- High entropy 
    - Lots of uncertainty
    - Nearly uniform distribution
- Low entropy
    - Less uncertainty
    - Outcomes have probabilities near 0 or 1

-- Insert image from slide --


## Other impurity measures 

- Gini index: $G(x) = \sum_i{P(x=x_i)(1-P(x=x_i))}$
- Misclassification rate: $E=1- \max_i{P(x=x_i)}$


-- Insert image from slide -- 


## Conditional entropy

- Amount of information needed to describe the outcome of a random variable *y* when the value of a random variable *x* is known
- Or amount of uncertainty of *y* when the value of *x* is known

$H(y|x) = \sum_i{Px=x_i)H(y|x=x_i)}$
$=-\sum_i{P(x=x_i)} \dot$

-- Finish later --


## Information gain 

- What happens if we split the data set based on the value of *x*?
- Information gain is increase in information after splitting
    - Equivalently, decrease in entropy (uncertainty) after splitting 
- $IG(x) = H(y) - H(y|x)$
    - Uncertainty before split - uncertainty after split 
- We prefer splitting variables with high information gain


## ID3 algorithm

Iterative Dichotomizer 3
- If all data points have the same label 
    - return a leaf with that label
- Else if all data points have identical feature values
    - return a leaf with the most common label
- Else
    - choose a feature that maximizes the information gain 
    - add a branch for each value of the feature 
    - for each branch 
        - call the algorithm recursively for the data points with the particular feature value

### Notes 

- If a feature has more than 2 values, it is still common to split only two branches
    - Splits to several branches can be achieved by a sequence of two-way splits 
- Typically, overfits to the traning data


## Continous variables 

- In principle, there are infinite number of possible split points 
- In practice, one can get good results by considering only one split point 
    - For example, mean or median of the variable

## How to avoid overfitting? 

- If there are no training points with identical feature values, ID3 will result in 100% traning accuracy
- Inductive bias: prefer smaller trees 
- Set a minimum size for a leaf or maximum depth for the tree 
    - Usually not enough
- Early stopping (pre-pruning)
    - Stop recursion once information gain is non-positive
    - Problematic, cannot handle, e.g., XOR
- Pruning (post-pruning)
    - Build a full tree, remove parts of it later


## Reduced-Error Pruning 

- Divide data to training and pruning (validation) data

1. Use the training data to build a full decision tree 
2. For each subtree *T*
    - If replacing the subtree with the majority label in *T* does not decrease accuracy on the pruning data 
        - Replace *T* with a leaf node that predicts the majority class


## Regression trees

- Prediction values *y* using the points associated with the leave
    - Typically, by averaging
- Learning 
    - Small modifications to the algorithm:
    - Instead of the impurity measures above, use squared error 
    - Predict with mean value for the data subset
    - Information gain from a split is the squared error before the split - squared error after the split


## Properties of decision trees

- Pros 
    - Fast (both to learn and predict)
    - Easy to interpret
    - Invariant to scaling 
    - Can handle both categorical and continuous data 
    - Implicit feature selection 
- Cons 
    - Unstable
        - Due to greedy learning, small differences in training data can result in totally different trees
    - Usually competive accuracy only in an ensemble (More on this in Lecture 10)

## Summary

- Decision tree models are simple and easy to interpret 
- Usually learned with greedy algorithms 
- Splits are chosen based on information gain 
- Without pruning they are prone to overfit


