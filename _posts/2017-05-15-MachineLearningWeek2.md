---
layout: post_layout
title:  "Coursera Machine Learning Week 2: Installing Octave, Feature Scaling, Normal Equation"
excerpt: "Using Octave to compute. Regularing feature variable range. Another method to substitute gradient descent."
date:   2017-05-15 13:00:00
mathjax: true
---  



### Octave Installation ###
Octave is a software for numerical computations, the language which uses similarly like Matlab, but Octave is free.
<br>
**Linux:**
<br>
Avoiding to install Octave 4.0.0, during Andrew Ng do not recommend this version. It is said that that version of Octave could cause programming assignments submitting fail. We install Octave through PPA(Personal Package Archive), instead of installing from linux distribution’s software repositories.
<br>
To set up your system to install Octave:
<br>

```terminal```
sudo apt-add-repository ppa:octave/stable
sudo apt-get update
sudo apt-get install octave
```

When it done, i get a version of 4.0.2 by that time, and it works well.

### Model Representation ###
This week we introduce multivariate linear regression and notation for equations where we can have any number of input variables.
<br>
$x^{(i)}_j$ = value of feature $j$ in the $i^{th}$ training example
<br>
$x^{(i)}$ = the column vector of all the feature inputs of the $i^{th}$ training example
<br>
$m$ = the number of training examples
<br>
$n$ = $\mid x^{(i)} \mid$; (the number of features)
<br>

### Multivariate Linear Regression ###
Linear regression with multiple variables is also known as "multivariate linear regression".
<br>
The multivariable form of hypothesis function accommodating these multiple features is as follows:
<br>
$h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2x_2 + \theta_3x_3 + \cdots + \theta_nx_n$
<br>
For concisely represent multivariable hypothesis function, we using the definition of matrix multiplication:
<br>
$h_\theta(x) = \begin{bmatrix} \theta_0&\theta_1&\cdots&\theta_n \end{bmatrix}$ $$\begin{bmatrix} {x_0}\\ {x_1}\\ {\vdots}\\ {x_n}\\ \end{bmatrix}$$ $= \theta^T x$
<br>
This is a vectorization of our hypothesis function for one training example.
<br>
Remark: Note that for convenience reasons in this course we assume $x_0^{(i)} = 1$ for $(i \in 1,...,m)$
<br>
The following example shows us the reason behind setting $x_0^{i} = 1$:
<br>
$$X = \begin{bmatrix} x_0^{(1)}&x_0^{(2)}&x_0^{(3)}\\ x_1^{(1)}&x_1^{(2)}&x_1^{(3)} \end{bmatrix}$$ $, \theta = $ $$\begin{bmatrix} \theta_0 \\ \theta_1 \end{bmatrix}$$
<br>
As a result, you can calculate the hypothesis as a vector with:
<br>
$h_\theta(X) = \theta^TX$
<br>

### Gradient Descent For Multiple Variables ###
Repeat until convergence: {
<br>
$\theta_j := \theta_j - \alpha\frac{1}{m}\sum\limits_{i=1}^m(h_\theta(x^{(i)}) - y_j^{(i)})$ for $j := 0...n$
<br>
}
<br>

### Gradient Descent in Practice I - Feature Scaling ###
There two techniques to help to speed up gradient descent are feature scaling and mean normalization. This is because $\theta$ will descend quickly on small ranges and slowly on large ranges, and so will oscillate inefficiently down to the optimum when the variables are very uneven. But these aren't exact requirements.
<br>

**feature scaling**
<br>
Feature scaling involves dividing the input values by the range, make sure features are on a similar scale:
<br>
$x_i := \frac{x_i}{s_i}$ 
<br>

**mean normalization**
<br>
We use mean normalization to perform feature scaling. Mean normalization involves subtracting the average value for an input variable from the values for that input variable resulting in a new average value for the input variable of just zero.
<br>
$x_i := \frac{x_i - \mu_i}{s_i}$
<br>
*$\mu_i$ is the average of all the values for feature(i) and $s_i$ is the range of values(max - min), or $s_i$ is the standard deviation.
<br>

### Gradient Descent in Practice I - Learning Rate ###
**Debugging gradient descent(recommend)**
<br>
Plotting a contour, which its x-axis with the number of iterations, and the cost function, $J(\theta)$ over the number of iterations of gradient descent. Make sure the gradient descent works well by visuallizing.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_two/debugginggradientdescent.jpg">
</div>
<br>

**Automatic convergence test**
<br>
Declare convergence if $J(\theta)$ decreases by less than E in one iteration, where E is some small value such as $10^{-3}$. However in practice it's difficult to choose this threshold value.
<br>

**The choosing of learning rate**
<br>
The learning rate $\alpha$ shouldn't be too small, otherwise gradient descent would converge slowly.
<br>
The learning rate $\alpha$ shouldn't be too lager neither, otherwise gradient descent would even not converge(because of overshoot problem).
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_two/choosinglearningrate.jpg">
</div>
<br>

### Features and polynomial Regression ###

**Feature reducing**
<br>
Reducing features from serveral to one, such as, we substitute $x_1$ and $x_2$ with $x_3$ in the form of $x_3 = x_1 * x_2$, etc. For exmaple, the frontage of a house($x_1$) is 50 feet and the depth of the house($x_2$) is 100 feet, then the size of the house or the land area($x_3$) is 500 ${feet}^2$, we can combine $frontage$ and $depth$ into a new feature $land area$ by taking $frontage * depth$.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_two/featurereducing.jpg">
</div>
<br>

**Polynomial Regression**
<br>
We can change the behavior or curve of our hypothesis function by making it a quadratic, cubic or square root function(or any other form), as follows:
<br>
quadratic: $h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2x_1^2$
<br>
cubic: $h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2x_1^2 + \theta_3x_1^3$
<br>
square root: $h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2\sqrt{x_1}$
<br>
pros: hypothesis function would fit the data well.
<br>
cons: range of $x_1^2$ and $x_1^3$ will increase rapidly and exponentially. Now, feature scaling becomes very important.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_two/polynomialregression.jpg">
</div>
<br>

### Normal Equation ###
Besides gradient descend, there is another way to minimize hypothesis function $J(\theta)$, that is normal equation.
<br>
Normal equation formula: $\theta = {(X^TX)}^{-1}X^Ty$
<br>
*There is no need to do feature scaling with the normal equation.
<br>

Comparision of gradient descent and normal equation:
<br>
<div class="imgcap">
<img src="/assets/pics/ml_week_two/normalequationCgradientdescent.jpg">
</div>
<br>
When the number of features gets so big, like, exceeds 10,000 it might be a good time to go from normal equation to gradient descent. Otherwise, we prefer to  using normal equation.
<br>

### Normal Equation Noninvertibility ###
If $X^TX$ is noninvertible, the common causes might be having:
<li>Redundant features, where two features are very closely related(i.e. they are linearly dependent).</li>
<li>Too many features(e.g. m $\le$ n). In this case, delete some features or use "regularization".</li>
Solutions to the above problems include deleting a feature that is linearly dependent with another or deleting one or more features when there are too many features.
<br>
<br>

<b>
Note: All materials come from Coursera Andrew Ng's Machine Learning Class.
</b>
<br>
<b>
Acknowledgement:
<br>
Coursera
<br>
Andrew Ng
</b>
<br>
<br>
<b>References:
<br>
http://wiki.octave.org/Octave_for_Debian_systems
<br>
https://en.wikipedia.org/wiki/Feature_scaling
</b>













