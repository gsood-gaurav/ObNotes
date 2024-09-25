## Misc
- Empirical studies demonstrates some emergent capabilities in LLMs manifests in models with sufficiently large number of parameters, such as few shot prompting, chain of thought reasoning
- Massive Multitask Language Understanding (MMLU) (Hendrycks et al., 2021): This task is
	used to measure a model’s world knowledge and problem-solving capabilities across various
	subjects. We evaluate the models in a 5-shot setting.
- BIG-Bench Hard (BBH) (Suzgun et al., 2023): This is a subset of 23 challenging tasks from
	the BIG-Bench benchmark (Srivastava et al., 2022) designed to measure a language model’s
	abilities in complex instruction following. The models are evaluated in a 3-shot setting.
- Discrete Reasoning Over Paragraphs (DROP) (Dua et al., 2019): This reading comprehension
	task measures a model’s math reasoning abilities. We evaluate the models in a 3-shot
	setting.
- HumanEval (Zheng et al., 2023): This task is used to measure a model’s programming
	capabilities. The models are evaluated in a zero-shot setting.
- HellaSwag Common Natural Language Inference.
- OBQA open book question anwering modelled after open book exams.
-  Winogrande Common Sense Reasoning.
- ARC-c Question Answering.
- ARC-e QA
- BoolQ QA for yes no questions
- PIQA common sense reasoning
- Models with less parameters, smaller architecture, uses less training data.
## Basic Idea
- Compute-Optimal model: size of the model and training data should increase at the same rate
- Potential of training smaller models with larger datasets remain under explored.
- importance of inference budget instead of compute-optimal
- inference-optimal LMs aim for optimal performance within specific inference constraints
	- Achieved by training models with more tokens than what is recommended by scaling law
	- Smaller models when trained with more data match or even outperform larger counter parts
- Training data repeated for up to 4 epochs result in minimal performance degradation compared to using unique data.
## Tiny Llama
- Behavior of small models when trained with significantly larger tokens than what is suggested by **_scaling law_**.
- Transformer decoder only model
- ~1.1 billion parameters
- pretrained on around ~3 trillion tokens
-  ~ 3 epochs
- Building on architecture and tokenizer of Llama2
- Flash Attention
- First attempt to train a 1B model with large amount of tokens
- Surpasses OPT-1.3B and Pythia-1.4B in various downstream tasks.
### Pretraining
- Data: Mix of natural language (from slim pyjama) and source code  (star coder)
	- ratio of 7:3 between natural language and source code
- Model architecture
	![[Pasted image 20240301101426.png]]
	- Positional Embeddings: RoPE
	- RMSNorm Normalization of input before each transformer sub layer
	- SWIGLU as an activation function
	- Grouped Query Attention
- Speed Optimization
	- Fully Sharded Data Parallel (FSDP): leverage multi GPU and multi node setup. It is crucial in scaling the training process across multiple nodes which significantly improves the training speed.
	- Flash attention fused layer norm, fused cross entropy loss, fused rotary positional embeddings which plays pivotal role is boosting computational throughput.
	- SwiGLU from xFormers
	- It allows 1.1B model to fit into 40GB of GPU RAM
	- Training throughput to 24000 tokens per second per A100-40G GPU
	- Tiny Llama requires only 3456 A100 GPU hours for 300B tokens
		- in contrast to Pythia's 4830 and MPTs 7920
### Training
- Build our framework on lit-gpt
- Employs auto regressive training objective in pre training phase.
- Llaam2's AdamW optimizer ($beta1=0.9$, $beta2=0.95$)
- Cosine learning rate schedule with maximum learning rate as $4.0*10^-4$ and minimum learing rate as $4*10^-5$ 
- 2000 warmup steps to facilitate optimized learning.
- batch size as 2M tokens
- Weight decay $0.1$ 
- Gradient clipping threshold of 1.0 to regulate gradient value.
- pretrain with 16 A100-40G  GPUs
### Results
- Comparison on Decoder only and ~1B parameters.
- Evaluation on common sense reasoning  and problem solving tasks.
- Language Model Evaluation Harness Framework to evaluate models.
- Models are evaluate on Zero shot settings on below tasks.
- Common Sense Reasoning
![[Pasted image 20240301103455.png]]
- Problem Solving
![[Pasted image 20240301103633.png]]
