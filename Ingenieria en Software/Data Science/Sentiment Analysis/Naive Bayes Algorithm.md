Is a classification technique based on Bayes' Theorems with the assumption of independence among predictors. In simple terms, a Naive Bayes classifier assumes that the presence of a particular feature in a class is unrelated to the presence of any other feature.

For example, it takes an object let's say an apple and takes it's characteristics (it's red, round, has a steam, etc.) and assumes that if it has a lot of apple characteristics then it must be an apple.

## The Naive Bayesian Equation

Bayes theorem provides a way of calculating [[Posterior Probability|posterior probability]] P(c|x) from P(c), P(x) and P(x|c). Look at the equation below:

$$P(c|x)=\frac{P(x|c)P(c)}{P(x)}$$
-   _P_(_c|x_) is the posterior probability of _class_ (c, _target_) given _predictor_ (x, _attributes_).
-   _P_(_c_) is the prior probability of _class_.
-   _P_(_x|c_) is the likelihood which is the probability of _predictor_ given _class_.
-   _P_(_x_) is the prior probability of _predictor_.

## How does the algorithm works? 
As an example let's suppose we have a dataset of if players played a game depending on the weather. Now, we have to classify whether players will play or not based on these weather  condition. To do this we follow these steps:

Weather | Played
--------|-------------
Sunny| No |
Overcast|Yes
Rainy|Yes
Sunny|Yes
Sunny|Yes
Overcast|Yes
Rainy|No
Rainy|No
Sunny|Yes
Rainy|Yes
Sunny|No
Overcast|Yes
Overcast|Yes
Rainy|No
Dataset of if game was played or not based on weather conditions

1. Convert dataset to frequency table

	**Frequency Table**
	
	| Weather | No | Yes |
	| - | - | - |
	|Overcast|0|4|
	|Rainy|3|2|
	|Sunny|2|3|
	|**Total**|**5**|**9**|

1. Create a likelihood table by finding the probabilities, for example Overcast probability $P(Overcast)=\frac{4}{14}=0.29$  and $P(Playing)=\frac{9}{14}=0.64$ 

	|Weather|No|Yes|$P(Weather)$|
	|--------|---|-|-|
	|Overcast| 0 | 4 | $\frac{4}{14}=0.29$|
	|Rainy|3|2|$\frac{5}{14}=0.36$|
	|Sunny|2|3|$\frac{5}{14}=0.36$|
	|**Total** | **5**|**9**|
	|**Probability**|**$\frac{5}{14}=0.36$**|**$\frac{9}{14}=0.64$**||

3. Now use [[Naive Bayes Algorithm#The Naive Bayesian Equation|Naive Bayesian Equation]] to calculate the posterior probability for each class. The class with the highest posterior probability is the outcome of the prediction.


### Example
Using the likelihood table above "Players will play if weather is sunny. Is this statement correct?".

$$ P(Yes|Sunny)=\frac{P(Sunny|Yes)*P(Yes)}{P(Sunny)}=\frac{\frac{3}{9}*0.64}{0.36}=0.593$$

Where $P(Yes|Sunny)$ is the probability of the players playing on a sunny weather.

## Pros 
- It is easy and fast to predict class of test data set. It also perform well in multi class prediction
- When assumption of independence holds, a Naive Bayes classifier performs better compare to other models like logistic regression and you need less training data.
- It perform well in case of categorical input variables compared to numerical variable(s). For numerical variable, normal distribution is assumed (bell curve, which is a strong assumption).

## Cons
- If categorical variable has a category (in test data set), which was not observed in training data set, then model will assign a 0 (zero) probability and will be unable to make a prediction. This is often known as “Zero Frequency”. To solve this, we can use the smoothing technique. One of the simplest smoothing techniques is called Laplace estimation.
- Another limitation of Naive Bayes is the assumption of independent predictors. In real life, it is almost impossible that we get a set of predictors which are completely independent.

