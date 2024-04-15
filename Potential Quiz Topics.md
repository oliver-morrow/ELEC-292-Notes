# PCA vs t-SNE
## Principal Component Analysis (PCA)
- **Linear Algorithm**: PCA is linear and identifies the direction (principal components) that maximizes the variance in the data.
- **Global Structure Preservation**: It works well when the global structure of the data is more important than the local relationships between data points.
- **Orthogonal Projection**: PCA projects data into orthogonal components that explain the most variance, resulting in uncorrelated features.
- **Scalability and Efficiency**: PCA is more efficient and easier to apply at scale, making it suitable for high-dimensional datasets.
- **Interpretability**: The principal components can sometimes be interpreted in terms of the original features, allowing insights into the structure of the data.
## t-SNE (t-Distributed Stochastic Neighbour Embedding)
- **Non-linear Algorithm**: t-SNE is a non-linear technique that is particularly well suited for the visualization of high-dimensional datasets.
- **Local Structure Preservation**: It excels at preserving local data structures and revealing clusters at several scales, making it great for exploratory data analysis.
- **Probabilistic Approach**: t-SNE converts the distances between data points into conditional probabilities that represent similarities, aiming to maintain these probabilities as much as possible in the reduced dimensionality.
- **Computational Complexity**: It is computationally more intensive, especially on very large datasets, and its results can vary depending on the specific parameters and random initialization used.
- **Interpretability**: The dimensions in the t-SNE output do not correspond to specific features of the data, making it less interpretable in terms of the original data structure.
`Key Differences:`
1. **Linearity vs. Non-linearity**: PCA is linear, while t-SNE is non-linear.
2. **Preservation of Structure**: PCA preserves global structure, whereas t-SNE is focused on preserving local neighborhood relationships.
3. **Scalability**: PCA is generally more scalable to large datasets.
4. **Use Cases**: PCA is often used for preprocessing and feature extraction, while t-SNE is primarily used for data visualization and exploration.
5. **Interpretability**: PCA components can sometimes be interpreted, but t-SNE dimensions lack direct interpretability.

In summary, the choice between PCA and t-SNE depends on the specific goals of your analysis, the size of your dataset, and the importance of interpretability in your application. PCA is typically used for dimensionality reduction in preprocessing steps to speed up learning algorithms or improve feature interpretability, while t-SNE is mostly used for exploratory data analysis and visualization to understand the structure of the data.
# Window Size Selection
1. **Balance Between Too Much and Too Little Data**
    - A smaller window size can capture more detailed information and may better reflect short-term patterns or variations in the data. However, it might also include more noise and result in higher computational costs due to the increased number of windows.
    - A larger window size smoothens the data, reducing the noise but also potentially losing important short-term variations.
2. **Contextual Relevance**:
    - The optimal window size often depends on the specific context of your data and the phenomena you are analyzing. For example, in time-series analysis or signal processing, the window size might be chosen based on the expected duration of the events or patterns of interest.
3. **Overlap Consideration**:
    - The slides suggest using a 50% or even more overlap between windows. This approach can help retain crucial information that might otherwise be lost at the boundaries of non-overlapping windows. It allows for a smoother transition and more continuity between windows but increases computational requirements.
4. **Empirical Testing**:
    - Often, the best way to determine the optimal window size is through empirical testing and validation. You might start with a window size based on theoretical considerations or previous studies and then adjust it based on the performance of your analysis or model.
5. **Performance Metrics**:
    - Evaluate the impact of different window sizes on performance metrics relevant to your task (e.g., classification accuracy, clustering purity, or signal reconstruction error). This evaluation can guide you to a window size that balances detail capture and noise reduction effectively.
6. **Computational Constraints**:
    - Larger datasets and smaller window sizes significantly increase computational costs. Consider your computational resources and the scalability of your analysis when choosing the window size.

