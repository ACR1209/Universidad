**1.) What is Linear Regression? Can you share the intuition behind linear regression? Why regression why not classification?** 
Linear regression is getting the tendency of the data into a line equation that allows to predict how will the data look in the cases that we don't have. We use linear regression in the case of continuos values and classification in the case of discrete data.

**2.) Write about Linear regression algorithm as a pseudocode and explain about linear regression.**
```
PROCEDURE linearRegression(x, y):
	mean_x = mean(x)
	mean_y = mean(y)
	beta_1_num = 0
	beta_1_den = 0
	FOR EACH index of x
		beta_1_num += (x[i] - mean_x) * (y[i] - mean_y)
		beta_1_den += (x[i] - mean_x) ** 2
	beta_1 = beta_1_num / beta_1_den
	beta_0 = mean_y - (beta_1 * mean_x)

	RETURN (beta_0, beta_1) 
END
```

**3.) Implement a linear regression algorithm from scratch using any of your fav programming languages. ( don’t use any libraries )**
```jupyter
def linearRegression(x: list[int], y:list[int])->tuple[int]:
	mean_x: float = sum(x) / len(x)
	mean_y: float = sum(y) / len(y)
	beta_1: float = sum([(x[i] - mean_x) * (y[i] - mean_y) for i in range(len(x))]) / sum([item - mean_x for item in x])
	beta_0: float = mean_y - (beta_1 * mean_x)
	return (beta_0, beta_1)  
```

**4.) What is Overfitting and underfitting?**
**5.) How can we prevent underfitting and overfitting?**
**6.) What is regularization?**
**7.) Write Ridge and Lasso regression from scratch in python?** 
**8.) Take a regression dataset from UCI ML Repo and Implement Linear Regression and regularized linear models using Sklearn.**