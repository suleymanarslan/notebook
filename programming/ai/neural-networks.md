
# Neural Networks

## What is a neural network?

* Think of each neuron as a function. It takes the outputs of all the neurons in the previous layer, and spits out a number between 0 and 1.
* The entire network is also just a function. It takes in N (e.g 784) numbers as an input and spits out 10 numbers.
* Imagine a 28x28 pixels picture of a handwritten digit.
* The network starts with 28x28=784 neurons. Each one of these takes a number that represents the grayscale value of the corresponding pixel, ranging from 0 for black pixels, up to 1 for white pixels. This number is called activation.
* The last year has 10 neurons; each representing one of the digits. The activation in these neurons -some number between 0 and 1- represents how much the system thinks that the given image corresponds with a given image.
* Activations on one layer, determines the activations on the next layer. If you feed an image lighting up all 784 neurons of the input layer according to the brightness of the each pixel; that pattern of the activations causes some very specific pattern in the next layer, which causes some pattern in the one after it, which finally gives some pattern in the output layer; the brightest neuron in the output layer is the choice of the network.

![](./images/neural-network-01.png)
