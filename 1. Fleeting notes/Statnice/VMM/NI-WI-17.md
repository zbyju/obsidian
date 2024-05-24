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