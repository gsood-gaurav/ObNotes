>[!note] Kevin Murphy Book

CART or decision trees are defined by recursively partitioning the input space, defining local model in each resulting region of input space. The overall model can be represented by tree, with one leaf per region.

By using enough splits(i.e. deep enough trees) we can make piece wise linear approximation to decision boundaries with more complex shapes, but it may require a lot of data to fit such a model.

Formally a regression tree may be defined as follows

$$
f(x;\theta) = \sum_{j=1}^Jw_j\mathbb{I}(x\in R_j)
$$
where $R_j$ is the region specified by the $j^{th}$ leaf node.

$$
w_j = \frac{\sum_{n=1}^Ny_n\mathbb{I}(x_n\in R_j)}{\sum_{n=1}^N\mathbb{I}(x_n \in R_j)}
$$
which is simply mean of the number of data points falling in $R_j$
 
 and 
 $\theta = \{(R_j,w_j):j = 1:J\}$ where $J$ is number of nodes.

To fit the model we need to minimize the following loss
$$
\mathcal{L} = \sum_{n=1}^N\mathcal{l}(y_n, f(x_n;\theta)) = \sum_{j=1}^J\sum_{x_n\in R_j} \mathcal{l}(y_n,w_j)
$$
Unfortunately this is not differentiable because of the need to learn the discrete tree structure.

## Limitations

- **Brittleness** Decision Trees are susceptible to changes in training data, which can lead to learning significantly different tress for similar datasets. In other words they are high variance estimators. This inherent  brittleness is addressed by using ensemble method such as random forests or gradient boosting trees which combine multiple trees to improve robustness and predictive performance. Ensemble methods reduce variance.
- **Computational Complexity** Finding the **optimal feature and threshold at each split** is an NP-complete problem which is computationally exhaustive. To mitigate this, heuristics are typically employed in embedded algorithms. Random Forests select this by randomly selecting subset of features (at each node) and samples to determine thresholds within each tree reducing computational demand
- **Overfitting** Decision Trees have a tendency to overfit to the training data, Stratgies like tree pruning (limiting maximum depth of trees, setting minimum samples per leaf) are commonly used to prevent overfitting which helps trees to generalize.
- Due to greedy nature of tree construction process they are not very accurate compared to other models.
- They have limitations of extrapolation for points seen outside the training data.

## Missing Features

- **Surrogate Splits** If a feature is missing, find other feature which will lead to similar split. This method can find highly correlated features.
- Categorical variable: just assign **missing** and treat data as fully observable.

## Pros and Cons

- They are easy to interpret
- Can handle both mixed discrete and continuous inputs
- They are insensitive to monotone transformations of the inputs (because split point are based on ranking the data points ), so there is no need to standardize the data.
- They perform automatic variable selection
- They are fast to fit and scale well to large datasets
- They can handle missing input features

## Ensemble Learning

- It has similar bias to the base models but lower variance.; a simple way to reduce variance
- In case of regression average or majority vote in case of classification
- Instead of taking Stacking learn how to combine output of various models on a separate dataset. $f(y|x) = \sum_jw_jf_m(y|x)$ where $w_j$ are learnt.
## Bagging

- Bagging fit M different base models to different randomly sampled version of dataset.

## Random Forest

- Tries to decorrelate the base learners even further by randomly choosing subset of input variables at each node of the tree as well as randomly chosen subset of the data cases.

## Gradient Boosting
 
- Sequentially building weak learners where each learner tries to improve upon the misslabelled examples by the previous learner by fitting on the residuals
- **learners are selected using gradient descent in function space.**
- 
 

>[!note] Other Source


- Cart models tree structure is good for capturing interactions.
- One line of thought is since tree based models works very well on tabular data, we strive to understand which [[Inductive Bias in Machine Learning|inductive biases]] make them well suited for these data
- 