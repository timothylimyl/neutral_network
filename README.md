# Building and understanding a neural network from scratch

The purpose of this project is to gain a strong foundation on Neural Networks (NN) which are the building blocks of Artificial Intelligence. By coding Neural Networks from scratch, a better understanding of the intricacies of NN will be gained. High level API such as Tensorflow and PyTorch will then be easily understood when needed to be use and further research to improve established frameworks can be made.

NN algorithms became heavily popularised for computer vision application after the 2012 ImageNet Competition where...(read paper again and cite it)

In this document, I will try my very best to run through every part of NN and also point you to the implementation in Python. I hope that by the end of it, the underlying concepts of neural networks will be made clear.

## Introduction to Neural Network (NN)

The human brain consist of billions of interconnected neurons receiving and transmitting information, providing us with the capability to deal with complex and demanding tasks. Artificial Neural Network (ANN) was developed to emulate the learning abilities of biological neurons system. The learning abilities of ANN made it an useful solution for a variety of complex problems such as facial recognition, speech recognition, image classification, machine translation which are used to be tasks that only humans can do but made possible for machine by utilising ANN. The main question for ANN is how does it learn to solve these tasks? In order to understand that, we will need to look at the overall architecture of the network and understand all of the functions used within the network.

## Neural Network Architecture

As shown in the image, the NN architecture consist of the **input, hidden and output layers**. All of these layers consist of multiple nodes which are connected to other nodes. Each nodes will consist of numeric value. Note that each layer for NN has 1D vector of nodes so any 2D and above data will be required to be flatten/reshape into the 1D space of numbers to be fed into the NN. The amount of nodes in the input layer follows the input data. Hidden layers are the layers connecting the input layer to the output layer. We have the flexibility to choose as many hidden layers as we want and vary the amount of nodes in each hidden layers as we see fit. The output layer nodes consist of values which we used to compared to the ground truth of our data for learning. This section provides you with more questions than answers about NN which is intended. Let's keep going by asking questions!

#### How are the nodes connected (what are the black lines)?

A node is connected to another node by a very simple and familiar equation (Y = MX + C). In the case of NN, the notations for the equation is **Y = Wx + b**  where  Y = Output, W= Weights, x=Input, b= Bias. Value of the node is multiplied by the weight value and then added with the bias value to produce a output value (Y) to be used for the connecting node. **Refer to code: , **

An issue with just using this equation (Y=Wx+b) is that it is only a linear equation which means that the NN unable to learn non-linear representation. To resolve this issue of needing non-linearity, we will take the node output value (Y) and put it into an **activation function** which gives us f(Y) for f is the activation function. An activation function provides non-linear mapping from input value to output.

NN is appealing in the first place because of the ability to approximate most continuous function accuractely. A feedforward NN with even a single hidden layer containing finite number of nodes and arbitrary activation function are universal approximators according to the universal approximation theorem. Read about approximation in this paper, [here](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.101.2647&rep=rep1&type=pdf).

There are many activation functions that we can look into but let's put our focus on the two popular activation functions which are Sigmoid and ReLu functions:

*insert image here

Given that our activation is f(Y), the value of the output (Y) is feed into the activation function to produces the **final value of the connecting node*

I found a very helpful visualization to aid the explanation, please head to the author's article [HERE](https://towardsdatascience.com/forward-propagation-in-neural-networks-simplified-math-and-code-version-bbcfef6f9250) for more information if needed:

**add gif**

The network of moving and computing values from one node to the next node in another layer in a forward direction only is called a **Feedforward Network**. The process of computing f(Wx+b) is known as **Forward propagation** as values are computed and propagated forward to reach the output nodes.

## Initialization of W and b values  (Before forward propagation) 

