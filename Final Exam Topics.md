1. Data set joins (Lab 3)
1. Writing procedures in SQL (Lab 3)
2. [[#Gradient Descent For Logistic Regression]]
3. Understanding [[#ROC Curve and AUC]], [[#Sensitivity, Recall, or true positive rate]], [[#Specificity]], and classifier thresholding
4. Understanding the role of variance in PCA and difference between PCA and TSNE
5. Lab-controlled data, In-the-wild data, mixed methods of data labelling, web scraping, crowdsourcing, automated data labelling, Test-Driven Development (TDD), Technological disruption & examples
6. Learn how to use sample and hold as well as zero mean replacement for imputing missing value.
7. Important thing to remember about normalization: When features in a dataset have vastly different scales, models can become biased towards the features with larger magnitudes. Normalization adjusts the scale of data so that different features contribute equally to the analysis or model training, thus removing the bias of large numbers.
8. Effects of larger and smaller window size of moving average on a signal.
# Data set joins
# Writing Procedures in SQL
## SQL Syntax
SQL's syntax is made up of 4 languages:
- [[#DDL]]: Data Definition Language
- [[#DML]]: Data Manipulation Language
- [[#DCL]]: Data Control Language
- [[#TCL]]: Transaction Control Language
### DDL
- Includes a set of statements which allow you to define or modify data structures and objects, like tables
- Includes the following commands:
	- CREATE
	- ALTER
	- DROP
	- RENAME
	- TRUNCATE
### DML
- The statement categorized under DML allow the user to manipulate data in the tables of a database.
- Includes the following commands:
	- SELECT
	- INSERT
	- UPDATE
	- DELETE
### DCL
- DCL tries to manage the rights that users have in databases.
- The following commands:
	- GRANT
	- REVOKE
### TCL
- Aims to manage transactions/changes made to the database.
- It includes:
	- COMMIT
	- ROLLBACK
	- SAVEPOINT
### DQL
- It is used to query or retrieve data from a table in the database.
- The main command is:
	- SELECT
## Why *relational* databases?
- A relational database stores data in tables with rows and columns, and allows relationships to be established between tables, while a regular database may store data in a variety of ways without the ability to establish relationships between data.
- Very time-consuming to perform complex queries on tables with many fields and records.
- Solving this, we use relational databases!
## How to adopt a database?
1. Design the database:
	- We consider our needs and resources
	- We use an entity-relationship diagram
2. Create the dataset using DDL
3. Manipulate it using DML
## Relational schemas
- Relational schemas are diagrams used to describe a database
- We generally use them to design and start coding our database
- ![[Pasted image 20240415130259.png|400]]
- ![[Pasted image 20240415130310.png|300]]
### Primary Key and Foreign Key
**Primary Key** is a column or possible a set of columns whose values:
- exist (NOT NULL);
- are unique for each table

**Foreign key** identifies the relationship between tables.
### Cardinality Constraints
![[Pasted image 20240415130521.png|400]]
## Data types in SQL
### String data types

| Name               | Syntax    | Example        |
| ------------------ | --------- | -------------- |
| Character          | CHAR      | CHAR(10)       |
| Variable character | VARCHAR() | VARCHAR(5)     |
| ENUM               | ENUM()    | ENUM('M', 'F') |
### Numeric data types

| Name           | Syntax                                    | Example      |
| -------------- | ----------------------------------------- | ------------ |
| Integer        | TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT |              |
| Fixed point    | DECIMAL                                   | DECIMAL(5,3) |
| Floating point | FLOAT, DOUBLR                             | FLOAT(5,3)   |
### Date, time, and files
| Name                | Syntax      | Example             |
| ------------------- | ----------- | ------------------- |
| Date                | DATE        | 2022-10-26          |
| Date time           | DATETIME    | 2022-10-26 12:38:01 |
| TIMESTAMP           | TIMESTAMP() | 1879812480          |
| Binary large object | BLOB        |                     |
## Creating a database in SQL
```sql
create database if not exists onq;
USE onq;

CREATE TABLE students (
	student_id INT NOT NULL,
	first_name VARCHAR(255),
	family_name VARCHAR(255),
	phone CHAR(12),
	major_code INT,
	supervisor_code INT,
	PRIMARY KEY (student_id)
)
```
### Constraints in SQL
- **NOT NULL**: If a field is specified as NOT NULL, you cannot insert information in that field unless you're inserting a proper value.
- **AUTO_INCREMENT**: Automatically increase the value of a field when you insert information.
- **PRIMARY KEY**: Illustrates the primary key of a table.
- **FOREIGN KEY**: Highlights the foreign key of a table.

**ALTER**: Adding a Unique Key
```sql
ALTER TABLE students
ADD UNIQUE KEY(phone);
```
**ALTER**: Adding a column to a table
```sql
ALTER TABLE students
ADD COLUMN gender ENUM('M', 'F') AFTER family_name;
```
**INSERT**: Adding a record to the table
```sql
INSERT INTO students (student_id, first_name, family_name, gender, phone, major_code, supervisor_code)
VALUES(20201456, 'Mike', 'Smith', 'M', '+1 343 333 ****', 10, 14);
```
## SELECT statement
- We use SELECT the most in SQL statements.
- It is used to retrieve information from SQL objects, and query data from a database.
- The simplest form of SELECT is:
	- `SELECT column_names FROM table_name;`
**SELECT ... WHERE**:
```sql
SELECT * FROM employees WHERE first_name = 'khalid' OR first_name = 'Maris';
```
Note: `*` means all employees.
Using patterns with **SELECT**:
```sql
SELECT * FROM employees WHERE first_name LIKE('%mo');
```
Note: `%mo` searches for names ending in `mo`.

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


