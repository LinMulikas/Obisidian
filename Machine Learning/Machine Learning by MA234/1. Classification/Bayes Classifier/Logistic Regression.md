**Defintion**.

In the [[Classification Problem]] problem of [[Machine Learning]], *logistic regression*, is a [[Bayes Classifier]] method maximizing the posterior $P(Y | X)$ by the following steps.
- Assume $y = \mathrm{Sig}(w^T x)$.
- Learn a hyper plane, use the sigmoid function to map it into probability space.
	- $P(y = 1 | x) = \mathrm{Sig}(w^Tx)$.
	- $P(y = 0 | x) = 1  - P(y = 1 | x)$.
- Multiply classes problem can learn more than one classifier.
- Optimize the $w$ with $\hat w = \arg\max_w L(w)$, where the $L(w)$ is the likelihood function.
-  Solve the logarithm likelihood problem with *Newton's Method*.
---------
**Language**.

The *logistic regression* is a [[Bayes Classifier]], also a method for [[Classification Problem]] in [[Machine Learning]]. Using the philosophy of [[SVM]], act it with [[Sigmoid Function]], it's a [[Binary Classifier]].