The process of selecting the window size is iterative and may require adjustments based on the results of initial analyses. It's important to document the rationale for the chosen window size and any observations made during the selection process, as this information can be valuable for both the current analysis and future research.
# Calculation Questions
## Pre-Processing
1. **Normalization Solution**: Given a dataset `[15, 22, 29, 36, 43]`, perform min-max normalization on the dataset where the new minimum is 0 and the new maximum is 1. What are the normalized values?
Formula: $X_{norm}=\frac{{X-X_{min}}}{X_{max}-X_{min}}$
$X_{min}=15$, $X_{max}=43$
Normalized values:
- For 15 $\frac{{15-15}}{43-15}=0$
- For 22 $\frac{{22-15}}{43-15}=0.25$
- For 29 $\frac{{29-15}}{43-15}=0.5$
- For 36 $\frac{{36-15}}{43-15}=0.75$
- For 43 $\frac{{43-15}}{43-15}=1$
2. **Mean Calculation Solution**: Given the dataset `[122, 325, 245, 240, 268`, find the mean.
Mean formula: $\mu=\frac{{\sum x_{i}}}{n}$
Mean: 240
3. **Standard Deviation Solution**: Given the dataset `[5, 10, 15, 20 ,25]`, find the standard deviation when the mean is 15.
Variance: $\sigma^2=\frac{{\sum (x_{i}-\mu)^2}}{n}$
$\sigma^2=\frac{{(5-15)^2+(10-15)^2+(15-15)^2+(20-15)^2+(25-15)^2}}{5}=40$
Standard deviation: $\sigma=\sqrt{ 40 }\approx 6.32$
4. **Sample and Hold Solution**: An IMU sensor data reading for 10 seconds is recorded as `[300, 305, NULL, 310, NULL, NULL, 315, 320, NULL, 325]`. Using sample-and-hold, calculate the imputed values for NULL positions.
The new dataset will be: `[300, 305, 305, 310, 310, 310, 315, 320, 320, 325]`
## Data Visualization
1. **Interpreting Line Graphs**: A line graph shows the monthly sales of a company as follows: January - $2000, February - $2400, March - $2800, April - $3200. If the trend continues, calculate the expected sales for May and June.
Sales trend: January to April - $2000, $2400, $2800, $3200 Increase each month: $400 Expected Sales: May - $3200 + $400 = $3600, June - $3600 + $400 = $4000
2. **Area Charts**: An area chart displays the contribution of two sales representatives to total sales over four months. If Representative A contributed sales of $2000, $3000, $2500, $4000 and Representative B contributed $1500, $2500, $2000, $3500 in the respective months, calculate the total sales for the period and the percentage contribution of each representative.
Total sales = Sum of contributions of Rep. A and Rep. B over four months = $(2000 + 3000 + 2500 + 4000) + (1500 + 2500 + 2000 + 3500) = $16500 Percentage contribution of Rep. A = $\frac{11500}{16500} \approx 69.7$ 
Percentage contribution of Rep. B = $\frac{5000}{16500} \approx 30.3$
3. **Pie Chart Calculations**: A pie chart shows the market share of four companies as follows: Company A - 25%, Company B - 30%, Company C - 20%, Company D - 25%. If the total market size is $100,000, calculate the revenue for each company based on their market share.
Company A: 25% of $100,000 = $25,000 
Company B: 30% of $100,000 = $30,000 
Company C: 20% of $100,000 = $20,000 
Company D: 25% of $100,000 = $25,000
4. **Scatter Plot Correlation Coefficient**: Given a scatter plot with points: (1,2), (2,4), (3,6), (4,8), calculate the correlation coefficient. What does the correlation coefficient indicate about the relationship between the two variables?
Points: (1,2), (2,4), (3,6), (4,8) This dataset shows a perfect linear relationship, thus the correlation coefficient, $r$, is $1$.

# Window Sizes
You are working on a project analyzing accelerometer data collected from a wearable device to identify patterns of physical activity among users. The accelerometer records data at a frequency of 100 Hz. Your goal is to analyze segments of this data to classify different types of physical activities, such as walking, running, and sitting.

Given the following information, determine the appropriate window size for your analysis:

1. Walking typically involves cycles of approximately 1 to 2 seconds.
2. Running involves faster cycles, typically around 0.5 to 1 second.
3. Activities like sitting or standing involve minimal movement over periods longer than 2 seconds.
4. You aim to ensure that each window captures at least one full cycle of the activity, preferably more for walking and running, to accurately classify the activity.

**Question:** Based on the above information and aiming for a balance between resolution and computational efficiency, what would be an appropriate window size (in seconds) for analyzing the accelerometer data? Additionally, calculate the number of data points per window given the recording frequency.

**Options:** A) 0.5 seconds B) 1 second C) 2 seconds D) 4 seconds

**Solution:**

First, calculate the number of data points per second: 100 Hz means 100 data points per second.

- For A) 0.5 seconds, you would have 50 data points per window.
- For B) 1 second, you would have 100 data points per window.
- For C) 2 seconds, you would have 200 data points per window.
- For D) 4 seconds, you would have 400 data points per window.

Considering the need to capture at least one full cycle of walking or running within a window and preferably more, **Option C) 2 seconds** seems most appropriate. This choice balances capturing enough of each activity's cycle (especially for walking, which has the longest cycle) while maintaining computational efficiency and resolution. With this window size, you would capture 200 data points per window, providing a rich dataset for analysis without being overly burdensome on computational resources.