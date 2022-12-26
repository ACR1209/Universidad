Is a type of [[Supervised Learning#Types of problems|regression algorithm]].  Is a linear equation that best describes the correlation of the explanatory variables with the dependent variable. This is achieved by fitting a line to the data using least squares.

![[Pasted image 20221226140852.png]]

## Mathematic foundation
In a multiple linear regression, meaning that the output gets affected by multiple [[Feature|features]], we have: 
$$y=\beta_0 + \beta_1*x_1 + \beta_2*x_2 + ... + \beta_p*x_p + \varepsilon$$
parameter $\beta_j$ of predictor variable $x_j$ represents the individual effect of $x_j$. It has an interpretation as the expected change in the response variable $y$ when $x_j$ increases by one unit with other predictor variables held constant. 

In a machine learning algorithm we want to obtain the $B_j$ where $B_0$ is the bias rate (where the regression starts on the y axis) and the rest are the feature rates (how much does and individual feature affect the outcome)

We can also see this as the dot product of two vectors, vector $\beta$ and vector $X$ where we store the bias rate in vector $\beta$  and the values of the features in vector $X$

$$\beta = \begin{bmatrix}
\beta_0\\
\beta_1\\
.\\
.\\
.\\
\beta_p\\
\end{bmatrix}
X = \begin{bmatrix}
x_0\\
x_1\\
.\\
.\\
.\\
x_p\\
\end{bmatrix}
$$
Thus the linear regression is:
$$ y=\beta*X$$

