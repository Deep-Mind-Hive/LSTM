# Long Short Term Memory (L.S.T.M.)


## 1. What is LSTM?
Long short-term memory (LSTM) units are units of a recurrent neural network (RNN). An RNN composed of LSTM units is often called an LSTM network. A common LSTM unit is composed of a cell, an input gate, an output gate and a forget gate. The cell remembers values over arbitrary time intervals and the three gates regulate the flow of information into and out of the cell.
LSTM networks are well-suited to classifying, processing and making predictions based on time series data, since there can be lags of unknown duration between important events in a time series. LSTMs were developed to deal with the exploding and vanishing gradient problems that can be encountered when training traditional RNNs. Relative insensitivity to gap length is an advantage of LSTM over RNNs, hidden Markov models and other sequence learning methods in numerous applications.



## 2. Need for LSTM
Recurrent Neural Networks work just fine when we are dealing with short-term dependencies. That is when applied to problems like:

<p align="center"><code>the color of the sky is _______. </code></p>

RNNs turn out to be quite effective. This is because this problem has nothing to do with the context of the statement. The RNN need not remember what was said before this, or what was its meaning, all they need to know is that in most cases the sky is blue. Thus the prediction would be:

<p align="center"><code>the color of the sky is blue. </code></p>

However, vanilla RNNs fail to understand the context behind an input. Something that was said long before, cannot be recalled when making predictions in the present. Let’s understand this as an example:

<p align="center"><code>I spent 20 long years working for the unnder-privileged kids in spain. I then moved to Africa. 
  ......
  I can speak fluent _______.</code></p>

Here, we can understand that since the author has worked in Spain for 20 years, it is very likely that he may possess a good command over Spanish. But, to make a proper prediction, the RNN needs to remember this context. The relevant information may be separated from the point where it is needed, by a huge load of irrelevant data. This is where a Recurrent Neural Network fails!

The reason behind this is the problem of [Vanishing Gradient](https://medium.com/@anishsingh20/the-vanishing-gradient-problem-48ae7f501257) We know that for a conventional feed-forward neural network, the weight updating that is applied on a particular layer is a multiple of the learning rate, the error term from the previous layer and the input to that layer. Thus, the error term for a particular layer is somewhere a product of all previous layer's errors. When dealing with activation functions like the sigmoid function, the small values of its derivatives (occurring in the error function) gets multiplied multiple times as we move towards the starting layers. As a result of this, the gradient almost vanishes as we move towards the starting layers, and it becomes difficult to train these layers.

A similar case is observed in Recurrent Neural Networks. RNN remembers things for just small durations of time, i.e. if we need the information after a small time it may be reproducible, but once a lot of words are fed in, this information gets lost somewhere. This issue can be resolved by applying a slightly tweaked version of RNNs – the Long Short-Term Memory Networks.



## 3. Architecture of LSTMs

<p align="center"><img width=500 alt="lstm arch" src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2017/12/10131302/13.png"></p>

The symbols used here have following meaning:

  1. X : Scaling of information

  2. (+) : Adding information

  3. σ : Sigmoid layer

  4. tanh: tanh layer

  5. h(t-1) : Output of last LSTM unit

  6. c(t-1) : Memory from last LSTM unit

  7. X(t) : Current input

  8. c(t) : New updated memory

  9. h(t) : Current output



## 4. Area of application
 1. Speech recognition
 2. Video synthesis
 3. Natural language processing
 4. Language modeling
 5. [Machine Translation also known as sequence to sequence learning](https://arxiv.org/pdf/1409.3215.pdf)
 6. [Image captioning ](https://arxiv.org/pdf/1411.4555v2.pdf)
 7. [Hand writing generation](https://arxiv.org/pdf/1502.04623v2.pdf)
 8. [Image generation using attention models](https://arxiv.org/pdf/1502.04623v2.pdf)
 9. [Question answering](http://www.aclweb.org/anthology/P15-2116)
10. [Video to text](https://arxiv.org/pdf/1505.00487v3.pdf)



  * A quick tutorial on [LSTM](https://www.youtube.com/watch?v=9zhrxE5PQgY) 

## 5. Simple Example
A simple example for lstm is [lstm.py](https://github.com/Deep-Mind-Hive/LSTM/blob/master/lstm.py)
We are using keras framework to demonstrate how to build LSTM sequential network

1. First we have to import all the dependencies 
    
    from keras.models import Sequential \n
    from keras.layers import LSTM, Dense \n
    import numpy as np
    
2. define your data dimension, timesteps, number of classes and batch size

        data_dim = 16
        timesteps = 8
        num_classes = 10
        batch_size = 32

3. Building model
  1. create the instance of the sequential model
  2. on that instance add a LSTM layer with 
