# Convolutional-Neural-Networks-1

# Edge Detection 

Basic Convolution for CNN is also known as cross correlation , but the normal nomenclarture that we use is Convolution 
since actual mathematical convolution of an input with a filter , along with convolution with the filter
another filter is also convoluted to narrow the output the second filter is the horizontal and vertical inverse of the original filter

# How is convolution performed?
When we have a filter of sxs and an input of nxn , we start of by taking the sxs filter and placing in the top left corner of the input matrix
and multiplying each number in the sxs with each number that sxs is placed over, all these numbers are then added together and placed in the first element of the output
matrix. the filter is then moved from the top left to one place to the right in matrix until the complete matrix has been convoluted.

# Filters

The Three main filters that are used widely while doing CNN is the sobel filter the scharr filter
and the basic filter.

# Basic Filter - [[1,0,1],[0,0,0],[-1,0,-1]]
# Sobel Filter - [[1,2,1],[0,0,0],[-1,-2,-1]]
# Scharr Filter - [[3,10,3],[0,0,0],[-3,-10,-3]]

Vertical and Horizontal Filters

We can multiply our input matrices with horizontal and vertical filters they provide different outputs in either case. But most commonly used is the 
horizontal filters.

# 2D Convolution

Whenever we do edge detection with an input of nxn filter along with a filter sxs the output matrix
we will get is an n - s + 1 matrix output

Due to the fact that when we convolute with two matrices and the edges are most of the time diminished while convoluting
we perform an extra step of preprocessing before convolution called padding

Padding is adding an extra layer around the input matrix so that the edges around the matrix are not diminished.
To decide on the amount of padding layers needed we calculate this amount with p = (s-1)/2

When convoluting a matrix that is padded the output matrix will be equivalent with the input matrix allowing the persitinence of the edges in the matrix
Due to the fact most of the information is lost during normal convolution , by padding we are preserving it.

Padded output = n + 2p - s + 1

Another method of convolution is called strided convolution 
Strided Convolution is basically convolution but instead of moving from the first matrix element we skip by a certain number of strides
Using Strided convolution without padding leads to loss of alot of information hence padding is highly suggsted.

Strided convolution output = ( n + 2p - s)/f + 1 where f is the number of stride.

# 3D Convolution

3D convolution is more of what everyday images require , since all images we process consist of Red , Green and Blue Channel (RBG) therefore
what is more used nowadays is 3D convolution, However converting them to Black and white and making them into a single channel can improve accuracy of our network but
will make it difficult for the model to detect objects based on color.

3D input matrix will be a nxnx3 matrix , therefore the filter it convulutes with will also be a sxsx3 matrix , however the output will remain as a oxo output.
Similar to 2D convolution now the filter consists of 27 values as compared to the 9 values we had in a single filter. Now in 3D convolution
the 27 values is multipled with the first top left part of the input matrix and moved on instead of the 9 values as seen earlier. 

Incase we decide to multiply the input matrix with several filters , each output would be different and then we would have final output of oxoxnc
where nc is the number of filters we convoluted with.

# Convolutional Neural Network Layer

Each layer that we have consists of the same architecture  - we have the input layer convoluting with a certain number of filters n , which provides an output o. Each layer that we have will add a bias to the output and that is inserted as a parameter into a non linearity activation function. Filters can also be brought forward as features for your image. The final activated output is then provided as an input for the next layer so that we can perform pooling, pooling is basically convoluting with a filter nxn so that the nxn matrix can move over the output matrix and take the average or maximum value of that specific matrix . To perform pooling we specify a filter size and a stride value to get a smaller matrix. This Layer of Convolution and Pooling makes one layer of a Convnet.

# Example

In this example we can understand a bit more of how an actual convolutional neural network works
Imagine i have an input matrix of 45x45x3 where Height of the matrix is 45 and the width if 45 and the number of channels is 3
And i want to convolve it with a filter of size 3x3x3 , and i have about 10 filters - i will not do any padding i will have a stride of 1 and therefore my output matrix can be calculated with the formula ( n + 2p - s)/f + 1  where f is the stride value p is the padding value and n is the matrix input value. The output matrix will be 42x42x10 , where 10 is the number of filters i then use pooling to make a smaller matrix with the most important features preserved, to help make my detections more robust.

Now i want to convolve it again using another 20 filters and the same parameters , my output would be a 39x39x20. Notice how having more filters increases the size of the output in the z axis. I finally flatten my final output layer and provide it as an input into a fully connected layer of lesser value of nx1 size, and then output it to an softmax or activation function to learn to predict the output with a new input.

