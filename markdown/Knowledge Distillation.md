We want to distill the knowledge from large model to small model
Can we help the training of tiny models with large models?
A larger temperature smooths the output probability distribution.
The goal of knowledge distillation is to align the class probability distributions from teacher and student networks.

What to match?
1. Output logits
2. Intermediate weights
3. Intermediate features
4. Gradients
5. Sparsity patterns
6. Relation information