# Convulutional-Neural-Networks-1

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

# 3D Convolution

3D convolution is more of what everyday images require , since all images we process consist of Red , Green and Blue Channel (RBG) therefore
what is more used nowadays is 3D convolution, However converting them to Black and white and making them into a single channel can improve accuracy of our network but
will make it difficult for the model to detect objects based on color.

3D input matrix will be a nxnx3 matrix , therefore the filter it convulutes with will also be a sxsx3 matrix , however the output will remain as a oxo output.
Similar to 2D convolution now the filter consists of 27 values as compared to the 9 values we had in a single filter. Now in 3D convolution
the 27 values is multipled with the first top left part of the input matrix and moved on instead of the 9 values as seen earlier. 

Incase we decide to multiply the input matrix with several filters , each output would be different and then we would have final output of oxoxnc
where nc is the number of filters we convoluted with.
