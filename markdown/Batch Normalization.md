The original authors precise definition is:

> We define internal covariate shift as the change in the distribution of network activations due to the change in network parameters during training.

After thorough it was shown that Batch Norm 

- Substantially decrease training time
- Remove necessity of drop-out
- Decrease amount of regularization needed
- Allow for increased learning rate.

Usually we apply Batch Norm to $z$ instead of $a$.