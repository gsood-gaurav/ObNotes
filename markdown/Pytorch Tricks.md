## Tensors
- There are two ways to construct a tensor in pytorch
	- `torch.Tensor`
	- `torch.tensor`
- `torch.tensor` infers datatype automatically while `torch.Tensor` always construct tensors with float32. It is always advisable to use `torch.tensor`
# `torch.no_grad()` and `model.eval()`
- `model.eval()` will notify all your layers that you are in eval mode, that way batchnorm or dropout layers will work in eval mode instead of training mode
- `torch.no_grad()` impacts the autograd engine and deactivates it. It will reduce memory usage and speed up computations but you won't be able to backprop
## Optimizer State
You should save the optimizer state **if you want to resume model training** later. Especially if Adam is your optimizer. Adam is an adaptive learning rate method, which means it computes individual learning rates for various parameters.

**It is not required if you only want to use the saved model for inference.**

PyTorch uses `float32` by default for the **parameter storage and all calculations.**  
If you are using mixed-precision training via `torch.cuda.amp` then some operations will be performed with `float16` inputs/outputs, but the computation will still be performed in `float32`.

For 32-bit states, Momentum and Adam consume 4 and 8 bytes per parameter. That is 4 GB and 8
GB for a 1B parameter model. Our 8-bit non-linear quantization reduces these costs to 1 GB and 2
GB.

- Speed:
    
    32-bit floating point operations are faster than 64-bit floating point operations on most hardware. This is because 32-bit numbers can be represented in fewer bits, which means that they can be processed more quickly.

- Accuracy:
    
    32-bit floating point numbers have a wide enough range to represent most real-world values with sufficient accuracy. This means that using 32-bit precision does not typically lead to a significant loss of accuracy in deep learning models.

- Compatibility:
    
    32-bit floating point is the most widely supported floating point format on hardware. This means that PyTorch models that are trained using 32-bit precision can be deployed on a wide range of devices, including CPUs, GPUs, and mobile devices.

The multiplication of two vectors is a memory-bandwidth-bound operation. The use of fp32 vectors requires less bandwidth than the use of fp64 vectors of identical length, therefore the use of fp32 vectors instead of fp64 vectors would generally be beneficial for performance.

However there are some cases where it may be beneficial to use a different precision such as 16-bit or 64-bit. For example, if you are training a model on a very large dataset, you may want to use 16-bit precision to reduce the memory usage. Or if you need  very high accuracy, you may want to use 64-bit precision. Overall 32-bit floating point precision is a good choice for most deep learning applications. It provides a balance between speed, accuracy and compatibility.

The multiplication of two vectors is a memory-bandwidth-bound operation. The use of fp32 vectors requires less bandwidth than the use of fp64 vectors of identical length, therefore the use of fp32 vectors instead of fp64 vectors would generally be beneficial for performance.

The multiplication of two vectors is a memory-bandwidth-bound operation. The use of fp32 vectors requires less bandwidth than the use of fp64 vectors of identical length, therefore the use of fp32 vectors instead of fp64 vectors would generally be beneficial for performance.

Float32 (FP32) stands for the standardized IEEE 32-bit floating point representation. With this data type it is possible to represent a wide range of floating numbers. In FP32, 8 bits are reserved for the "exponent", 23 bits for the "mantissa" and 1 bit for the sign of the number. In addition to that, most of the hardware supports FP32 operations and instructions.

In the float16 (FP16) data type, 5 bits are reserved for the exponent and 10 bits are reserved for the mantissa. This makes the representable range of FP16 numbers much lower than FP32. This exposes FP16 numbers to the risk of overflowing (trying to represent a number that is very large) and underflowing (representing a number that is very small).

For example, if you do `10k * 10k` you end up with `100M` which is not possible to represent in FP16, as the largest number possible is `64k`. And thus you'd end up with `NaN` (Not a Number) result and if you have sequential computation like in neural networks, all the prior work is destroyed. Usually, loss scaling is used to overcome this issue, but it doesn't always work well.

A new format, bfloat16 (BF16), was created to avoid these constraints. In BF16, 8 bits are reserved for the exponent (which is the same as in FP32) and 7 bits are reserved for the fraction.

This means that in BF16 we can retain the same dynamic range as FP32. But we lose 3 bits of precision with respect to FP16. Now there is absolutely no problem with huge numbers, but the precision is worse than FP16 here.

In the Ampere architecture, NVIDIA also introduced [TensorFloat-32](https://blogs.nvidia.com/blog/2020/05/14/tensorfloat-32-precision-format/) (TF32) precision format, combining the dynamic range of BF16 and precision of FP16 to only use 19 bits. It's currently only used internally during certain operations.

In the machine learning jargon FP32 is called full precision (4 bytes), while BF16 and FP16 are referred to as half-precision (2 bytes). On top of that, the int8 (INT8) data type consists of an 8-bit representation that can store 2^8 different values (between [0, 255] or [-128, 127] for signed integers).

While, ideally the training and inference should be done in FP32, it is two times slower than FP16/BF16 and therefore a mixed precision approach is used where the weights are held in FP32 as a precise "main weights" reference, while computation in a forward and backward pass are done for FP16/BF16 to enhance training speed. The FP16/BF16 gradients are then used to update the FP32 main weights.

During training, the main weights are always stored in FP32, but in practice, the half-precision weights often provide similar quality during inference as their FP32 counterpart -- a precise reference of the model is only needed when it receives multiple gradient updates. This means we can use the half-precision weights and use half the GPUs to accomplish the same outcome.

**To calculate the model size in bytes, one multiplies the number of parameters by the size of the chosen precision in bytes. For example, if we use the bfloat16 version of the BLOOM-176B model, we have `176*10**9 x 2 bytes = 352GB`! As discussed earlier, this is quite a challenge to fit into a few GPUs.**

bitsandbytes can be run on 8-bit tensor core-supported hardware, which are Turing and Ampere GPUs (RTX 20s, RTX 30s, A40-A100, T4+). For example, Google Colab GPUs are usually NVIDIA T4 GPUs, and their latest generation of GPUs does support 8-bit tensor cores. Our demos are based on Google Colab so check them out below!

To determine how this `dispatch` can be performed, generally specifying `device_map="auto"` will be good enough as 🤗 Accelerate will attempt to fill all the space in your GPU(s), then loading them to the CPU, and finally if there is not enough RAM it will be loaded to the disk (the absolute slowest option).

load_in_4bit=True, This flag is used to enable 4-bit quantization by replacing the Linear layers with FP4/NF4 layers from `bitsandbytes`.