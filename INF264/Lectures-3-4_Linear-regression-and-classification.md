# Linear Regression and Classification

## Learning goals

- After completing this module, a student can 
    - apply linear models to regression and classification tasks
    - apply linear models to non-linear data using basis functions
    - explain bias-variance tradeoff and its realtion to overfitting 
    - minimize objective functions using gradient descent


## Agenda

- Linear regression 
- Non-linear regression with basis functions 
- Bias-variance tradeoff 
- Logistic regression for classification

**Warning**: Linear algebra and calculus ahead


## Linear regression

- Simple and widely studied models 
- Often computationally convenient

-- Insert image --


### Univarate regression 

- Univariate means that the object has only one feature 
- Let x be the feature and y the label
- In regression, we predict response values using a function $f$: 
    $y = f(x) + \epsilon,$

where $\epsilon$ is the error (or residual) for the observation


### Univariate linear regression

- In univariate linear case, we can write

$y = w * x + b + e$

-- Insert image --

- How to choose $w$ and $b$?
    - Empirical risk minimization (ERM): minimize loss on training data
- What is a loss function? 
    - Loss function $L(y, f(x))$ measures "cost" of predicting $f(x)$ when the true label is $y$
    - For example, squared loss $L(y, f(x)) = (y - f(x))^2$
        - $L(y,f(x)) = 0$ only if $y = f(x)$
        - The loss increases when $y$ and $f(x)$ are far apart
    
- Minimize the sum of squared error on the traning set 

$$ E(w,b) = \sum_{i=1}^n\epsilon_i^2 = \sum_{i=1}^n(y_i - (wx_i + x))^2 $$

where the sum is over $n$ data points in the training data

- Estimates for the parameters can be found by solving

$$ (\hat w,\hat b) = arg min_{w,b} E(w,b)$$

- or, equivalently, minimize the mean squared error (MSE)
$$ \frac 1n \sum_{i=1}^n (y_i - (wx_i + b))^2$$


- Goal: minimize $E(w,b)$ by choosing values for parameters
- Solution: compute partial derivatives (gradient) and set them zeroes.
- Partial derivative w.r.t. b:
$$
\frac{\delta E(w,b)}{\delta b} = -2 \sum{i=1}^n (y_i - wx_i - b)
$$

- Set to zero and solve. We get 
$$
\hat b = \bar y - w\bar x,
$$

where $\bar y = (1/n)\sum_i y_i and \bar x = (1/n)\sum_i x_i$

--finish rest of univariate slides later--


### Multivariate linear regression

-- Insert image --

- Learn a linear function $f : \Bbb{R}^d -> \Bbb{R}$
- Instead of a line, we have a hyperplane
- Data matrix $\mathbf X \in \Bbb R^{n\times d}$ has $n$ instances $x_i^{\pmb T}$
 as it rows and $y \in \Bbb R^n$ has the corresponding labels $y_i$
- $\mathbf X$ is often called the design matrix 
- Weights are stored in $\mathbf w \in \Bbb R_{\pmb d}$
- Useful trick: $\mathbf x$ can automatically include a constant term, 
$\mathbf x = (1,x^{(1)},x^{(2)},\dots,x^{(d)})^{\pmb T}$, such that the intercept is automatically included:
$$ 
\mathbf w^{\pmb T}\mathbf x = w^{(0)} + w^{(1)}x^{(2)} + \dots + w^{(d)}x^{(d)}
$$

Note that $x^{(j)}$ denotes the *j*th feature

--finish slides later--


## Loss functions 

- So far we have used squared loss 
    - Computationally convenient -> widely used 
    - Sensitive to outliers

- Other common option is absolute loss: $|y-\hat f(x)|$
    - Less sensitive to outliers 
    - Computations become more complex

-- Insert image --


## Non-linearities

- Linear models are computationally convenient but as simple 
    models they are unable to capture complex non-linear relations
- Apply a non-linear transformation to data and perform linear 
    regression an transformed data

-- Insert image --

--finish rest later--


## Basis functions 

- Examples:
    - Polynomials of degree $k: \phi (x) = (1,x,x^2, \dots ,x^k)$
    - Interactions between two features: 
        $\phi ((x^{(1)},x^{(2)})) = (1,x^{(1)},x^{(2)},x^{(1)}x^{(2)})$
    - Radial basis functions, e.g., Gaussion: $\phi(\mathbf x) = e^{-(\epsilon ||\mathbf x - \mathbf c ||)^2}$, where $\mathbf c$ is called a center point

- Pros 
    - Adds flexibility 
- Cons 
    - If dimensionality grows, then also computational requirements grow
    - How to choose appropriate basis functions? 

-- Insert image --

## Feature engineering 

- Use domain knowledge to construct transformations of the original features
- Can be achieved by basis functions
- Often critical to the performance of machine learning algorithms

*Coming up with features is difficult, time-consuming, requires expert
knowledge. "Applied machine learning" is basically feature engineering. Andew Ng*


## Bias-variance tradeoff

