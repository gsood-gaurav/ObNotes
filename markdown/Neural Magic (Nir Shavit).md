- Llama and MPT family
- Focused on Inference
- When someone is finetuning the model one of the things they will do is to sparsify and quantize the model
- Model is sparse and efficient on CPUs
	- Sparsity can lead to good inference on CPUs
	- CPUs already has lot of memory.
- For the 7B model
- People know how to get to 4bits per weight without loosing accuracy
- Beyond 4 bits e.g. 2 bits things get complicated and there are not good schemes there
- Neural magic uses combination of quantization and sparsification for achieving accuracy.
- Sparsification vs Scaling laws.
- In the brain there is extreme level of sparsity.
- Neural magic's approach is while you are finetuning you use our techinques and then you can use deepspeed for inference on CPUs.
- Sparsification and Quantization is very specific to architectures and datasets.
	- It is not general approach which applies to every LLM out there.
- Sparsified and Quantized models are open source (can be downloaded from sparse zoo)
	- But what is not open source is the Deep Sparse run time (perhaps how to run on CPUs)
	- https://sparsezoo.neuralmagic.com/
![[Pasted image 20240310161639.png]]

- **Pruning is the process of removing weight connections in a network to increase inference speed and decrease model memory size**. In general, neural networks are very over parameterized. Pruning a network can be thought of as removing unused parameters from the over parameterized network.
- The process of sparsification is taking a trained deep learning model and removing redundant information from the over-parameterized network resulting in a faster and smaller model. Techniques for sparsification include everything from inducing sparsity using pruning and quantization to distilling from a larger model to create a smaller version. When implemented correctly, these techniques result in significantly more performant and smaller models with limited to no effect on the baseline metrics.
- **Ultimately the power of sparsification is only realized when the deployment environment supports it**. DeepSparse is specifically engineered to utilize sparse networks for GPU-class performance on CPUs.
- Quantization is a technique to reduce the computational and memory costs of running inference by representing the weights and activations with low-precision data types like 8-bit integer (`int8`) instead of the usual 32-bit floating point (`float32`).

	Reducing the number of bits means the resulting model requires less memory storage, consumes less energy (in theory), and operations like matrix multiplication can be performed much faster with integer arithmetic. It also allows to run models on embedded devices, which sometimes only support integer data types.
- The two most common quantization cases are `float32 -> float16` and `float32 -> int8`.