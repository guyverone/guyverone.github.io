---
layout: post_layout
title:  "Coursera Machine Learning Week 1: Machine Learning Introduction"
excerpt: "What is machine learning? What can it do?"
date:   2017-05-13 09:00:00
mathjax: true
--- 

On March 19, 2016, one of the strongest Go player in the world, lee Sedol, has been defeated by Google DeepMind's artificial-intelligence program, AlphaGo.
After machine first beats mankind in 1997, again, artificial intelligence rises people's interest. Machine learning was widely known to the public by that game, and what behind AlphaGo is an artificial neural network, a deep learning method, which deep learning is a subset of machine learning.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/alphagovslee.jpg">
</div>
<br>

As an important field of Computer Science, Machine Learning nowadays become more applicable than decades ago because of enormous amount of data which generated every day by the internet or electronic devices and the powerful computational ability now we have. There are many areas have been targeted by machine learning: Data mining, Auto vechiles, Recommemdations, Healthcare, Gen engine, Market analyzing, etc. And it is changing our live right now.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/ml_apply.jpg">
</div>
<br>

### Machine Learning Definition
<li>
Arthur Samuel(1959). Machine Learning: Field of study that gives computers the ability to learn without being explicitly programmed.
</li>
<li>
Tom Mitchell(1998) Well-posed Learning Problem: A computer program is said to learn from experience E with respect to some task T and some performance P, if its performance on T, as measured by P, improves with experience E.
</li>

### Capability Of Machine Learning
<li>
Grew out of work in AI
</li>
<li>
New Capability for computers
</li>

### Use Cases That Using Machine Learning 
**Database mining**.Large datasets from growth of authomation/web.
<br>
E.g., Web click data, medical records, biology, engineering.

**Applications can't program by hand**
<br>
E.g., Autonomous helicopter, Handwriting recognition, most of Natural Language Processing(NLP), Computer Vision.

**Self-customizing programs**
<br>
E.g., Amazon, Netflix product recommendations.

**Understanding human learning(brain, real AI)**

### Machine Learning Algorithms
Generally, machine learning algorithms are classified into two categories: Supervised learning and unsupervised learning.

**Supervised Learning**
<br>
In supervised learning, the output of a bunch of data set have been well and correctly labeled, letting the algorithm to find the relationship between the input and the output.
<br>

Regression and Classification are two important components of supervised learning. In a regression problem, we are trying to predict within a continuous output, meaning that we are trying to map input variables to some continuous function. In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories.
<br>

Example:
<br>
Given data about the size of houses on the real estate market, try to predict their price. Price as a function of size is a continuous output, so this is a regression problem.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/housingpricepredict_regression.jpg">
</div>
<br>

We could turn this example into a classification problem by instead making our output about whether the house "sells for more or less than the asking price." Here we are classifying the houses based on price into two discrete categories.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/housingpricepredict_classification.jpg">
</div>
<br>

**Unsupervised Learning**
<br>
Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variable. We can derive this structure by clustering the data based on relationships among the variables in the data.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/newsclustering1.jpg">
<img src="/assets/pics/ml_week_one/newsclustering2.jpg">
</div>
<br>

In other words, letting a algorithm to find the commons or patterns among all these variables in the data. Clustering is putting data together which have common features, Non-clustering is discrete data into two or more groups by the group's own feature.
<br>


Example:
<br>
Clustering: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/genesclustering.jpg">
</div>
<br>