- How to evaluate how good a models is?
- What if we consider only the error on training data?
    - A simple model will not be able to fit perfectly to the training data
    - A complex model typically fits better 
    - For example, in polynomial regression increasing the degree of 
        the polynomial never decreases the fit 
    - A polynomial with degree *n - 1* will fit perfectly to *n* data points
- The model that fit best on training data is not necessarily the one that generalises best


## Overfitting 

- Our goal is to find a model that predicts well unseen data (generalization)
- Overfitting: "the production of an analysis that correpsonds too closely
    or exactly to a particular set of data, and may therefore fail to fit 
    additional data or predict future observations reliably"
- How do we know that a model is overfitting?


## Bias-variance tradeoff 

- **Bias**: Error due to medoling assumptions
- **Variance**: Error due to variations in the training set
- Simple models tend to have high bias and low variance
- Complex models tend to have low bias and high variance
- Goal: low bias and low Variance

-- Insert image --


### Bias-variance tradeoff of squared error

- Consider a training set *D* containing *n* points, each coming from a distribution $P(\mathbf x, y)
- Assume the data are generated as $y_i = f(\mathbf x_i) + \epsilon_i$, for some function $f$ and $\epsilon_i \sim N(0, \sigma^2)$
- Let $\hat f_D : \mathcal X \to \Bbb R$ be the model that our algorithm produces from training data *D*
- Consider squared errors. Now, the exception of error over all possible training sets is 
$$
E_D[(y - \hat f_D(\mathbf x))^2]
$$



-- finish slides later --

## Bias-variance tradeoff 

- Exact bias-variance docomposition not possible in practice because the true function is not known
- Diagnosis using training and test errors 
    - High training error, high test error -> underfitting 
    - Low training error, high test error -> overfitting 

-- Insert image --

## Simple vs. complex models 

- Simple models cannot predict complex phenomena accurately
- Complex models can predict complex phenomena but they require lots of training data 
- The more training data you have, the more complex models can you learn 

## Regularization 

- To reduce overfitting, one may want to penalize complexity
- Basically, regularization is any modification in the objective function 
(or more generally learning algorithm) that intends to reduce generalization 
error but not training error 
- For example, the objective function for linear regression with L2-regulazer can be written as 
$$ ||(\mathbf y - \mathbf w^T \mathbf X^T)||_2^2 + \lambda ||\mathbf w||_2^2$$
where hyperparameter $\lambda \geq 0$ specifies the strength of regularization 
    - Regression with L2-regularizer is called *ridge regression*
- How to choose $\lambda$?
    - For example, use cross-validation (more next week)

### Regularized linear regression 

- With L2-regularizer we get objective 
$$ ||(\mathbf y - \mathbf w^T \mathbf X^T)||_2^2 + \lambda ||\mathbf w||_2^2$$
- Note that the more data points you have, the smaller is the effect of regularization
- Setting gradient to zero and solving the equations we get
$$\hat {\mathbf w} = (\mathbf X^T\mathbf X + \lambda \mathbf I)^{-1} \mathbf X^T \mathbf y $$

## Linear models for classification 

- Using standard linear regression is problematic in predicting categorical responses 
- We can use a variant called logistic regression Instead

-- Insert image --

## Logistic regression

- Consider binary classification problem 
    - $y_i \in \{0,1\}$
- Let *p* denote our prediction of the probability that $P(y = 1|\mathbf x)$
- Logistic linear regression 
$$ log \frac{p}{1-p} = \mathbf w^T \mathbf x),$$
where $\sigma (\cdot)$ is the so-called logistic sigmoid
$$ \sigma (z) = \frac{e^z}{1+e^z} = \frac{1}{1+e^{-z}}$$

-- Insert image of sigmoid function --

## Logistic regression for classification 

- When used in classification, the decision boundary is defined by 
$P(y = 1|\mathbf x) = P(y = 0|\mathbf x) = 0.5$. This corresponds to a hyperplane
$$\mathbf w^T \mathbf x = 0$$

- Classification rule:
$$\mathbf w^T \mathbf x > 0 \to y=1$$
$$\mathbf w^T \mathbf x < 0 \to y=0$$


## Learning parameters 

- Intuition: Try to maximize the probability of the true class label

-- Finish slides later --

## Gradient descent 

- An approximate method for finding a local minimum of a multivariate function 
    - A maximim can be found using an analogous gradient ascent technique
- Let $f(x)$ be a differentiable function. Then, in the neighborhood of point

## Learning rate 

- Choosing a good value for the learning rate (step-size) $\gamma$ is important
    - Too small $\gamma$, convergence takes too long
    - Too large $\gamma$, the precess may "jump over" the local minimum

-- Insert image --

## Gradient descent for logistic regression 

## Summary

- Linear regression is a simple model for regression problems 
- Non-linearities can be modeled using basis functions 
- Logistic regression provides a way to use linear models in classification tasks- Prediction error consist of bias, variance, and irreducible error 
    - Simple models tend to have high bias and low variance; 
        complex models low bias and high variance 
    - We would want to find a model with low bias and variance 
    - Regularization is one way to control complexity of a model
