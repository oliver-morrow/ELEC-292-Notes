# What is pre-processing
- The concept of fixing minor or major issues within data, so they become more usable.
- It involves a number of different possible steps:
	- Missing data (imputation)
	- Normalization
	- Feature extraction
	- Dimensionality reduction
	- Noise reduction
	- Source separation
	- etc.
## Missing Data
- **Deletion**:
	- Pros: works fast, especially in large sets
	- Cons: may result in asynchronous signals, hard to handle by various systems
- **Imputation**: The process of replacing missing data with estimated values
	- Pros: More accurate than deletion, preserves *spatio-temporal* dimensions
	- Cons: requires processing -> memory, battery lag
	- Imputation techniques:
		- Simple imputation
		- Regression imputation
		- Expectation maximization
		- kNN
		- ML-Based
### Simple Imputation
- **Zero Replacement**: Replaces with zeros
- **Sample and Hold**: Replaces with previous value
## Normalization
- **What is normalization?** The process of modifying data such that it has zero mean and fits in a particular range.
- **Why?** In many cases, the values recorded by sensors can be influenced by electronic modules (amplification factors), noise, etc. In such cases, we need to create a uniform range across our dataset since we care more about the shape and patterns of the data as opposed to the actual values given by the sensors.
- This is also called the z-score operation
### What is noise?
- We have two notions which can degrade the quality of our data: noise and artifacts
- Noise may obscure/destroy features in a signal, while artifacts appear to be features but are not. However, they are used interchangeably in most books.
- Two main types: High frequency noise and low frequency noise
- Low frequency noise adds a slow moving noise to our signal, like an offset
- High frequency noise adds fast moving noise to our signal.
#### Filtering
To remove noise, we use filtering
- There's a number of ways to create filters, but we will just use the **Moving Average (MA)** filter that filters out *high frequency* noise.
- Therefore, MA is a low-pass filter.
- The concept behind MA is that they slide a window of size N, where N is usually an odd number, down the signal and average all of the points in that window.
- They replace each value in the input signal with the average value of values in a filter that precedes (and includes) that value.
- Intuitively, averaging a number of numbers reduces their noise as the noise cancels each other out.
- The operation will shrunk and shift the input signal by N-1 points.
- The longer the window size (N), the smoother the output will be.
- However, with stronger filtering, more information may be lost.
- So we need to find a good balance
## Feature Extraction
![[Pasted image 20240330132628.png]]
![[Pasted image 20240330132636.png]]
![[Pasted image 20240330132642.png]]
Feature extraction requires some design choice:
1. Window size: smaller gives more information (balance between too much data vs too little)
2. Window overlap: We mostly use 50% or even more overlap between windows. For example is very coming to use a rolling window that moves ahead **one sample at a time**. This helps retain important information.
3. Types of features: balance between too many features and high-dimensional data
4. 