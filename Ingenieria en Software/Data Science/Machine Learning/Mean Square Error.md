In statistics, the mean squared error (MSE)or mean squared deviation (MSD) of an estimator (of a procedure for estimating an unobserved quantity) measures the average of the squares of the errors—that is, the average squared difference between the estimated values and the actual value. MSE is a risk function, corresponding to the expected value of the squared error loss. The fact that MSE is almost always strictly positive (and not zero) is because of randomness or because the estimator does not account for information that could produce a more accurate estimate. In machine learning, specifically empirical risk minimization, MSE may refer to the empirical risk (the average loss on an observed data set), as an estimate of the true MSE (the true risk: the average loss on the actual population distribution.

## Mathematical formulation
$$
J(\beta) = \frac{1}{m} + \sum_{n=1}^{m} (\hat{y}-y_n)
$$
Where:
- $m$ is the number of datapoints or actual values.
- $J(\beta)$ is how good the regression fits the data.
- $\hat{y}$ is the predicted value by the regression model.
- $y_n$ is the actual datapoint value.