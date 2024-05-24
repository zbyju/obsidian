**Extrakce vlastností z multimédií pro potřeby vyhledávání – techniky pro obrázky, audio, video, geometrie. MPEG-7 deskriptory, lokální obrazové deskriptory (SIFT). Deskriptory z hlubokých konvolučních neuronových sítí.**

# Feature Extraction from Images
- global = property of entire image/video
- local = related to some segment

- low-level - basic features that don't have semantic information (color, texture, shape, melody)
- high-level - more complex features that have semantic information (recognized object, voice)
- domain-specific - they have semantic information but not general purpose (face, fingerprint)
## Semantic Gap
If we just look at low-level features we lose the semantics and we can't match it with high level queries
## MPEG
MPEG-4 for video in TV and internet (for representing videos)
MPEG-7 for describing videos (for representing descriptions of videos)

It specifies general visual descriptors:
- Color
	- Dominant color, Scalable color, Color layout, Color structure
- Texture
	- Homogeneous texture, texture browsing, edge histogram
- Shape
	- Region shape, Contour shape
And also application dependent:
- Face descriptor
### Color Space
= Color model (mathematical description of representing color) + mapping to physical color space (frequencies of colors)
- RGB (semantically hard)
- HSV - hue, saturation, value (easier for human to interpret)

This is done so that when measuring distance it matches our perception of similar colors.
### Color Quantization
Separating colors into clusters that represent the same color
- linear = bins of same size
- non-linear = HMMD
- lookup = enumerated colors
### Similarity
For colors its good to use quadratic form distance - Matrix with correlation between colors.
## Global Features
### Dominant Color Descriptor
N - number of dominant colors to find (number of bins)
for each dominant color i:
- $c_i$ - vector of C color components (centroid color)
- $p_i$ - percentage of pixels in the image corresponding to $c_i$
- $v_i$ - variance of the color bin (how different the colors are within that group) 
- s - high value = similar colored pixels were together
	- only one value; not depending on N

Then we put this into a vector and measure the correlation between them for similarity.
### Scalable Color Descriptor
compressed color histogram in HSV
H - 16 bit
S - 4 bit
V - 4 bit
They basically just compress the image and then use only those colors. The low bins have the most important colors, high bins have less important.
### Color Layout Descriptor
Downsize the image to 8x8 and then encode as JPEG.
Very small - just 8 bytes
### Color Structure Descriptor
M bins and window ($s\times s$ pixels).

Window goes through the whole picture and if there is at least one pixel from the bin then it increments a counter for that bin (in one pass it counts everything). It only counts presence, not number of occurrences within that window.
### Homogeneous Texture Descriptor
It assumes the image has a homogeneous texture

![[Pasted image 20240524201631.png]]

We have bins that have 6 angles and 6 granularities (the further away the more frequent the texture pattern).
We then have Gabon filters (matrices) that activate for an image or don't activate; we then increment the counter of the bin every time it a filter activates. There are many filters that represent 1 or more bins.
### Texture Browsing Descriptor
12-bit
- regularity - 4 levels of regularity
- directionality - 6 levels per direction (vertical, horizontal) angle of the texture
- coarseness - 3 levels per direction (vertical, horizontal)
### Edge Histogram Descriptor
Local edge distribution in image
1. image into 4x4 subimages
2. for each subimage we get a 5 bin histogram
	- no direction
	- vertical
	- horizontal
	- 45 degree
	- 135 degree
3. concat all histogram (= 5x16 = 80 bins)
### Face Descriptor
1. Database of faces
2. PCA => Eigenfaces
3. Query is then represented as a linear combination of eigenfaces
4. Compare vectors
## Deep Learning
### Convolution Neural Network (CNN)
- They are deep (many layers)
- At first there convolutional layers that are not fully connected (important!) which improves performance by a lot; they extract global features (edges, textures, ...)
- Then there are standard fully connected percepton layers that extract local features
- Each layer = 1 more level of abstraction for features
#### Back-propagation
- Looks for minimum of the loss function in weight space using gradient descent
- For convolution layers we need to adjust this but it still works the same
	- Convolutions layers learn the convolution filters
#### Types of layers
- data layers (input in B/W or RGB)
- vision layers
	- convolution layers, pooling layers
- activation layers
	- ReLU, Sigmoid
- common layers
	- inner product (full connected layer)
- loss layers (classification layers)
	- softmax, euclidean
### Convolution Layer
- Each depth "layer" has one set of weights (not full connected) = filter
	- => number of features the layer is able to recognize
	- Depth column: ![[Pasted image 20240524220556.png]]
	- Within the same width, height position but at different depth we have the same input but different weights
- The input is not the whole output of the previous layer but only a window
	- The neuron top left has window in the top left, neuron next to it has window moved one "pixel" next to it, ...
	- Each layer has enough neurons to go through all the possible positions with the window
	- Depth slice: ![[Pasted image 20240524220003.png]]
- Depth => number of features
- Width and height
	- Stride = size of the window
	- Stride 1 => window 1x1; 2 => window 2x2
	- Zero padding = to be able to calculate the convolution on the borders we add zeroes around
	- The input output layers are defined by stride and zero padding
