*Bayes classifier* is the classifier try to maximum the posterior $P(Y | X)$.

Recall the [[Bayes Theorem]]
$$P(Y | X) = \frac{P(X, Y)}{P(X)} = \frac{P(X | Y)P(Y)}{P(X)}$$
The method including
- Directly estimate the $P(Y | X)$.
	Use a model with parameter $w$, one can optimize the
	$$P(Y | X, w)$$
	to solve this proglem.
	
	**Related Category**.
	[[Logistic Regression]].
	
	
- Use the right equality to esitimate $P(Y | X)$.
	With the assumption that $P(X)$ is a constant, one can assume the distribution of $P(Y)$ and $P(X | Y)$. 
	
	**Related Category**.
	[[Linear Discriminant Analysis]]