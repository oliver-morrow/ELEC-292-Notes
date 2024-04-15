1. Data set joins (Lab 3)
1. Writing procedures in SQL (Lab 3)
2. Implementing gradient descent for logistic regression
3. Understanding ROC, AUC, sensitivity, specificity, and classifier thresholding
4. Understanding the role of variance in PCA and difference between PCA and TSNE
5. Lab-controlled data, In-the-wild data, mixed methods of data labelling, web scraping, crowdsourcing, automated data labelling, Test-Driven Development (TDD), Technological disruption & examples
6. Learn how to use sample and hold as well as zero mean replacement for imputing missing value.
7. Important thing to remember about normalization: When features in a dataset have vastly different scales, models can become biased towards the features with larger magnitudes. Normalization adjusts the scale of data so that different features contribute equally to the analysis or model training, thus removing the bias of large numbers.
8. Effects of larger and smaller window size of moving average on a signal.
# Gradient Descent For Logistic Regression
w2x2A regression model can be characterized as: (assuming $x\in \mathrm{R}$) $$f(x,w)=w_{0}+w_{1}x+w_{2}x^2+\dots+w_{m}x^2=\sum_{j=0}^{m}w_{j}x^j$$
If $m=1$, then we have a linear regressor (linear regression model). Otherwise, it is non-linear. In non-linear cases, we can have term like.

To find the best *regression model*, we need to quantify the error that a model would create (called a **loss** or cost function). The most natural way to quantify the error is to use the mean squared error. That is, we calculate the sum of *the sum of the squared differences between the predictions and the ground truth values*: $$J(w)=\frac{1}{2m}\sum_{i=1}^{m} (f(x(i))-y(i))^2$$
In the above equations, $m$ is the total number of data pointers (aka samples), $f(x(i))$ represents the model's output (predictions) which depends on $w$.

**Goal**: Find $w$ such that $J(w)$ is minimum.
## Summary
- In summary, if we find the right $w=w_{0},w_{1},w_{2},\dots,w_{m}$, we have trained our regression model.
- Accordingly, we can have infinite models, but some are better than others (because for some $w$ values, we will have less error ($J$) in the model).
- How good the model is will depend on the $w$, which itself will depend on (1) how good our data is, (2) algorithms we use to get from our data to $w$.
- To solve this problem, i.e., find $w$ such that $J(w)$ is minimum, we can use analytical calculations (bad!) or optimization solutions like **Gradient Descent** (GD).
## Logistic Regression
### Classification
- Question: How can we use a regression model to classify data into distinct classes?
- Problem: Regression models generate *unbounded* values. For instance, if we train a regression model to regress to 0 and 1 for cat vs. dog classification, it might generate 29!
	- We need a bounded regressor to be able to use it as a classifier.
- Question: For a binary classification problem (only two classes), what should this bound be?

Recall: $$g(x)=\frac{1}{1+e^{-x}}$$Its output is always bounded between 0 or 1; we can interpret its output as the ***probability*** value.
- For variables (features) $x_{1},\dots x_{m}$ $$f(x)=\frac{1}{1+e^{-(w_{0}+w_{1}x_{1}+w_{2}x_{2}+w_{m}x_{m})}}$$
- When the classification problem only has two classes (e.g., cat vs. dog; apple vs. orange, etc), we call this a binary problem.
- Question: the output of logistic regression is a probability between 0 and 1, so how can we convert it to distinct classes, 0 or 1?
- The loss function typically used for logistic regression is called the cross-entropy loss: $$J(w)=-\sum_{i=1}^my(i)\log(f(x(i)))+(1-y(i))\log(1-f(x(i)))$$
- An optimizer like Gradient Descent (GD) is used to solve $w$ such that $J(w)$ is minimized.
## Mathematics Behind GD: Gradient Vector
Gradient vector of a scaler function $f(x_{1},x_{2},\dots x_{n})$, denoted by $\nabla f$, is a vector containing all the partial derivatives of the function:$$\nabla f=\left( \frac{\partial f}{\partial x_{1}},\frac{\partial f}{\partial x_{2}},\dots,\frac{\partial f}{\partial x_{3}} \right)$$It can be proved that $\nabla f$ vector points toward the steepest ascent (Calculus II).
### Gradient Descent Algorithm
Repeat until convergence {
$$\theta _{i}=\theta_{i}-\alpha {\frac{\partial J(.)}{\partial \theta_{i}}}\;\text{for all i}$$
}
In vector form: $\theta=\theta-\alpha \nabla J(\theta)$
## Model Selection and Evaluation
So, now how do we train the model using GD?
### Step 1
Divide our data into two distinct parts (usually after shuffling)
1. Training set: used to train the model (find the optimum values of model parameters). Sometimes the training set itself is divided into train and validation sets to better tune the hyperparameters (i.e., to figure out what model should be used on the test set, the validation set is used to tune the model. Learning rate is a hyperparameter)
2. Test set: used to evaluate the generalization of the model. That is, the ability of the model to do classification on data which is not involved in the training process itself.

**It is VERY important that there is no leakage between training and testing sets. Otherwise, the true performance is unknown.**
### Step 2
We train the model on the training set, and then test on the test set to report the performance metrics. There are. number of training/testing schemes. Though, it is common to leave either 20% or 30% of the data for testing, or perform k-fold cross-validation.

In k-fold cross validation, the data is divided into k parts, and:
- trained on part 1,...,k-2,k-1, tested on part k
- trained on part 1, k-2, k, tested on part k-1
- trained on part 1,..., k-3, k-1, k tested on part k-2
- ...
Then all the results are averaged and the mean and STD are reported.
![[Pasted image 20240414222049.png|400]]
## Evaluation Metrics
Note: the following criteria are calculated using the test set.
### Confusion Matrix
In the case of binary classification, it is a $2*2$ matrix, seen below:
![[Pasted image 20240414222405.png|200]]
**TP**: The number of positive samples which are correctly predicted positive.
**FP**: The number of negatives samples incorrectly predicted as positive.
**FN**: The number of positive samples incorrectly predicted as negative.
**TN**: The number of negative samples which are correctly predicted negative.
### Accuracy
Accuracy is the ratio of correct predictions made by the model to the total number of predictions made.$$\text{Accuracy}=\frac{TP+TN}{TP+FP+TN+FN}$$
### Sensitivity, Recall, or true positive rate
This captures how our model is performing on the detection task (in terms of detecting the thing we're looking for). $$\text{Sensitivity}=\frac{TP}{TP+FN}$$
### Specificity
This shows how our model is performing on the negative class. $$\text{Specificity}=\frac{TN}{TN+FP}$$
### Precision
This shows how many samples are truly classified by the model out of all the predictions$$\text{Precision}=\frac{TP}{TP+FP}$$
### F1 Score
$$\text{F1}=\frac{2*\text{Precision}*\text{Recall}}{\text{Precision}+\text{Recall}}=\frac{2*TP}{2*TP+FP+FN}$$
### False Positive Rate
$$\text{FPR}=\frac{FP}{FP+TN}$$
### ROC Curve and AUC
**ROC**: Receiver operating characteristics curve is a curve which shows the performance of the model in all classification *thresholds*. The $X$ axis represents the sensitivity in a given threshold (or FP rate), and $Y$ axis shows the specificity in a given threshold (or TP rate)

**AUC**: Area under curve of the ROC curve.

The goal is to choose a model with the highest AUC possible.


