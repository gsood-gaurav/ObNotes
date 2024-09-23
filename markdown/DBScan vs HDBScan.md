DBScan relies on density-based notion of clusters which is designed to discover clusters of arbitrary shape.
Notion of clusters is based upon density in the database.
There are two basic types of clustering algorithms: **_Partitioning_** and **_Hierarchical_** algorithms. 

Partition Algorithms construct a partition of a database $D$ of $n$ objects into set of $k$ clusters. $k$ is an input parameter for these algorithms i.e. some domain knowledge is required that is not available for many applications.

Hierarchical Algorithms create a hierarchical decomposition of $D$. The hierarchical decomposition is represented by a _dendogram_, a tree that iteratively splits $D$ into smaller subsets until each subset consists of only one object. In such a hierarchy each node of tree represents a cluster of $D$. The dendogram can be either be created from the leaves upto the root (_agglomerative approach_) or from the roort down to leaves (_divisive_ approach) by merging or dividing clusters at each step. In contrast to partitioning algorithms, hierarchical algorithms do not need k as an input.

**cluster_selection_epsilon**: Where we require a low minimum cluster size but want to avoid an abundance of microclusters in high density regions.