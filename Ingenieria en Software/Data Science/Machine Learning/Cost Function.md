Is a function that allows us to evaluate how good a [[Supervised Learning#Types of problems|regression algorithm]] adapts to the data by measuring the difference between the predicted value and the actual value. 

![[Pasted image 20221226143203.png]]

To calculate the error shown above we use a the [[Mean Square Error]] 

![[Mean Square Error#Mathematical formulation|]] 


## Optimize the cost function

To optimize the cost function, meaning that this function decreases the error to 0 we use the [[Gradient Descent Algorithm]] to minimize the error by taking the partial derivative of $J(\beta)$ like:

$$
\frac{\partial}{\partial} J(\beta) =  \frac{2}{m} * \sum_{n=1}^{m} (\hat{y}-y_n)
$$ $$ \beta_i =\beta_i - \alpha * \frac{\partial}{\partial} J(\beta_i) $$
