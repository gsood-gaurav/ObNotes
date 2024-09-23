UMAP is a nonparametric graph-based dimensionality reduction algorithm using applied Riemannian geometry and algebriac topology to find low-dimensional embeddings of structured data. The UMAP algorithm consists of two steps
- computing a graphical representation of a data set (fuzzy simplical complex)
- through stochastic gradient descent optimizing a low-dimensional embedding of the graph.

Here we extend the second step of UMAP to a parametric optimization over neural network weights, learning a parametric relationship between data and embedding.

Current nonlinear dimensionality reduction algorithms can be divided broadly into **nonparametric algorithms**, which rely on the efficient computation of probabilistic relationships from neighborhood graphs to extract structure in large data sets.
and **parametric algorithms** which driven by advances in deep learning optimize an objective function related to capturing structure in a data set over neural network weights.

## Theoretical Foundations
The theoretical foundations for UMAP are largely based on manifold theory and topological data analysis.

At high level, UMAP uses local manifold approximations and patches together local fuzzy simplical set representations to construct a topological representation of the high dimensional data. Given some low dimensional representation of data, a similar process can be used to construct an equivalent topological representation. UMAP then optimizes the layout of the data representation in the low dimensional space to minimize the cross entropy between two topological representations.

The construction of fuzzy toplogical representation can be broken down into two problems: approximating a manifold on which the data is assumed to lie; and constructing a fuzzy simplical set representation of the approximated manifold.

The data is assumed to be uniformly distributed on the manifold. Real world data is rarely so nicely behaved. However, if we assume that the manifold has Riemannian metric not inherited from the ambient space, we can find a metric such that the data is approximately uniformly distributed with regard to that metric.

**What is meant by uniform distribution on manifold $M$ is any ball of fixed volume should contain approximately same number of points of $X$ regardless of where on the manifold it is centered.

The approximate geodesic distance from $X_i$ to its neighbors by normalising distances wrt the distance to the $k^{th}$ nearest neighbor of $X_i$.

In essence by creating a custom distance for each $X_i$, we can ensure the validity of the assumption of uniform distribution on the manifold. The cost is that we now have an independent notion of distance for each and every $X_i$, and these notions may not be compatible. We have a family of discrete metric spaces (one for each $X_i$) that we wish to merge into a consistent globla structure. This can be done is natural way by converting the metric spaces into fuzzy simplical sets.

## Computational View of UMAP
UMAP ultimately can be described in terms of, costruction of, and operations on, weighted graphs. In particular this situates UMAP in the class of k-neighbor based graph learning algorithms such as Laplacian Eignemaps, Isomaps and t-SNE

As with other k-neighbor graph based algorithms, UMAP can be described in two phases. In the first phase a particular weighted k-neighbour graph is constructed. In the second phase a low dimensional layout of this graph is computed. The difference between all algorithms in this class amount to specific details in how the graph is constructed and how the layout is computed.

Assumptions in UMAP
- There exists a manifold on which data would be uniformly distributed
- The underlying manifold of interest is locally connected
- Preserving the topological structure of this manifold is the primary goal.

Any algorithm that attempts to use a mathematical structure to a k-neighbor graph to approximate a manifold must folllow a similar basic structure

- Graph Construction
	1.  Construct a weighted k-neighbor graph
	2. Apply some transform on the edges to ambient local distance
	3. Deal with the inherent asymmtery of the k-neighbour graph
- Graph Layout
	1. Define the objective function that preserves desired characterstics of this k-neighbor graph
	2. Find a low dimensional representation which optimizes this objective function

Many dimension reduction algorithms can be broken down into these steps because they are fundamental to a a particular class of solutions. Choices for each step must be either chosen through task oriented expermentation or by selecting a set of believable axioms and building strong theoretical arguments from these. Our belief is that basing our decisions on a strong foundational theory will allow for a more extensible and generalizable algorithm in the long run

We theoretically justify using the choice of using a k-neighbour graph to represent a manifold 
UMAP computes 15 nearest neighbor by default which is computationally less costly.