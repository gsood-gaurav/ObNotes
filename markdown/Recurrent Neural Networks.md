- RNNs are for processing sequential data
- To go from multilayer network to recurrent networks we need to take advantage of one of early ideas found in machine learning and statistical models of the 1980s: sharing parameters across different parts of a model. 
- Parameter sharing makes it possible to extend and apply the model to examples of different forms and generalize across them
- If we had separate parameters for each value of time index, we could not generalize to sequence lengths not seen during training, nor share statistical strenght across different sequence lengths and across different positions in time
- Such sharing is particulary important when a specific piece of information can occur at mulitiple positions with the sequence.
 
 # Parameter Sharing

Being able to efficiently process sequences of varying length is not the only advantage of parameter sharing. As you said, you can achieve that with padding. The main purpose of parameter sharing is a reduction of the parameters that the model has to learn. This is the whole purpose of using a RNN.

If you would learn a different network for each time step and feed the output of the first model to the second etc. you would end up with a regular feed-forward network. For a number of 20 time steps, you would have 20 models to learn. In Convolutional Nets, parameters are shared by the Convolutional Filters because when we can assume that there are similar interesting patterns in different regions of the picture (for example a simple edge). This drastically reduces the number of parameters we have to learn. Analogously, in sequence learning we can often assume that there are similar patterns at different time steps. Compare `'Yesterday I ate an apple'` and `'I ate an apple yesterday'`. These two sentences mean the same, but the `'I ate an apple'` part occurs on different time steps. By sharing parameters, you only have to learn what that part means once. Otherwise, you'd have to learn it for every time step, where it could occur in your model.

There is a drawback to sharing the parameters. Because our model applies the same transformation to the input at every time step, it now has to learn a transformation that makes sense for all time steps. So, it has to remember, what word came in which time step, i.e. `'chocolate milk'` should not lead to the same hidden and memory state as `'milk chocolate'`. But this drawback is small compared to using a large feed-forward network.

# Padding

As for padding the sequences: the main purpose is not directly to let the model predict sequences of varying length. Like you said, this can be done by using parameter sharing. Padding is used for efficient training - specifically to keep the computational graph during training low. Without padding, we have two options for training:

1.  We unroll the model for each training sample. So, when we have a sequence of length 7, we unroll the model to 7 time steps, feed the sequence, do back-propagation through the 7 time steps and update the parameters. This seems intuitive in theory. But in practice, this is inefficient, because TensorFlow's computational graphs don't allow recurrency, they are feedforward.
2.  The other option is to create the computational graphs before starting training. We let them share the same weights and create one computational graph for every sequence length in our training data. But when our dataset has 30 different sequence lengths this means 30 different graphs during training, so for large models, this is not feasible.

This is why we need padding. We pad all sequences to the same length and then only need to construct one computational graph before starting training. When you have both very short and very long sequence lengths (5 and 100 for example), you can use [bucketing and padding](https://www.tensorflow.org/versions/r1.0/tutorials/seq2seq#bucketing_and_padding). This means, you pad the sequences to different bucket lengths, for example [5, 20, 50, 100]. Then, you create a computational graph for each bucket. The advantage of this is, that you don't have to pad a sequence of length 5 to 100, as you would waste a lot of time on "learning" the 95 padding tokens in there.

## LSTM Layer in TensorFlow
- *recurrent_activation* is for input, forget and output gates.
- *activation* applies to hidden and output hidden state.
- 