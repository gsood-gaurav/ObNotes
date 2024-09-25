## Misc
- Scaling Law: Scaling up compute or architecture
- HumanEval has been widely adopted for comparing LLMs performance on Code.
- 
## Phi-1
- Different Objective how quality of data affects.
- Code Genreation Task
- 1.3B parameters
- Training for 4 days on 8 A100s
- textbook quality data from web(6B tokens) synthetically generated textbooks and exercises with GPT-3.5(1B tokens)
- attains pass@1 accuracy 50.6% on HumanEval and 55.5% on MBPP
- 8 passes over 7B token (roughly 50B tokens)
	- followed by fineturing on less than 200M tokens.
	![[Pasted image 20240301112610.png]]
- Flash Attention implementation of MultiHead Attention.
- MHA and MLP layers in parallel configuration
- Phi-1, architecture 24 layers, hidden dimension of 2048, MLP inner dimension of 8192, 32 attention heads of 64 dimension.
- The smaller 350M parameter phi 1-small model consists of 20 layers, hidden dimension of 1024, MLP-inner dimension of 4096, and 16 attention heads of dimension 64 each.
- tokenizer as codegen-350M-mono
- Aside from FlashAttention, our models do not use other techniques like Fill-In-the-Middle (FIM) [BJT+22], or Multi-Query-Attention (MQA) [RSR+20] that could further boost performance and efficiency [LAZ+23].
- For both pretraining and finetuning, we concatenate our respective datasets into a single dimensional array with “⟨∣endoftext∣⟩” token used for separating the files.
- We train our models on sequence length of 2048 sliced from our dataset array with next-token prediction loss.
- We use fp16 training with AdamW optimizer, linear-warmup-linear-decay learning rate schedule, and attention and residual dropout of 0.1.
- We train on 8 Nvidia-A100 GPUs using deepspeed.
- Our pretrained base model phi-1-base was obtained in under 4 days of training. Finetuning to obtain phi-1 used an additional 7 hours on the same hardware.
- phi-1-base was trained on the CodeTextbook dataset (filtered code-language corpus and synthetic textbooks). We use effective batch size 1024 (including data parallelism and gradient accumulation), maximum learning rate 1e-3 with warmup over 750 steps, and weight decay 0.1, for a total of 36,000 steps. We use the checkpoint at 24,000 steps as our phi-1-base – this is equivalent to ∼ 8 epochs on our CodeTextbook dataset for a total of little over 50B total training tokens. Despite the small size and computation, this model already achieves a 29% accuracy on HumanEval.
- phi-1 is obtained by finetuning phi-1-base on the CodeExercises dataset. For finetuning, we use the same setup as pretraining, but different hyperparameters: we use effective batchsize of 256, maximum learning rate 1e-4 with 50 steps of warmup, and weight decay 0.01. We train for total of 6,000 steps and pick the best checkpoint (saved every 1000 steps).
![[Pasted image 20240301114115.png]]
https://www.microsoft.com/en-us/research/blog/phi-2-the-surprising-power-of-small-language-models/