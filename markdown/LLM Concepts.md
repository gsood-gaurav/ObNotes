- Context Length in Transformers
You are right that a transformer can take in an arbitrary **amount of tokens even with fixed parameters**, **excluding the positional embedding matrix**, whose size directly grows with the maximum allowed input length. Apart from memory requirements (O(n²)), the problem transformers have regarding input length is that they don't have any notion of token ordering. This is why positional encodings are used. They introduce ordering information into the model. This, however, implies that the model needs to learn to interpret such information (precomputed positional encodings) and also learn such information (trainable positional encodings). The consequence of this is that, during training, the model should see sequences that are as long as those at inference time because for precomputed positional encodings it may not correctly handle the unseen positional information and for learned positional encodings the model simply hasn't learned to represent them. **In summary, the restriction in the input length is driven by: Restrictions in memory: the longer the allowed input, the more memory is needed (quadratically), which doesn't play well with limited-memory devices. Need to train with sequences of the same length as the inference input due to the positional embeddings**. If we eliminate those two factors (i.e. infinite memory and infinite-length training data), you could set the size of the positional embeddings to an arbitrarily large number, hence allowing arbitrarily long input sequences. Note, however, that due to the presence of the positional embeddings, there will always be a limit in the sequence length (however large it may be) that needs to be defined in advance to determine the size of the embedding matrix.

In this paper, we argue that analyzing fine-tuning through the lens of intrinsic dimension provides us with empirical and theoretical intuitions to explain this remarkable phenomenon. We
empirically show that common pre-trained models have a very low intrinsic dimension; in other words, there exists a low dimension reparameterization that is
as effective for fine-tuning as the full parameter space. For example, by optimizing only 200 trainable parameters randomly projected back into the full space, we can tune a RoBERTa model to achieve 90% of the full parameter performance levels on MRPC.

We empirically show that common NLP tasks within the context of pre-trained representations
have an intrinsic dimension several orders of magnitudes less than the full parameterization.

We propose a new interpretation of intrinsic dimension as the downstream fine-tuning task’s
minimal description length within the framework of the pre-trained model. Within this
interpretation, we empirically show that the process of pre-training implicitly optimizes
the description length over the average of NLP tasks, without having direct access to those
same tasks.

The terms "training context" and "max_position_embeddings" are both related to the handling of input sequences in transformer-based neural network models, particularly in the context of natural language processing (NLP). However, they refer to different aspects of sequence processing:

1. **Training Context:**
    
    - The "training context" typically refers to the length of input sequences used during the training phase of the model. It represents the number of tokens or words considered as context by the model during the training process. The training context determines the size of the input sequences that the model is exposed to during training.
    - For example, if a model has a training context of 512 tokens, it means that during training, input sequences of up to 512 tokens in length are used to train the model's parameters (weights and biases).
2. **max_position_embeddings:**
    
    - The "max_position_embeddings" parameter specifies the maximum length of input sequences that the model can process during both training and inference. It represents the maximum number of tokens or words that the model's architecture and implementation can handle.
    - This parameter determines the size of the positional embedding matrix, which encodes positional information for tokens in a sequence, and limits the length of sequences that the model can effectively process.
    - For example, if a model has a max_position_embeddings value of 1024, it means that it can handle input sequences of up to 1024 tokens in length during both training and inference.

In summary, while both the training context and max_position_embeddings parameters are related to handling input sequences in transformer-based models, the training context specifically refers to the length of input sequences used during training, while max_position_embeddings defines the maximum length of input sequences that the model can handle during both training and inference.