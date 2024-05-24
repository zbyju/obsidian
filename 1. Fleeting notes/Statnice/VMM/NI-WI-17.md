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