- Each neuron does (perceptron):
	- $\sum_i w_i x_i + b$ and then applies some function f which either activates (gives some value) or doesn't and gives 0

![[Pasted image 20240524215246.png]]
#### Back propagation in CNN
We do convolution with the input window and the weights = forward propagation
Then we need inverse filters to do backpropagation
### Pooling layer
Downsampling
No weights
We define stride (how much downsampling) and we take some value (pooling):
- max value (most often)
- average
### Fully connected layer
activation computer as inner product
all neurons from previous to all neurons in next
### Loss layer
Determines the penalization of predicted and true labels
## Transfer learning
Using already trained deep neural networks and using them for other purposes/specific domains

The first layers extract global features
The last layers extract specific features

We can utilize the first layers and only train the last few layers
# Local Image Features
They information at some position but the position is irrelevant

These points can be:
- Random sampling
- Interest point detection
	- trying to find points that are interesting
- Segmentation
	- make segments and then divide&conquer
## Feature Clustering
Random sample of X points (1000)

This is a lot of data and not robust

Similar to bag of features (but without a global vocabulary) we cluster them (k-means).

### Set of representatives
Then we get a set that holds the position of the centroid and its properties around it (color, coarseness, ...)

Then use Quadratic form distance, hausdorff distance, earth mover's distance, ...
### Bag of features
make a big vocabulary of features (representatives)
descriptor is the histogram of features

Quadratic form, Lp distance, ...
### Hausdorff similarity
Counts how many features are similar enough in the two documents; then divides by the number of features.
## Interest points
- well defined well positioned in image
- local information is rich (spike in brightness)
- stable - it is going to stay even after changes in rotation, scale, ...
### Edge/blob detection
#### First-order derivative:
We use some predefined kernels that approximate the first order derivative after doing convolution with the image:
1. Edge detection using convolution:
	- Matrix for detecting horizontal edge $G_x = K_x * A$
	- Matrix for detecting vertical edge $G_y = K_y * A$
	- These matrices are derivative estimations
1. Gradient magnitude = $\sqrt{G_x^2 + G_y^2}$ (how powerful the edge is)
2. Gradient direction = $arctan(G_y / G_x)$ (what is the average direction of the edge)
#### Second derivative of Gaussian - DoG detector
Gaussian kernel will blur the image
1. Blur the image using two different gaussians
	- Gaussian with parameter t
	- Gaussian with parameter kt - k = blurring parameter
2. Subtract the blurred images => we get image of edges
## Interest point detection
Use DoG detector + scaling

1. Edge detection using gaussian blurring
	- Blur the image with different k parameters
	- Downscale the image and blur with the same k parameters
	- Find differences

![[Pasted image 20240525000419.png]]

2. Find extremes as candidates for interest points for each row
	- Look at all the images within on octave (row) ![[Pasted image 20240525000826.png]]
	- if the center point is an extreme point (local minimum/maximum) compared to neighbors (in this example 26 neighbors) then it is a candidate
3. Identify interest points
	- If a candidate is a candidate in all octaves (rows) then it is an interest point
## SIFT
Use interest point and then:
1. Remove low contract interest points
	- They were local extreme on the small cube of neighbors but not really
	- Remove all that are too small of extremes compared to other extremes
2. Remove points on edges
3. Find one main dominant orientation
	- Look at the neighborhood
	- Find all edges and their orientation
	- Make a histogram of 8 bins of direction of edge
	- Count how many edges are in what direction
	- Choose the one with highest occurrence = dominant orientation
4. Find the neighborhood orientations
	- Look at the neighborhood 16x16 of the interest point
	- Find all edges and their orientation
	- Make them relative to the dominant orientation
	- Make a histogram of 8 bins of direction of edge
	- Count how many edges are in what direction within subneighborhood 4x4
	- The orientation with the highest count = dominant orientation of the subneighberhood
	- We have 16 subneighborhoods within the 16x16 neighborhood => we get 16x8 (8 bins) feature descriptors
	- We scale them based on how far they are from the center
	- They are relative to the dominant orientation
		- => rotation invariant
5. Result are SIFTs; each one is 128 values (4x4x8) - relative values of number of occurrences of angles

- Local
- Invariant to rotation because angles are relative to a main one
- Invariant to scaling because we work with DoG scale detector (interest points are there for all scales)

### Bag of Features
Use them in bag of features 
1 feature = 1 SIFT

Query image then also gets sifts -> bag of features + tfidf -> sparse histogram -> querying using inverted index

Because SIFTs have lost the position information we can bring it back with reranking geometric verification

### Geometric Verification
We add another information to the bag of features - some very approximate position of the SIFT (e.g. which quadrant of the image it is in)

Each visual word is partitioned further by the position

The position is represented by a binary number (00, 01, 10, 11)

We calculate the hamming distance (XOR on binary representation); the lower the distance the better.
## High level object detection
Take the classic CNN and then get rid of the classification part and add another convolution layer (= detection layer) that has depth of how many different object we want to detect

It gives two outputs:
- X,Y of bounding boxes
- Prediction of how likely it is that certain part has some kind of object