W and b values must be initialized first or else there are no values to propagate along the NN in the first run. With the appropriate intialization, the neural network can be trained quicker. If any constant initilization scheme is used, it will lead the nodes to learn the same features during training as all of the nodes will have identical influence on the loss function.Example is that if we forward propagate an input layer with 3 nodes (x1,x2,x3) and the connecting node (output) value is f(wx1,wx2,wx3) where all weights are of the same value and biases is 0. The identical influence of the parameters leads to identical gradient (see gradient descent). Thus, all nodes connecting to the next layer will evolve symmetrically throughout the training process which prevents different nodes from learning different things.

Initialising weights with values too small will lead to slow learning, taking a lot of epochs before convergence of the loss function (vanishing gradients). However, initialising the weights with values too large and it may learn to divergence, loss function is unable to converge to a local/global minimum (exploding gradients).

Read more and try it for yourself [here](https://www.deeplearning.ai/ai-notes/initialization/), this article provides a great GUI to aid understanding.

The values for the weights (W) and biases (b) of the connections can be initialized via the Xavier Initialization Method to provide with appropiate initial values for efficient training. 

Rules of thumbs to follow to prevent exploding or vanishing gradients due to initialization: a) The mean of the activations should be zero. b) The variance of the activations should stay the same across every layer.

In Xavier Initialization, every weights of the layers are picked randomly from a normal distribution with mean = 0 and variance = 1/n for n is number of nodes in the previous layer. The biases are initialized with zeros. (Refer to line )


## Loss Function (How does the NN learn?)

As previously mentioned, the values of the output nodes are compared to the ground truth data which is done through a loss function. The loss function is set up in a way to provide a goal for the network to acheive. The loss function will be optimized according to the set-up of the goal such as getting the output values close to ground truth value (minimising error). In the case of NN, a cross-entropy cost function can be used: 

Notations: y_hat = predicted output from output nodes , y = ground truth

Cost Function = - y log (y_hat)  -  (1-y) log (1-y_hat) 

Intuition:  a) If y = 1, Loss = -log(y_hat)     *Higher y_hat, produces lower value(error)*
            b) If y = 0, Loss = -log(1-y_hat) *Lower y_hat, produces lower value(error)*

To minimise the cost function, parameters of Weight (W) and Bias(b) of every connection will be changed in search for the global/local minimum of the loss function by a process known as gradient descent. In other words, the error between the output (y_hat) and ground truth (y) is minimized by tuning the parameters of W and b.


## Gradient Descent (How is the cost function minimised?)

Gradient descent is a process where the gradient of the cost function is used to provide the direction and magnitude in search of the local/global minimum. In the context of the NN architecture, the gradient of the weights and biases are computed via **backpropogation** to be used to minimise the loss function. 

*Add Formula:

*Add Code implementation:


## Backpropogation (How are the gradients computed?)

*Add Formula for those you used in your implementation and show how it is derived (later put onto latex for FYP report)


## Summary

The 5 important parts to building a neural network are:

1. Initilisation of paramaters - Initialising values of weights (W) and biases (b).
1. Forward Propagation -  Propagating the values of nodes from one layer to another by the combination of linear function and non-linear activation functions ( f(Wx+b) )
2. Loss Function  - Setting up a loss function to provide an objective to be optimized.
3. Backpropagation - Computation of equations of gradient for the loss function with respect to W and b.
4. Gradient Descent - Gradients of W and b is used in gradient descent to tune the parameters W and b to optimized the loss function.


## Extra (Great learning resources and things I find interesting)

1. Interesting example on the importance of hidden layers to approximate the functions governing the logic of XOR gate, [HERE](https://medium.com/@jayeshbahire/the-xor-problem-in-neural-networks-50006411840b). This also provides insight on why we will want to make the layer deeper sometimes to better approximate representation(continuous functions).
2. Introduction to Neural Network videos, [HERE](). These series of videos has the best visualization of the underlying concepts for NN.
3. Deep Learning Specialization by deeplearning.ai on Coursera, [HERE]().
4. FastAI Lectures Series, [HERE](https://course.fast.ai/)
5. Backpropagation:

# Let's use it!




