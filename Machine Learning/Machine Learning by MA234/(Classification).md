# 0. Introduction


# 1. kNN


**Comments**

- Simplest supervised learning method, use the prior knowledge.

- Low bias, high variance.

**Conclusion**

- Advantages
  Not sensitive to outliers, easy to implement and parallelize, good for large training set.

- Drawbacks
  Sensitive to k, take large storage, computationally intensive.

**Algorithm**

- Input: training set with labels and the sample to be predicted.
- Output: predict label of x.

**Steps**
1. Compute $d(x, x_i)$.
2. Sort for finding the smallest k points.
3. Vote the label of x by majority.

# 2. Bayes Classifier

Learn the conditional distribution, with the assumotion the classifier is actually a piecewise constant function.

### Hypothesis Space

Assume $\mathcal Y \in \{y_1, \ldots, y_n\}$ and $f: \mathcal{X \to Y}$ is the distribution of , a picewise constant function.

### Loss function
- Using the 0-1 loss, learning by minimizing
  $$\mathcal E(f) = E_{P(X, Y} L(Y, f(X)) = 1 - P(Y = f(X))$$

### Prediction

Predict by bayes law

$$f^*(x) = \arg \max_c P(Y = c | X = x)$$

### Error rate

$$\inf_\mathcal{E}(f) = \mathcal E(f^*) = 1 - P(Y = f^*(x))$$

### Decision boundary

The boundary devides the domain into K parts, where the predict will be a constant.

# 3. Decision Tree

## Basic Idea

Considering every properties can be chosen as a *decision node*, which can be used into partition the data. After sorting the importance of the *decision node* by some *criterion*, we can build a tree. Then for every input, we can use the tree from the root to leaf to divide the possible lables of $x$.

As the decision tree use the above idea will always get a binary division, which means it will split the plane with orthogonal lines.


## The criterion of build a tree

How to measure the good of a node can represente, here we need to introduce some concept.

The impurity means a node can't give useful information to the decision.

We build a tree by the following steps.

1. Decide a criterion to represente the uncertainty.
2. Calculute the gain of certainty by split, also the loss of uncertainty by split (same as that).
3. Optimize the gain or loss.



### Gini Index Method

#### Gini Index

[[Gini Index]].

Define Gini Index of a node $t$, by

$$G(t) = 1 - \sum_{i = 1}^C p(i | t)^2$$
One should notice the right conditional probability part has a sum 1.


[[The maximum of Gini Index]].

Note that the right summary part measure the total probability that this point can determined. Thus Gini Index shows the uncertainty, impurity, of using the node to devide. 

Note that, in a binary classfication problem decided by a node always has the conditional probability with $p_1 + p_2 = 1$. Thus, considering the Gini Index, which will get

$$1 - p_1^2 - p_2^2$$

Only when $p_1 = p_2 = 1/2$, the probability get the maximum $1/2$. Thus, all the note give a Gini index less than $1/2$. The smaller the better.

Thus $1 - G(t)$ is useful.




#### Gini Index of a Split

[[Gini Index of a Split]].
Considering the split at node $t$, casue $K$ children node classes. 

Then define the remained [[Gini Index]] after the split as [[Gini Index of a Split]], by 
$$G_{s}(t) = \sum_{k = 1}^K \frac{n_k}{n} G(k)$$
where $k$ is the k-th child node of $t$.



**Build a tree**

Considering a tree, we need to sum all the Gini index of children as $Gini_{index}$.


#### Gini Index Gain
As [[Gini Index]] show the uncertainty of a node, we try to find the best split, which means it get a maximum gain of $G(t) - G_s(t)$.



### Information Gain Method

#### Information Gain

[[Information Gain]].
Use the Entropy at node $t$ to measure the uncertainty

$$H(t) = -\sum_{C} p(c | t) \log_2(p(c | t))$$

- maximum at $p(c|t) = 1/c$, minimum at $p(c|t) = 1$.


#### Split information (ID3)

Considering the overfit problem, we need to control the max information get from the split

$$H_{split} = -\sum_{K}\frac{n_k}{n}\ln$$

and the optimation will tends to get a bigger gain information and a smaller split information. Thus we can use the ratio to get a same result.

- But the method is easy to divides too many children nodes.


### Misclassification Error

Use the *misclassification error*, one can prune the tree.

#### Misclassification Error.
The least possibility of misclassification.
$$Error(t) = 1 - \max_c p(c | t)$$
  
The slides Comparing Three Impurity Measures has an example, the example.

> (400, 400) means two unknow calsses just know they are two classes, noted as points1, points2.
> And node A split them into c1: (300, 100), c2: (100, 300)
> And node B split them into c2: (200, 400), c2: (200, 0)
>
> Thus, we need to assume the initial classes of poitns by (c1, c2) or (c2, c1), then can calculates the max error.

### Comparing Three Impurity Measures

![[Pasted image 20230320154423.png]]
#### Gini Index

#### Entropy

#### Misclassification Error


- 上面两个更敏感
- 上面两个可以用来建立树
- 三者都可以用来剪枝


# Logistic Regression
[[Logistic Regression]].


# Linear Discriminant Analysis (LDA)
