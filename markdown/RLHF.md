LLMs are able to generate diverse and compelling text from human input prompts. However what makes a good text is inherently hard to define as it is subjective and context dependent.

Writing a loss function to capture these attributes seems intractable and most language models are still trained with simple next token prediction loss (cross entropy). To over come shortcomings of the loss itself people define metrics that are designed to better capture human preferences such as _BLEU_ and ROUGE. While being better suited than the loss function itself at measuring performance these metrics simply compare generated text to references with simple rules and thus are also limited. Wouldn't it be great if we use human feedback for generated text as a measure of performance or go even further and use that feedback as a loss to optimize the model? That is the idea of RL from Human feedback(RLHF); use methods from reinforcement learning to directly optimize a language model with human feedback.

## RLHF; step by step

The RLHF process can be broken down into three core steps:

> [!note] Steps
> - Pretraining a language model (LM)
> - gathering data and training a reward model
> - fine-tuning the LM with reinforcement learning.

## Reward Model Training

The idea is to generate a reward model calibrated with human preferences. The underlying goal is to get a model or system that takes in a sequence of text, and returns a scalar reward which should numerically represent the human preference.
The system can be end to end LM or a modular system outputting a reward. e.g. a model ranks outputs, and ranking is converted to a reward.