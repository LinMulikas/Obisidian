**Basic Concept**

Use a [[Graph]] construction to represente all the points as the vertexes and the *distance* or *similarity* as the edges.

**Similraity**
- $\varepsilon$-distance.
	Connect two points iff 
	$$d(x_i, x_j) < \varepsilon,\ \varepsilon \sim (\frac{\log n}{n})^p$$


- k-nn.
	Connect $v_i$ to $v_j$ if $j$ is in the k-nearest neighbor of $i$.


- Full Connected graph.
	Firstly, connect all the points with the distance function
	$$d(x_i, x_j) = \exp\{-\frac{\|x_i - x_j\|^2}{(2 \sigma^2)}\}$$
	the $\sigma$ is a control factor. The adjacency matrix is not sparse.

