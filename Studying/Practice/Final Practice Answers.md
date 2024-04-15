# SQL
1. Given the 2 tables below, create the output of the following query.
![[Pasted image 20240415143300.png]]
**Query**:
```sql
SELECT students.first_name, students.last_name, majors.major_code
FROM students
RIGHT JOIN majors
ON students.student_id = majors.student_id;
```

**Understanding**:
1. Selecting `first_name`, `last_name`, and `major_code` from the `students` table.
2. Performing a RIGHT JOIN with students and majors, where students is the left table and majors is the right one.
	1. The RIGHT JOIN essentially says "give me all records from the right table (`majors`), and the matching ones from the left (`students`). If there's no match from the left, fill with NULL.
3. The match we are looking for is by `student_id`.

**Output**:

| first_name | last_name | major_code |
| ---------- | --------- | ---------- |
| Trevor     | Mcdonald  | 101        |
| Trevor     | Mcdonald  | 120        |
| Ali        | Gerretsen | 5080       |
| NULL       | NULL      | 002        |
# Gradient Descent (GD)
2. Given the following logistic regression with 1-D input $x_{i}\in R$, implement the gradient descent algorithm for updating $w_{0}$. $$f(x_{i})=\frac{1}{1+e^{-(w_{0}+w_{1}x_{1})}}$$ $$J(w_{0},w_{1})=-\frac{1}{m}\sum_{i=1}^{m}[y_{i}\log^{f(x_{i})}+(1-y_{i})\log^{(1-f(x_{i}))}]$$


# ROC and AUC
3. Given the data below, calculate true positive rate (tpr) and false positive rate (fpr) at different thresholds. Draw the resulting receiver operating characteristic (ROC) curve and calculate the area under curve (AUC). (labels: 1: circle, 0: triangle)
![[Pasted image 20240415154422.png]]

# PCA
4. Suppose that you are assigned a task to apply principal component analysis (PCA) on a 2D dataset for dimension reduction. You do the calculations and find out that the first principal component is positioned at an angle of 5 degrees contraclockwise from the x-axis. What can you infer about the variance of the dataset along x and y axes?

**Answer**: Since the first principal component is aligned only 5 degrees from the x axis, it provides a good indication of the variance of the set. The first principal component provides the direction of maximum variance in the dataset. Since it's only slightly tilted from the x-axis, this suggests that a significant portion of the variance in the dataset occurs along the x-axis (or very close to it) with less variance along the y-axis.
# Data Labelling
5. Imagine that you're spearheading an initiative to develop an augmented reality (AR) application that uses a smartphone's camera to identify and provide educational content about various animal species encountered in nature. The goal is to make zoology engaging and accessible for both students and wildlife enthusiasts, offering instant information about animals through image recognition. Your team decides to compile and utilize a comprehensive dataset consisting of both professionally captured images in zoos and wildlife reserves and user-contributed photographs from their natural encounters. Given the assortment of data sources, including user submissions, your team opts to employ a hybrid approach for data annotation and validation. Considering this scenario, answer the following questions:
	1. How would your team execute a hybrid/mixed approach for data labelling?
	2. What challenges could emerge from integrating professional images with user-contributed wildlife photos, and how would you tackle these challenges to ensure the AR application's success?

**Answer** **1**: To ensure proper labelling in a hybrid model, the team would use an automated labelling tool to first distinguish types of animals quickly, then employ wildlife experts to manually review and correct any unclear or misinterpreted images. This ensures the images are accurate, even for some rare animals that the automated tool may not be able to classify. Also, by letting app users report errors or confirm data, the team can improve the app on an ongoing basis.

**Answer** **2**: Some of the challenges could be that the user-contributed photos could have large signal noise or poor lighting, affecting accuracy. To improve this, the team can use pre-processing techniques to clean the photos, remove noise, and ensure optimal accuracy regardless of photo quality.

# Pre-Processing/Normalization
6. As a data scientist working for a nutrition analysis startup, you are tasked with developing a machine learning model to predict the likelihood of vitamin deficiencies in individuals based on their dietary intake and blood test results. Among the features in your dataset are Vitamin D level, measured in nanograms per milliliter (ng/mL) with values typically ranging from 20-50 ng/mL, and Daily Caloric Intake, measured in calories, with a typical range from 1,200 to 3,500 calories per day. Considering the substantial difference in scale between these measurements, what preprocessing step would you deem essential to perform on these features before using them in your predictive model, and why?

**Answer**: Given the significant disparity in scale between Vitamin D levels and daily caloric intake, it is essential to apply normalization as a preprocessing step before incorporating these variables into the machine learning model. Normalization ensures that each feature contributes proportionately to the model's prediction, preventing features with larger numerical ranges from dominating those with smaller ranges. Two common methods are normalization and standardization. Normalization rescales the data into a 0,1 range. Standardization rescales the data to have a mean of zero and standard deviation of 1. By scaling the values to a smaller scale, the predictive model can more effectively learn patterns and relationships between features and predict the likelihood of vitamin deficiencies.
# Filtering
7. The TechInspect team is developing a system for diagnosing problems in industrial machinery by analyzing acoustic signals. They encounter a challenge with low-frequency background noise interfering with their signal data. Which type of filter (High-pass filter/Low-pass filter) would be most effective for isolating the relevant frequencies indicative of machinery faults? Explain your reasoning.

**Answer**: A high-pass filter would be most effective, since it blocks low frequency noise, and allows high frequency signals to pass. A high-pass filter allows frequencies higher than its cutoff frequency to pass through while attenuating frequencies lower than the cutoff frequency. Given that the noise is of low frequency, the High-pass filter would effectively remove or reduce the unwanted noise, thereby allowing the system to focus on the higher frequency components that are more indicative of machinery faults.