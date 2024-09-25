An important paradigm in NLP consist of large scale pretraining on general domain data and adaptation to particular tasks or domains. As we pre-train larger models full fine tuning which retrains all model parameters becomes less feasible.

LORA freezes the pretrained model weights and injects trainable rank decomposition matrices into each layer of the Transformer architecture, greatly reducing the number of trainable parameters for downstream tasks.

Compared to GPT-3 175B finetuned with Adam, LoRA can reduce the number of trainable parameters by 10,000 times, GPU memory requirement by 3 times, 
LoRA performs on-par or better than finetuning in model quality on RoBERTa, DeBERTa, GPT-2, and GPT-3, despite having fewer trainable ,  training throughput and unlike adapters, no additional inference latency.

Studies show that learned over-parameterized models in fact reside on a low intrinsic dimension. We hypothesized that change in weights during model adaption also has a low "intrinsic rank" leading to our proposed LORA approach. LoRA allows us to train some dense layers in a neural network indirectly by optimizing rank decomposition matrices of the dense layer's change during adaptation instead, while keeping the pretrained weights frozen.

![[Pasted image 20240326161842.png]]

Using GPT-3 175B as an example, we show that a very low rank (i.e., r in Figure 1 can be one or
two) suffices even when the full rank (i.e., d) is as high as 12,288, making LoRA both storage- and compute-efficient.

LoRA possess several key advantages
- A pretrained model can be shared and used to build many LoRA modules for different tasks. We can freeze the shared model and efficiently switch tasks by replacing the matrices $A$ and $B$  reducing the storage requirements and task switching overhead significantly
- LoRA makes training more efficient and lowers the hardware barrier to entry by up to 3 times when using adaptive optimizers since we don't need to calculate the gradients or maintain the optimizer states for most parameters. Instead we optimize the injected much smaller low-rank matrices
- Our simpler design allows us to merge the trainable matrices with the frozen weights, when deployed introducing no inference latency, compared to fully fine tuned model by construction.
- LoRA is orthogonal to many prior methods and can be combined with many of them such as prefix tuning.
- LoRA is agnostic to training objective.
One of the main drawbacks for full fine-tuning is that each downstream task, we learn a different set of parameters $\mathbb\triangle \phi$  whose dimension $|\triangle \phi|$ equals $|\phi_0|$. Thus if pretrained model is large such as GPT-3 storing and deploying many independent instances of fine-tuned models can be challenging.
In this paper we adopt a more ***parameter efficient approach*** where task specific parameter increment $\mathbb\triangle \phi$ is encoded by smaller sized set of parameters $\Theta$ with $|\Theta|<|\Phi_0|$.
We then propose to use a low rank representation to encode $\mathbb\triangle \phi$ which is both compute and memory efficient.
When the pre-trained model is GPT-3 175B, the number of trainable
parameters $|\Theta|$ can be as small as 0:01% of $|\Theta|$.

## Adapter Layers introduce Inference Latency
![[Pasted image 20240326172520.png]]![[Pasted image 20240326172558.png]]