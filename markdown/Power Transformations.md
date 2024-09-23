
# Design Goals of BoxCox Transformation
- The formulas should be simple, straightforward, well understood and easy to calculate
- They should not change the middle of the data much, but affect the tails more
- The family should be rich enough to induce large changes in the skewness of the data if  necessary: this means it should be able to contract or extend one tail of the data while extending or contracting the  other, by arbitrary amounts

Let's consider the implication of each in turn

1. Simplicity
Linear Transforms--those of the form $x \rightarrow \alpha x+\beta$ for constants $\alpha$ and $\beta$--merely change the scale and location of data;they cannot change the shape of the distribution. The next simplest formula is to consider power transformations, of the form $x \rightarrow x^\lambda$ for (nonzero) constant $\lambda$ 

2. Stability


