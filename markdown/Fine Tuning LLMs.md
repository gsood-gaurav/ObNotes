Base [LLMs](https://www.analyticsvidhya.com/blog/2023/03/an-introduction-to-large-language-models-llms/) do well at text generation on single-turn QA but struggle with multi-turn conversations like chat models. The base models need to be trained on transcripts of dialogues to be able to hold multi-turn conversations.

**LoRA** stands for Low-rank Adaptation, a popular fine-tuning technique in which we select a few trainable parameters instead of updating all the parameters via a low-rank approximation of original weight matrices.

QLoRA or Quantized LoRA is a step further than the LoRA. Instead of a full-precision model, it quantizes the model weights to lower floating point precision before applying LoRA. Quantization is the process of downcasting higher bit values to lower values. A 4-bit quantization process involves quantizing the 16-bit weights to 4-bit float values.

Quantizing the model leads to a substantial reduction in model size with comparable accuracy to the original model. In QLoRA, we take a quantized model and apply LoRA to it. The models can be quantized in multiple ways, such as through llama.cpp, AWQ, bitsandbytes, etc.

## Gradient Accumulation

The idea behind gradient accumulation is to instead of calculating the gradients for the whole batch at once to do it in smaller steps. The way we do that is to calculate the gradients iteratively in smaller batches by doing a forward and backward pass through the model and accumulating the gradients in the process. When enough gradients are accumulated we run the model’s optimization step. This way we can easily increase the overall batch size to numbers that would never fit into the GPU’s memory. In turn, however, the added forward and backward passes can slow down the training a bit.

## Gradient Checkpointing

Even when we set the batch size to 1 and use gradient accumulation we can still run out of memory when working with large models. In order to compute the gradients during the backward pass all activations from the forward pass are normally saved. This can create a big memory overhead. Alternatively, one could forget all activations during the forward pass and recompute them on demand during the backward pass. This would however add a significant computational overhead and slow down training.

Gradient checkpointing strikes a compromise between the two approaches and saves strategically selected activations throughout the computational graph so only a fraction of the activations need to be re-computed for the gradients. See [this great article](https://medium.com/tensorflow/fitting-larger-networks-into-memory-583e3c758ff9) explaining the ideas behind gradient checkpointing.

