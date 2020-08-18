# Neural-Network-CPP
This is an example of building a super-fast neural network using C++.
---

This article explains how to create a super-fast Artificial Neural Network that can crunch millions of data points withing seconds! even milliseconds. Artificial Intelligence and Machine Learning are nowadays one of the most trending topics among computer geeks. Data scientists are being hired by tech giants for their excellence in these fields.

## Why use C++
Now, if you have already implemented a neural network model in some other programming language then you might have noticed (Especially, if we have a low-end PC ) that your models work pretty slow on even small datasets. When you began learning about Neural Networks you might have googled Which language is best for machine learning? and the obvious answer you get is Python or R is best for machine learning, other languages are hard so you must not waste your time on them!. Now, if the user starts programming, they face the problem of time and resource consumption. So, this article shows how to a super fast neural network.


## Explanation of constructor function – Initializing the neurons, cache and deltas
The topology vector describes how many neurons we have in each layer, and the size of this vector is equal to a number of layers in the neural network. Each layer in the neural network is an array of neurons, we store each of these layers as a vector such that each element in this vector stores the activation value of neuron in that layer (note that an array of these layers is the neural network itself. Now in line 8, we add an extra bias neuron to each layer except in the output layer (line 7). The cache and delta vector is of the same dimensions as that of the neuronLayer vector. We are using vectors here as layers and not a 2D matrix as we are doing SGD and not batch or mini-batch gradient descent. Now, a cache is just another name of the sum of weighted inputs from the previous layer.
A notation that we will use for dimensions of a matrix is: [m n] denotes a matrix having m rows and n columns.

### Initializing Weights matrix
Initializing weights matrix is a bit tricky! (mathematically). Pay very serious attention to whatever you read for the next few lines as this will explain how we want to use the weights matrix throught this article. I assume that you know how layers are interconnected in a neural network.

CURRENT_LAYER represents the layer which is taking input and PREV_LAYER and FWD_LAYER represents a layer back and a layer front of the CURRENT_LAYER.
c-th column in the weights matrix represents the connection of c-th neuron in CURRENT_LAYER to all the neurons in the PREV_LAYER.
r-th element of c-th column in the weights matrix represents the connection of c-th neuron in CURRENT_LAYER to r-th neuron in the PREV_LAYER.
r-th row in the weights matrix represents the connection of all the neurons in the PREV_LAYER to r-th neuron in CURRENT_LAYER.
c-th element of r-th row in the weights matrix represents connection of c-th neuron in PREV_LAYER to r-th neuron in CURRENT_LAYER.
Points 1 and 2 will be used when we use weights matrix in normal sense, but points 3 and 4 will be used when we use weights matrix in transposed sense (a(i, j)=a(j, I))

Note that we have an extra bias neuron in the previous layer. If we do a simple matrix product of neuronsLayer vector of PREV_LAYER and weights matrix of CURRENT_LAYER, we will get the new neuronsLayer vector of CURRENT_LAYER. What we have to do now is modify our weights matrix in a manner so that the bias neuron of CURRENT_LAYER remains unaffected by matrix multiplication! For that we set all the element of last column of weights matrix to 0 (line 26) except that last element (line 27).


## Explanation of feed forward algorithm:
C-th element (neuron) of the CURRENT_LAYER takes it’s input by taking a dot product between neuronLayers vector of PREV_LAYER and the C-th column. This way, it takes the inputs multiplied by weight and this also automatically adds up the bias term. The last column of weights matrix is initialized by setting all elements to 0 except the last element (set to 1), what this means is that the bias neuron of CURRENT_LAYER takes input from bias neuron of PREV_LAYER only.

