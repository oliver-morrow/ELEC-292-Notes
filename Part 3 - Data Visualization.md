# What is data visualization?
- What? It is the process of using graphs/plots to demonstrate data.
- When/Why?
	- Beginning: Becoming familiar with data is key to using the data in a project.
	- During: During a project, visualization helps gain **insights**, identify patterns/trends/outliers, and summarize information in large data sets.
	- End: At the end, results should be **communicated** with end-users/customers, often in a universal fashion.
# Different Types of Graphs and Charts
There are a variety of different graphs:
- Bar graph
- Column graph
- Line graph
- Dual axis charts
- Area charts
- Stacked bar charts
- Pie charts
- Scatter plots
## Bar Graphs/Column Charts
- Effective for comparing/contrasting data between different groups. Also, we can use it to track the changes of something with regards to a variable (e.g., time).
- Column charts are similar to bar graphs, we mainly use them to show differences among groups or track something with respect to a variable.
## Line Graphs
Mainly used to identify **trends** in data. Additionally, we use line graphs to track changes over usually a **continuous** variable.
## Dual Axis Charts
In dual axis charts, we have a shared x axis and 2 y axes. We mainly use these charts to find relationships (correlation) between two variables. Variables can be discrete, continuous, or one of each.
## Area Charts
Area charts look like line charts; however, the space between the lines and the x-axis is usually filled with a specific colour. We use these charts to show the **contribution** of something with respect to something else (ratio).
## Stacked Bar Charts
A form of bar chart. Similar to area charts, they are used when we have different items and we want to highlight their contribution (or ratio).
## Pie Charts
This chart depicts how much each item **contributes** **to** **the** **whole**. It's fractions of the total amount and highlights **composition** of something.
## Scatter Plots
We use scatter plots when we want to reveal the relationship between two different variables, examining their patterns and trends, identifying outliers, etc.
## Bubble Charts
Similar to scatter plots; but they exhibit more information using the area of the circles.
## Heat Maps
Heat maps show the relationship between two items or variables. It uses **colour** to represent values in a table or matrix. They make outliers **easy to spot**. An example of the application of heat maps is confusion matrices.
# Matplotlib
## Object Hierarchy in Matplotlib
**Figure Object**: This is the object which contains all of the Axes objects. It also keeps track of legends, colours, etc. Roughly speaking, think of it as a container, containing your plots.
**Axes**: It sticks onto the Figure object and contains an area to plot our charts. Axes usually contain 2 Axes objects (1 for x, 1 for y).
## Transformations in Matplotlib
# Curse of Dimensionality
- Curse of dimensionality is a term used to refer to the problem we face when working with high-dimensional data.
- Humans cannot observe more than 3 dimensions.
- Processing high dimensional data requires more resources.

**Solution?**
- Reduce dimensionality from N to M where M << N (ideally M = 2 or 3)
- What happens when we reduce dimensions?
	- We lose information!
- So how do we do this?
	- Aim to retain as much information as possible.
## Principle Component Analysis (PCA)
Assume we want to reduce the dimension of a figure from 2 to 1. One approach could be to remove one axis, e.g., y, which we will only keep x values.
![[Pasted image 20240330130901.png|400]]
- Removing the axis in this case loses us far too much information.
- In statistics and ML, the variance of samples can be regarded as the amount of **information** the samples are carrying. Therefore, the higher the variance, the more information we have. The equation for variance is: $$\sigma^2=\frac{{\sum_{i=1}^n(x_{i}-\mu)^2}}{n}$$
- Looking back at the original figure, what other 1D projection would retain more information than just removing y?
- PCA tries to find a coordinate system on which if you project the data, you obtain the highest possible variance.
 ![[Pasted image 20240330131005.png|400]]
# Pandas
- Library built on NumPy and used to handle tabular data.
- A useful data structure in pandas is called DataFrame.
- We can assign an arbitrary name to the columns or rows of a DataFrame.
# t-Distributed Stochastic Neighbourhood Embedding (t-SNE)
- Unlike PCA, which tries to preserve global structure and may lose local structure, t-SNE preserves both local and global structure.
- The intuition behind t-SNE is that it tries to match the conditional data distributions in high and low dimensions within a neighbourhood.
