Instead of compressing the entire input sequence into a fixed context vector, attention mechanism proposes a dynamic representation of the input sequence at each decoding step. A weighted sum of the representations on the input at each time step.
The process of assigning weights should be differentiable.

 Consider the following
$$D ={(k_1,v_1),...(k_m,v_m)}$$
a database of m tuples of keys and values. Moreover, denote by $q$ a query. Then we can define the attention over $D$ as 
$$Attention(q,D)=\sum_{i=1}^m\alpha(q,k_i)v_i$$
where $\alpha(q,k_i)\in R(i=1,...,m)$ are scalar attention weights. The operation itself is referred to as attention pooling. The name attention derives from the fact that the operation pays particular attention to the terms for which $\alpha$ is significant(large). 

