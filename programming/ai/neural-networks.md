
# Neural Networks

## What is a neural network?

* Think of each neuron as a function. It takes the outputs of all the neurons in the previous layer, and spits out a number between 0 and 1.
* The entire network is also just a function. It takes in N (e.g 784) numbers as an input and spits out 10 numbers.
* Imagine a 28x28 pixels picture of a handwritten digit.
* The network starts with 28x28=784 neurons. Each one of these takes a number that represents the grayscale value of the corresponding pixel, ranging from 0 for black pixels, up to 1 for white pixels. This number is called activation.
* The last year has 10 neurons; each representing one of the digits. The activation in these neurons -some number between 0 and 1- represents how much the system thinks that the given image corresponds with a given image.

![](./images/neural-network-01.png)

* Activations on one layer, determines the activations on the next layer. If you feed an image lighting up all 784 neurons of the input layer according to the brightness of the each pixel; that pattern of the activations causes some very specific pattern in the next layer, which causes some pattern in the one after it, which finally gives some pattern in the output layer; the brightest neuron in the output layer is the choice of the network.
* How exactly activations in one layer might determine the activations in the next? The goal is to have some mechanism that can conceiveably combine pixels into edges, or edges into patterns, or patterns into digits.
* Let's say the hope is one particular neuron in the second layer to pick up on whether or not the image has an edge in a region of the image.
* What parameters should exist to capture a pattern ? We'll assign a weight to each connection between our neuron and the neurons from the first layer;

![](./images/neural-network-02.png)

* Next; take all the activations from the first layers and compute their weighted sum.
* If we made all of the weights associated with almost all of the pixels zero, except for some positive weights in this region we care about, then taking the weighted sum of all the pixel values amounts to adding up to the values of the pixels in the region we care about.
* If we wanted  to pick up on whether there is an edge here, have some negative weights associated with the surrounding pixels, then the some is largest when those middle pixels are bright, but the surrounding pixels are darker.

![](./images/neural-network-03.png)

* We want activations to be a number between 0 and 1; a common thing to do is pump this weighted sum into sigmoid function that squashes the real number into a range between 0 and 1. Very negative inputs will be close to zero, very high numbers will be close to 1.

![](./images/neural-network-04.png)

* We need neurons to light up only when they have a meaningfully high number, not just when they're higher than zero. We'll add bias -another number e.g (-10)- to set how high the weighted sum needs to be, before the neuron starts getting meaningfully active, before passing the sum to sigmoid function.

![](./images/neural-network-05.png)
