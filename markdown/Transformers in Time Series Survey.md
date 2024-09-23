Among multiple advantanges of Transformers, the ability to capture long-range dependencies and interactions is especially attractive for time series modelling, leading to exciting progress in various time series application.

Time Series Analysis/Modelling Tasks
1. Forecasting
2. Anomaly Detection
3. Classification

Empirically we perform the following
1. Roubustness analysis
2. model size analysis
3. seasonal-trend decomposition analysis
to check how Transformer perform in time series.

Seasonality is important frature of time series. How to effectively model long range and short range temporal dependency and capture seasonality simultaneously remains a challenge.

## Network Modifications for Time 

### Positional Encoding

As the ordering of time series matters, if of great importance to encode the positions of input time series into transformers. A common design is to first encode positional information as vectors and then inject them into the model as an additional input together with the input time series. How to obtain these vectors when modelling time series with Transformers can be divided into three main catagories.

#### Vanilla Positional Encodings

A few works simply introduce vanilla positional encoding used, which in then added to the input time series embeddings and fed to Transformer. 
**Although this approach can extract some positional information from time series, they were unable to fully exploit the important features of time serie data.**

#### Learnable Positional Encodings

As the vanilla positional encoding is hand crafted and less expressive and adaptive, several studies found that learning appropiate positional embeddings from time series data can be much more effective. Compared to fixed vanilla positional encoding, learned embeddings are more flexible and can adapt to specific tasks. One approach introduces an embedding layer in transformer that learns embedding vectors for each position index jointly with other model parameters. Another approach uses an LSTM network to encode positional embeddings which can better exploit sequential ordering information in time series.

#### Timestamp Encoding

When modelling time series in real-world scenarios, the timestamp information is commonly accessible includng calendar timestamps(e.g. second, minute, hour, week, month and year)and special timestamps (holidays and events). These timestamps are quite informative in real applications but hardly leveraged in vanilla transformers. To mitigate the issue, **Informer** propsed to encode timestamps as additional positional encoding by using learnable embedding layers. A similar timestamp encoding scheme was used in **Autoformer** and **FEDformer.**

### Attention Module

Central to Transformer is the self-attention module. It can be viewed as a fully connected layer with weights that are dynamically generated based on the pairwise similarity of input patterns. As a result, it shares the same maximum path length as fully connected layers, but with much less number of parameters, making it suitable for medlling long-term dependencies.

The self-attention module in the vanilla Transformer has a time and memory complexity of $\mathcal{O}(N^2)$  ($N$ is the input time series length), which becomes bottleneck when dealing with long sequences. Many efficient Transformers were proposed to reduce the quadratic complexity that can be classified into two main catagories
- Explicitly introducing sparsity bias into the attention mechanism like LogTrans and Pyraformer
- exploring the low-rank property of the self-attention matrix to speed up the computaion e.g. Informer and FEDformer

### Architecture-based Attention Innovation

To accomodate individual modules in Transfomers for modelling time series, a number of works seek to rennovate Transformers on the architecture level. Recent work introduce hierachical architecture into Transformer to take into account the multi-resolution aspect of time series. Informer inserts max-pooling layers with stride 2 between attention blocks which down-sample series into its half slice. Pyraformer designs a $C$-ary tree based attention mechanism in which nodes ath the finest scale correspond to the original time series, while nodes in the coarser scales represent series at lower resolutions. Pyraformer developed both inter scale and intra scale attentions in order to better capture temporal dependencies across different resolutions. Besides the ability to integrate information at different multi-resolutions a hirearchical architecture also enjoys the benefits of efficient computaion, particulary for long time series.

## Application of Time Series Transformers

### Forecasting

Module-level and Architecture-level variants are two large categories and the former consists of the majority of the up-to-date works.

#### Module-level variants

In the module-level variants for time series forecasting, their main architectures are similar to the vanilla transformer with minor changes. Researchers introduce various time series inductive biases  to design new modules. The following summarized work consists of three different types
- Designing new attention modules
- exploring innovative way to normalize time series data
- utilizing the bias for token inputs.

##### Design of new attention Modules

AST, Pyraformer, Quatformer and FEDformer all of which exploit sparsity inductive bias or low rank approximation to remove noise and achieves a low order calculation complexity.

LogTrans proposes convlutional self-attention by employing causal convolutions to generate queries and keys in the self attention layer. 
It introduces sparse bias, a Logsparse mask, in self attention model that reduces computational complexity from $\mathcal{O}(N^2$ ) to $\mathcal{O}(N log N)$. Instead of using explicit sparse bias, Informer selects dominant queries based on queries and key similarities thus acheiving similar improvements as LogTrans in computational complexity. It also designs a generative style decoder to produce long-term forecasting directly and thus avoids accumulative error in using one forward-step prediction for long-term forecasting. 

AST uses a generative adversarial encoder-decoder framework to train a sparse Transformer model for time series forecasting. It shows adversrial training can improve time series forecasting by directly shaping the output distribution of the network to avoid error accumulation through one-step ahead inference.

Pyraformer designs a hierarchical pyramidal attention module with a binary tree following the path, to capture temporal dependencies of different ranges with linear time and memory complexity. FEDformer applies attention operation in the frequency domain with Fourier transform and wavelet transform. It achieves a linear complexity by randomly selecting fixed-size subset of frequency.