Non-clustering: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment.(i.e. identifying individual voices and music from a mesh of sounds as a cocktail party).
<br>
<i>Cocktail party problem algorithm: [W,s,v] = svd((repmat(sum(x.*x,1),size(x,1),1).*x)*x');</i>


### Model Representation ###
$x^{(i)}$ denotes the "input" variables
<br>
$y^{(i)}$ denotes the "output" or target variables that we are trying to predict.
<br>
$(x^{(i)},y^{(i)})$ denotes a training example.
<br>
$(x^{(i)},y^{(i)})$; i=1,...,m denotes a list of m training examples.
<br>
* Note that the superscript "(i)" in the notation is simply an index into the training set, and has nothing to do with exponentiation.

X denotes the space of input values.
<br>
Y denotes the space of output values.
<br>
Most situations, X = Y = $\mathbb{R}$. 
<br>


### Cost Function With One Parameter###
We do a simple way to predict the housing price, that is drawing a straight line to pass through all the $(x_i,y_i)$ points and makes them as close as possible by using Cost Function to make sure we are on the right direction.
<br>
For further understanding Cost Function, we need to introduce hypothesis Function first. hypothesis Function is our predict function, its a linear equation, which draws a straight line.
<br>
<i>Hypothesis Function formula</i>: $h_\theta(x) = \theta x$
<br>
Hypothesis Function is our predict function, x comes from the given data such as the size of the house, we need to find out &theta; to make this function work.
<br>
<i>Cost Function formula</i>: $J(\theta) = \frac{1}{2m}\sum\limits_{i=0}^m(h_\theta(x) - y)^2$
<br>
**Relationship between hypothesis function and cost function**
<br>
When cost function $J(\theta)$ gets its minimal value, then the &theta; is the exactly value which hypothesis function are looking for. In other words, cost function is a squared error function, it's made up by many tiny errors between $h_\theta(x)$ and y, when all these tiny errors gets minimal, then the output value of hypothesis function $h_\theta(x)$ produced closely approximates y. After that we can use hypothesis function $h_\theta(x)$ to predict such as the price of the house. Here are a grap to show you the relationship between them:
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/hypothesisAndCost.jpg">
</div>
<br>

### Cost Function With Two Parameters###
<br>
<i>Hypothesis Function formula</i>: $h_\theta(x) = \theta_0 + \theta_1x$
<br>
<i>Cost Function formula</i>: $J(\theta_0,\theta_1) = \frac{1}{2m}\sum\limits_{i=0}^m(h_\theta(x) - y)^2$
<br>

This time we need to find out values of $\theta_0,\theta_1$ when cost function $J(\theta_0,\theta_1)$ gets minimal. During two parameters, cost funcion becomes a three dimensions geometric figure, which look like a bowl-shape, consist of three axis: $J(\theta_0,\theta_1)$, $\theta_0$, $\theta_1$. 
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/bowlshape.jpg">
</div>
<br>

**Relationship between hypothesis function and cost function in two parameters**
<br>
Right below is a contour plot, which consist of contour lines. A contour line of a two variable function has a constant value at all points of the same line.
For example, These three green points found on the green line below have the same value for $J(\theta_0,\theta_1)$ and as a result, they are found along the same line. The circled x displays the value of the cost function for the grap on the left when $\theta_0$ = 800, and $\theta_1$ = -0.15.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/contour.jpg">
</div>
<br>

### Gradient Descent With One Parameter###
Gradient descent is a way that cost function $J(\theta)$ used to get to its minimal value by steps. 
<br>

<i>Gradient descent formula</i>: repeat $\theta = \theta - \alpha\frac{\partial}{\partial\theta}J(\theta)$
<br>
$\frac{\partial}{\partial\theta}J(\theta)$ is the slope of gradient, it could be positive or negative, but eventually it becomes 0 and $\theta$ would be stabilized on one value.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/gradientdescent_theta.jpg">
</div>
<br>

Picking that value of $\alpha$ is a technical skill. $\alpha$ is called learning rate, it can't be too small or too large. When $\alpha$ is too small, gradient descent would taked longer to converge. When $\alpha$ is too large, it would caused overshoot problem, makes gradient descent fail to converge, or even diverge.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/gradientdescent_alpha.jpg">
</div>
<br>

### Gradient Descent With Two Parameters###
<i>Gradient descent formula</i>: repeat $\theta_j = \theta_j - \alpha\frac{\partial}{\partial\theta}J(\theta_0,\theta_1)$
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/gradientdescent_optima.jpg">
</div>
<br>

### Gradient Descent For linear Regression ###
We substitute gradient descent and cost function below.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/gradientdescent_combine.jpg">
</div>
<br>

We update $\theta_0, \theta_1$ simultaneously.
<br>

<div class="imgcap">
<img src="/assets/pics/ml_week_one/gradientdescent_simultaupdate.jpg">
</div>
<br>

The point of all this is that if we start with a guess for our hypothesis and then repeatedly apply these gradient descent equations, our hypothesis will become  more and more accurate.
<br>

**Local optima and global optima**
<br>
Gradient descent would have a local optima problem. But for gradient descent for linear regression, it always gets the global optima, during it a convex function.
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
