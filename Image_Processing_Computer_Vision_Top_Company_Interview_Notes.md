# Image Processing & Computer Vision — Data Science / ML / AI Engineer Notes

## 0. Learning Path

Follow this order:

1. Image fundamentals
2. Image representation and color spaces
3. Image I/O and visualization
4. Basic image operations
5. Image preprocessing
6. Histograms and thresholding
7. Edge detection
8. Morphological operations
9. Geometric transformations
10. Image filtering and convolution
11. Feature detection and description
12. Segmentation
13. Object detection
14. Object tracking
15. Feature extraction with CNNs
16. Transfer learning
17. Modern computer vision
18. OpenCV + Python workflow
19. Evaluation metrics
20. Deployment and production considerations
21. Interview questions
22. Practical project workflow

---

# 1. What Is Image Processing?

Image processing is the process of manipulating an image to improve it, extract useful information, or prepare it for further analysis.

Typical goals:

- Remove noise
- Improve contrast
- Resize or rotate images
- Detect edges
- Segment regions
- Extract features
- Prepare images for machine learning

### Example

An image captured from a camera may contain:

- Noise
- Poor lighting
- Blur
- Unwanted background
- Different image sizes

Image processing can clean and transform the image before a machine-learning model receives it.

### Simple pipeline

```text
Raw Image
   ↓
Resize
   ↓
Noise Reduction
   ↓
Contrast Enhancement
   ↓
Normalization
   ↓
Feature Extraction / Model
```

---

# 2. What Is Computer Vision?

Computer Vision (CV) is a broader field in which machines are trained to understand and interpret visual information from images and videos.

Image processing focuses heavily on manipulating images.

Computer vision focuses on understanding what the image contains.

### Example

Image processing:

> "Remove noise from this image."

Computer vision:

> "Detect the person and identify their activity."

### Relationship

```text
Image Processing
       ↓
Preprocessing
       ↓
Feature Extraction
       ↓
Computer Vision Model
       ↓
Prediction / Understanding
```

Image processing is therefore often one component of a computer-vision system.

---

# 3. Image vs Computer Vision vs Deep Learning

| Concept | Main Purpose |
|---|---|
| Image Processing | Manipulate and improve images |
| Computer Vision | Understand visual content |
| Machine Learning | Learn patterns from data |
| Deep Learning | Learn complex representations automatically |
| CNN | Neural network architecture commonly used for vision |
| Object Detection | Locate and classify objects |
| Image Classification | Assign a class to an image |
| Segmentation | Assign labels to pixels/regions |

---

# 4. How an Image Is Represented

A digital image is represented as a grid of pixels.

A grayscale image can be represented as a 2D matrix.

Example:

```text
[
 [  0,  50, 100],
 [100, 150, 200],
 [200, 220, 255]
]
```

Usually:

- `0` = black
- `255` = white

For an 8-bit grayscale image:

```text
Pixel range = 0 to 255
```

A color image generally contains multiple channels.

For RGB:

```text
Red
Green
Blue
```

An RGB image can therefore be represented as:

```text
Height × Width × 3
```

Example:

```text
224 × 224 × 3
```

---

# 5. Pixels

A pixel is the smallest addressable element of a digital image.

Each pixel contains intensity or color information.

For RGB:

```text
Pixel = [R, G, B]
```

Example:

```text
[255, 0, 0] → Red
[0, 255, 0] → Green
[0, 0, 255] → Blue
```

---

# 6. Image Dimensions

An image commonly has:

```text
Height × Width × Channels
```

Example:

```text
1080 × 1920 × 3
```

means:

- Height = 1080 pixels
- Width = 1920 pixels
- Channels = 3

### Important interview point

For a grayscale image:

```text
Height × Width
```

For a color image:

```text
Height × Width × Channels
```

---

# 7. Bit Depth

Bit depth determines how many intensity values can be represented.

For `n` bits:

```text
Number of possible values = 2^n
```

Examples:

```text
8-bit  → 256 values
16-bit → 65,536 values
```

Most standard images used in basic computer vision are commonly represented with 8-bit pixel values.

---

# 8. Resolution

Resolution refers to the number of pixels used to represent an image.

Example:

```text
1920 × 1080
```

Total pixels:

```text
1920 × 1080 = 2,073,600
```

Higher resolution generally provides more visual detail but increases:

- Memory usage
- Processing time
- Storage requirements

---

# 9. Channels and Color Spaces

A color space defines how colors are represented.

Important color spaces:

- RGB
- BGR
- HSV
- Grayscale
- LAB
- YCrCb

---

# 10. RGB

RGB stands for:

```text
Red
Green
Blue
```

Each channel normally contains values from:

```text
0 to 255
```

Example:

```text
[255, 0, 0] → Red
```

RGB is common in image representation and many deep-learning frameworks.

---

# 11. BGR

OpenCV commonly uses BGR channel ordering instead of RGB.

```text
B → Blue
G → Green
R → Red
```

This is a very common interview question.

### Important

```python
import cv2

image = cv2.imread("image.jpg")
```

OpenCV loads the image in:

```text
BGR
```

If displaying with a library expecting RGB, conversion may be required.

---

# 12. Grayscale

A grayscale image contains one intensity channel instead of three color channels.

Typical representation:

```text
0   → black
255 → white
```

Advantages:

- Lower memory usage
- Faster processing
- Simpler representation
- Useful when color is not important

Example:

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

# 13. HSV

HSV means:

```text
H → Hue
S → Saturation
V → Value
```

HSV is often useful for color-based segmentation because color information is separated from brightness.

Example use cases:

- Detecting colored objects
- Traffic-sign analysis
- Color segmentation
- Industrial inspection

```python
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
```

---

# 14. Image Acquisition

Images can originate from:

- Cameras
- Mobile devices
- Satellites
- Medical imaging systems
- CCTV
- Web datasets
- Sensors
- Video streams

A production CV system should consider:

- Camera quality
- Lighting
- Frame rate
- Resolution
- Lens distortion
- Camera position

---

# 15. Loading an Image with OpenCV

```python
import cv2

image = cv2.imread("image.jpg")

print(image.shape)
```

Common output:

```text
(height, width, channels)
```

Display:

```python
cv2.imshow("Image", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

In notebooks, Matplotlib is often more convenient:

```python
import matplotlib.pyplot as plt

plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```

---

# 16. Saving an Image

```python
cv2.imwrite("output.jpg", image)
```

Always verify that:

- The output path is correct.
- The image is not empty.
- The required format is supported.

---

# 17. Resizing

Images often need to be converted to a common size before ML inference.

```python
resized = cv2.resize(image, (224, 224))
```

### Why resize?

Neural networks often expect fixed input dimensions.

Example:

```text
Raw image → 1920×1080
          ↓
Resize
          ↓
224×224
          ↓
CNN
```

---

# 18. Interpolation

When resizing, the algorithm estimates new pixel values.

Common interpolation methods:

### Nearest Neighbor

Uses the nearest pixel.

Advantages:

- Fast
- Simple

Disadvantage:

- Can produce blocky results

### Bilinear

Uses neighboring pixels.

Generally smoother than nearest-neighbor.

### Bicubic

Uses a larger neighborhood and can produce smoother results.

### Area

Often useful for downsampling.

Example:

```python
resized = cv2.resize(
    image,
    (224, 224),
    interpolation=cv2.INTER_AREA
)
```

---

# 19. Image Cropping

Cropping selects a region of interest (ROI).

```python
crop = image[100:400, 200:500]
```

Conceptually:

```text
image[y1:y2, x1:x2]
```

Important:

```text
Rows → y
Columns → x
```

---

# 20. Region of Interest (ROI)

ROI means the portion of an image relevant to the task.

Example:

```text
Full image
 ├── Background
 ├── Person
 └── Object
```

If only the object matters, process that region rather than the entire image.

Benefits:

- Lower computation
- Less noise
- Faster processing
- More focused features

---

# 21. Image Normalization

Normalization scales pixel values into a desired range.

Common example:

```python
image = image / 255.0
```

Then:

```text
0   → 0.0
255 → 1.0
```

Benefits:

- Better numerical stability
- More suitable neural-network inputs
- Can improve optimization

---

# 22. Standardization

Standardization transforms values using:

```text
z = (x - mean) / standard_deviation
```

Unlike simple min-max normalization, standardization centers the values around zero.

For computer vision, the exact preprocessing depends on the model.

---

# 23. Data Augmentation

Data augmentation creates modified versions of training images.

Common transformations:

- Rotation
- Horizontal flip
- Vertical flip
- Crop
- Translation
- Scaling
- Brightness changes
- Contrast changes
- Noise injection

Example:

```text
Original
   ↓
 ┌───────────────┐
 │   Image       │
 └───────────────┘
   ↓
 ┌───────┬───────┬───────┐
 │ Flip  │Rotate │ Crop  │
 └───────┴───────┴───────┘
```

### Why augmentation?

It helps the model generalize to variations not seen exactly in training.

### Important

Augmentation should usually be applied to training data, not blindly to validation/test data.

---

# 24. Noise in Images

Noise is unwanted variation in pixel values.

Common types:

- Gaussian noise
- Salt-and-pepper noise
- Speckle noise
- Sensor noise

Noise can reduce model performance and make edge/feature detection harder.

---

# 25. Image Filtering

Filtering modifies pixel values using neighboring pixels.

Applications:

- Noise reduction
- Smoothing
- Sharpening
- Edge detection

Common filters:

- Mean filter
- Gaussian filter
- Median filter
- Bilateral filter

---

# 26. Mean Filter

The mean filter replaces a pixel with the average of neighboring pixels.

Conceptually:

```text
1 2 3
4 5 6
7 8 9
```

Average:

```text
(1+2+3+4+5+6+7+8+9) / 9
```

It smooths the image but can blur edges.

---

# 27. Gaussian Blur

Gaussian filtering applies a weighted average based on a Gaussian distribution.

```python
blur = cv2.GaussianBlur(image, (5, 5), 0)
```

Applications:

- Noise reduction
- Preprocessing before edge detection
- Smoothing

Gaussian blur is frequently used before Canny edge detection.

---

# 28. Median Filter

Median filtering replaces a pixel with the median of its neighborhood.

It is particularly effective against salt-and-pepper noise.

```python
filtered = cv2.medianBlur(image, 5)
```

### Mean vs Median

| Filter | Typical Use |
|---|---|
| Mean | General smoothing |
| Gaussian | Smooth noise while preserving structure reasonably well |
| Median | Salt-and-pepper noise |

---

# 29. Bilateral Filter

Bilateral filtering smooths an image while attempting to preserve edges.

```python
filtered = cv2.bilateralFilter(image, 9, 75, 75)
```

It considers:

- Spatial distance
- Intensity/color difference

---

# 30. Convolution

Convolution is fundamental to image processing and CNNs.

A small matrix called a kernel/filter slides over an image.

Example:

```text
Image:

[1 2 3
 4 5 6
 7 8 9]

Kernel:

[1 0
 0 -1]
```

The kernel interacts with local image regions to produce a feature response.

Conceptually:

```text
Image
  ↓
Kernel slides
  ↓
Multiplication + Summation
  ↓
Feature Map
```

---

# 31. Kernel / Filter

A kernel is a small matrix used to detect a particular pattern.

Examples:

- Horizontal edges
- Vertical edges
- Sharpening
- Blurring

Example horizontal edge kernel:

```text
[-1 -1 -1
  0  0  0
  1  1  1]
```

The output indicates where corresponding patterns are present.

---

# 32. Image Histogram

An image histogram shows the distribution of pixel intensities.

For grayscale images:

```text
X-axis → intensity
Y-axis → frequency
```

A histogram helps understand:

- Brightness
- Contrast
- Distribution
- Saturation of intensities

Python:

```python
hist = cv2.calcHist(
    [gray],
    [0],
    None,
    [256],
    [0, 256]
)
```

---

# 33. Contrast

Contrast describes the difference between light and dark regions.

Low contrast:

```text
Most pixels have similar intensities.
```

High contrast:

```text
Pixel intensities are more widely distributed.
```

Contrast enhancement can make features easier to detect.

---

# 34. Histogram Equalization

Histogram equalization attempts to improve contrast by redistributing intensity values.

```python
equalized = cv2.equalizeHist(gray)
```

Useful for some low-contrast grayscale images.

---

# 35. CLAHE

CLAHE means:

```text
Contrast Limited Adaptive Histogram Equalization
```

It performs local contrast enhancement while limiting excessive amplification.

```python
clahe = cv2.createCLAHE(
    clipLimit=2.0,
    tileGridSize=(8, 8)
)

enhanced = clahe.apply(gray)
```

Useful when different image regions have different lighting.

---

# 36. Thresholding

Thresholding converts an image into regions based on intensity.

Basic idea:

```text
if pixel > threshold:
    white
else:
    black
```

Example:

```python
_, binary = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)
```

---

# 37. Binary Thresholding

Produces two values:

```text
0
255
```

Useful for:

- Document processing
- Object separation
- Simple segmentation
- Shape extraction

---

# 38. Adaptive Thresholding

A single threshold may not work when illumination varies.

Adaptive thresholding calculates thresholds locally.

```python
adaptive = cv2.adaptiveThreshold(
    gray,
    255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)
```

Useful for:

- Documents
- Uneven lighting
- Text extraction

---

# 39. Otsu Thresholding

Otsu's method automatically chooses a threshold based on the image histogram.

```python
_, binary = cv2.threshold(
    gray,
    0,
    255,
    cv2.THRESH_BINARY + cv2.THRESH_OTSU
)
```

It is especially useful when foreground and background form reasonably separable intensity groups.

---

# 40. Edge Detection

An edge represents a significant change in image intensity.

Edges can represent:

- Object boundaries
- Shape boundaries
- Surface changes

Common algorithms:

- Sobel
- Scharr
- Laplacian
- Canny

---

# 41. Sobel Operator

Sobel calculates image intensity gradients.

There are commonly separate horizontal and vertical operators.

```python
sobel_x = cv2.Sobel(
    gray,
    cv2.CV_64F,
    1,
    0,
    ksize=3
)

sobel_y = cv2.Sobel(
    gray,
    cv2.CV_64F,
    0,
    1,
    ksize=3
)
```

---

# 42. Laplacian Operator

Laplacian uses second-order derivatives.

```python
laplacian = cv2.Laplacian(
    gray,
    cv2.CV_64F
)
```

It can detect rapid intensity changes but may be more sensitive to noise.

---

# 43. Canny Edge Detection

Canny is a widely used multi-stage edge detector.

```python
edges = cv2.Canny(
    gray,
    100,
    200
)
```

Conceptual stages:

1. Noise reduction
2. Gradient calculation
3. Non-maximum suppression
4. Double thresholding
5. Edge tracking by hysteresis

### Interview point

Canny is generally more robust than simply applying a single derivative filter because it uses multiple stages to produce thin and connected edges.

---

# 44. Morphological Operations

Morphological operations work mainly with binary images and a structuring element.

Important operations:

- Erosion
- Dilation
- Opening
- Closing

Applications:

- Remove small noise
- Fill small holes
- Separate objects
- Connect nearby regions

---

# 45. Erosion

Erosion shrinks foreground regions.

Useful for:

- Removing small objects
- Separating connected objects
- Removing boundary pixels

```python
kernel = np.ones((3, 3), np.uint8)

eroded = cv2.erode(
    binary,
    kernel,
    iterations=1
)
```

---

# 46. Dilation

Dilation expands foreground regions.

Useful for:

- Filling gaps
- Connecting nearby components
- Strengthening objects

```python
dilated = cv2.dilate(
    binary,
    kernel,
    iterations=1
)
```

---

# 47. Opening

Opening:

```text
Erosion → Dilation
```

Useful for removing small noise while preserving larger structures.

---

# 48. Closing

Closing:

```text
Dilation → Erosion
```

Useful for:

- Filling small holes
- Closing small gaps
- Connecting nearby foreground regions

---

# 49. Geometric Transformations

Common transformations:

- Translation
- Rotation
- Scaling
- Reflection
- Affine transformation
- Perspective transformation

---

# 50. Translation

Translation shifts an image horizontally or vertically.

Conceptually:

```text
x' = x + tx
y' = y + ty
```

---

# 51. Rotation

Rotation changes image orientation.

```python
matrix = cv2.getRotationMatrix2D(
    center,
    angle,
    scale
)

rotated = cv2.warpAffine(
    image,
    matrix,
    (width, height)
)
```

---

# 52. Affine Transformation

Affine transformations preserve:

- Straight lines
- Parallel lines

They can represent:

- Translation
- Rotation
- Scaling
- Shearing

---

# 53. Perspective Transformation

Perspective transformation maps points from one plane/view to another.

Useful for:

- Document scanning
- Bird's-eye views
- Perspective correction

Example:

```text
Camera image
     ↓
Perspective transform
     ↓
Rectified document
```

---

# 54. Image Segmentation

Segmentation divides an image into meaningful regions.

Examples:

- Foreground/background
- Tumor region
- Road region
- Person region

Main approaches:

- Thresholding
- Region-based segmentation
- Clustering
- Contours
- Semantic segmentation
- Instance segmentation

---

# 55. Contours

Contours represent boundaries of connected regions.

```python
contours, hierarchy = cv2.findContours(
    binary,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)
```

Applications:

- Shape detection
- Object counting
- Area calculation
- Boundary analysis

---

# 56. Contour Area

```python
area = cv2.contourArea(contour)
```

Useful for filtering objects by size.

Example:

```text
if area > minimum_area:
    keep object
```

---

# 57. Bounding Rectangle

```python
x, y, w, h = cv2.boundingRect(contour)
```

It gives a rectangular region around the contour.

---

# 58. Object Detection vs Classification

### Image Classification

Answers:

> What is in the image?

Example:

```text
Image → Dog
```

### Object Detection

Answers:

> What objects are present and where are they?

Example:

```text
Dog → bounding box
Cat → bounding box
Person → bounding box
```

---

# 59. Object Detection Pipeline

Typical pipeline:

```text
Input Image
    ↓
Preprocessing
    ↓
Detection Model
    ↓
Candidate Boxes
    ↓
Confidence Scores
    ↓
Non-Maximum Suppression
    ↓
Final Bounding Boxes
```

Popular model families include:

- YOLO
- SSD
- Faster R-CNN
- RetinaNet
- DETR

---

# 60. YOLO

YOLO stands for:

```text
You Only Look Once
```

YOLO treats object detection largely as a single neural-network inference problem.

Advantages:

- Fast
- Suitable for real-time applications
- Strong practical performance

Applications:

- CCTV
- Traffic monitoring
- Industrial inspection
- Retail analytics
- Robotics

---

# 61. Non-Maximum Suppression (NMS)

A detector may produce multiple overlapping boxes for the same object.

NMS removes redundant boxes.

Basic process:

1. Sort boxes by confidence.
2. Select highest-confidence box.
3. Calculate overlap with remaining boxes.
4. Suppress boxes above an IoU threshold.
5. Continue.

---

# 62. IoU

IoU means:

```text
Intersection over Union
```

Formula:

```text
IoU =
Area of Intersection
--------------------
Area of Union
```

IoU measures overlap between predicted and ground-truth bounding boxes.

Example interpretation:

```text
IoU = 1.0 → perfect overlap
IoU = 0.0 → no overlap
```

---

# 63. Image Classification

Classification maps an image to one or more classes.

Example:

```text
Input image
     ↓
CNN
     ↓
Probabilities
     ↓
Cat: 0.92
Dog: 0.05
Other: 0.03
```

For multiclass classification, softmax is commonly used in the final layer.

---

# 64. Multi-Class vs Multi-Label

### Multi-Class

Exactly one class is selected.

```text
Cat OR Dog OR Horse
```

### Multi-Label

Multiple classes can be true simultaneously.

```text
Person + Helmet + Vehicle
```

Sigmoid outputs are commonly used for multi-label classification.

---

# 65. CNN Fundamentals

CNN means:

```text
Convolutional Neural Network
```

CNNs are designed to learn spatial patterns.

Typical architecture:

```text
Input Image
    ↓
Convolution
    ↓
Activation
    ↓
Pooling
    ↓
Convolution
    ↓
Activation
    ↓
Pooling
    ↓
Flatten / Global Pooling
    ↓
Fully Connected Layer
    ↓
Output
```

---

# 66. Why CNNs Work Well for Images

Images contain local spatial patterns.

Early CNN layers may learn:

- Edges
- Lines
- Corners

Middle layers may learn:

- Textures
- Shapes
- Parts

Deeper layers may learn:

- Objects
- Complex semantic patterns

This creates hierarchical feature learning.

---

# 67. Convolution in CNN

A CNN kernel learns weights rather than using a manually designed fixed filter.

Conceptually:

```text
Input Image
     ↓
Learnable Filters
     ↓
Feature Maps
```

The network learns which patterns are useful for the task.

---

# 68. Stride

Stride controls how far the kernel moves.

Example:

```text
Stride = 1
```

moves one pixel at a time.

```text
Stride = 2
```

moves two pixels at a time and generally reduces spatial dimensions.

---

# 69. Padding

Padding adds pixels around an image before convolution.

Common types:

### Valid Padding

No padding.

Spatial dimensions usually decrease.

### Same Padding

Padding is selected to preserve spatial dimensions for suitable stride settings.

---

# 70. Pooling

Pooling reduces spatial dimensions.

Common types:

- Max pooling
- Average pooling

### Max Pooling

Selects the maximum value in each local region.

Example:

```text
[1 3
 2 4]

Max = 4
```

Benefits:

- Reduces computation
- Provides some translation tolerance
- Compresses feature maps

---

# 71. Activation Functions in CNNs

Common functions:

- ReLU
- Sigmoid
- Tanh
- Softmax

ReLU:

```text
f(x) = max(0, x)
```

It introduces non-linearity and is widely used in hidden layers.

---

# 72. Transfer Learning

Transfer learning starts with a model trained on a large dataset and adapts it to a new task.

Typical process:

```text
Pretrained CNN
      ↓
Remove / replace final layer
      ↓
Add task-specific head
      ↓
Train on target dataset
```

Advantages:

- Less training data required
- Faster training
- Often better performance

Common pretrained families:

- ResNet
- VGG
- EfficientNet
- MobileNet
- ConvNeXt
- Vision Transformers

---

# 73. Feature Extraction vs Fine-Tuning

### Feature Extraction

Freeze most pretrained layers and train a new classifier.

```text
Backbone → Frozen
Head → Trainable
```

### Fine-Tuning

Unfreeze some or many backbone layers and continue training.

```text
Backbone → Partially trainable
Head → Trainable
```

Fine-tuning can produce better task-specific representations when sufficient data is available.

---

# 74. ResNet

ResNet introduced residual connections.

Conceptually:

```text
Input
  ↓
Layers
  ↓
+ Input
  ↓
Output
```

Residual learning helps train deeper networks.

---

# 75. MobileNet

MobileNet architectures are designed for efficient computation.

Useful for:

- Mobile devices
- Edge devices
- Real-time applications

They use depthwise separable convolutions to reduce computation compared with standard convolution.

---

# 76. Semantic Segmentation

Semantic segmentation assigns a class to every pixel.

Example:

```text
Road → road
Car → car
Person → person
Sky → sky
```

All objects of the same class share the same label.

---

# 77. Instance Segmentation

Instance segmentation distinguishes individual object instances.

Example:

```text
Person 1 → separate mask
Person 2 → separate mask
Person 3 → separate mask
```

Popular model family:

```text
Mask R-CNN
```

---

# 78. Semantic vs Instance Segmentation

| Task | Output |
|---|---|
| Classification | Class |
| Detection | Class + Bounding Box |
| Semantic Segmentation | Class per pixel |
| Instance Segmentation | Object instance + pixel mask |

---

# 79. Object Tracking

Tracking follows an object across video frames.

Example:

```text
Frame 1 → Person ID 7
Frame 2 → Person ID 7
Frame 3 → Person ID 7
```

Important components:

- Detection
- Motion estimation
- Association
- Identity management

Popular approaches include:

- SORT
- Deep SORT
- ByteTrack

---

# 80. Optical Flow

Optical flow estimates apparent motion of pixels between frames.

Applications:

- Motion analysis
- Tracking
- Video stabilization
- Action analysis

Common methods:

- Lucas-Kanade
- Farneback

---

# 81. Feature Detection

Feature detection identifies distinctive points or regions.

Examples:

- Corners
- Blobs
- Keypoints

Common algorithms:

- Harris Corner Detector
- FAST
- SIFT
- ORB

---

# 82. SIFT

SIFT stands for:

```text
Scale-Invariant Feature Transform
```

It detects and describes local image features.

It is designed to provide robustness to:

- Scale changes
- Rotation
- Some illumination/viewpoint changes

Typical stages:

1. Scale-space construction
2. Keypoint detection
3. Keypoint localization
4. Orientation assignment
5. Descriptor generation

---

# 83. ORB

ORB means:

```text
Oriented FAST and Rotated BRIEF
```

It is designed to be computationally efficient.

Advantages:

- Fast
- Suitable for real-time applications
- Useful for feature matching

---

# 84. Feature Matching

Feature matching finds corresponding features between images.

Example:

```text
Image A → Keypoints
Image B → Keypoints
       ↓
Descriptor Matching
       ↓
Corresponding Points
```

Applications:

- Image stitching
- Object recognition
- Image registration
- Tracking

---

# 85. Homography

Homography describes a projective transformation between two planes.

It is commonly used when matching points between images of the same planar surface.

Applications:

- Panorama stitching
- Document alignment
- Perspective correction

---

# 86. Image Registration

Image registration aligns two or more images.

Example:

```text
Image A
   ↓
Transformation
   ↓
Aligned Image B
```

Applications:

- Medical imaging
- Satellite imagery
- Change detection

---

# 87. Video Processing

A video is a sequence of frames.

```text
Frame 1
Frame 2
Frame 3
...
Frame N
```

If a video has:

```text
30 FPS
```

approximately 30 frames are processed each second.

A real-time system must consider:

- FPS
- Latency
- Resolution
- Model inference time
- Hardware acceleration

---

# 88. Computer Vision Evaluation Metrics

## Classification

Important metrics:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC

### Accuracy

```text
Accuracy =
Correct Predictions
-------------------
Total Predictions
```

Accuracy can be misleading for imbalanced datasets.

---

# 89. Precision

```text
Precision =
TP
-------
TP + FP
```

Precision answers:

> Of the predictions marked positive, how many were actually positive?

High precision means fewer false positives.

---

# 90. Recall

```text
Recall =
TP
-------
TP + FN
```

Recall answers:

> Of all actual positive cases, how many did the model detect?

High recall means fewer false negatives.

---

# 91. F1 Score

```text
F1 =
2 × Precision × Recall
----------------------
Precision + Recall
```

F1 balances precision and recall.

---

# 92. Detection Metrics

Important metrics:

- IoU
- Precision
- Recall
- AP
- mAP

### AP

Average Precision summarizes the precision-recall relationship for a class.

### mAP

Mean Average Precision averages AP across classes.

Depending on the benchmark, mAP may be reported at different IoU thresholds.

Always specify the evaluation convention.

---

# 93. Segmentation Metrics

Common metrics:

### Pixel Accuracy

Percentage of correctly classified pixels.

### IoU / Jaccard

```text
IoU = Intersection / Union
```

### Dice Coefficient

```text
Dice =
2 × Intersection
-----------------
Prediction + Ground Truth
```

Dice is widely used in medical and segmentation tasks.

---

# 94. Confusion Matrix for Vision Classification

For binary classification:

```text
                 Actual
              Pos       Neg

Pred Pos       TP        FP
Pred Neg       FN        TN
```

Use it to understand which errors the model is making.

---

# 95. Class Imbalance in Computer Vision

Example:

```text
Normal images = 95%
Defect images = 5%
```

A model predicting "Normal" for every image could achieve 95% accuracy but be useless.

Solutions:

- Data augmentation
- Class weighting
- Oversampling
- Undersampling
- Focal loss
- Better evaluation metrics

---

# 96. Data Leakage in Computer Vision

Data leakage occurs when information from validation/test data influences training.

A common mistake:

```text
Images from the same person
        ↓
Some in train
Some in test
```

The model may memorize person-specific characteristics.

Better:

```text
Person-level split
        ↓
Train people
Validation people
Test people
```

This is especially important for:

- Medical imaging
- Face recognition
- Human behavior analysis
- Video datasets

---

# 97. Image Dataset Splitting

Typical split:

```text
Training
Validation
Test
```

Example:

```text
70% Train
15% Validation
15% Test
```

The exact split depends on dataset size and project requirements.

For video data, split at the subject/video level when appropriate rather than randomly splitting individual frames.

---

# 98. Overfitting in Computer Vision

Overfitting occurs when a model performs well on training data but poorly on unseen data.

Symptoms:

```text
Training accuracy → very high
Validation accuracy → significantly lower
```

Solutions:

- More data
- Data augmentation
- Regularization
- Dropout
- Early stopping
- Transfer learning
- Reduce model complexity

---

# 99. Underfitting

Underfitting occurs when the model fails to learn the training patterns sufficiently.

Symptoms:

```text
Training performance → poor
Validation performance → poor
```

Possible solutions:

- Increase model capacity
- Improve features
- Train longer
- Reduce excessive regularization
- Improve preprocessing

---

# 100. Batch Size, Epochs and Learning Rate

### Batch Size

Number of samples processed before one parameter update.

### Epoch

One complete pass through the training dataset.

### Learning Rate

Controls how large parameter updates are during optimization.

These hyperparameters strongly affect training behavior.

---

# 101. CNN Training Workflow

```text
Collect Images
      ↓
Clean / Label Data
      ↓
Train / Validation / Test Split
      ↓
Resize
      ↓
Normalize
      ↓
Augmentation
      ↓
CNN / Pretrained Model
      ↓
Loss Function
      ↓
Optimizer
      ↓
Training
      ↓
Validation
      ↓
Hyperparameter Tuning
      ↓
Final Test
      ↓
Deployment
```

---

# 102. Common Loss Functions

### Binary Classification

Binary Cross Entropy:

```text
BCE
```

### Multi-Class Classification

Categorical Cross Entropy is commonly used.

### Multi-Label Classification

Binary cross entropy is commonly used independently across labels.

### Object Detection

Detection models generally use combinations of classification, localization, and sometimes objectness losses.

### Segmentation

Common losses:

- Cross entropy
- Dice loss
- Binary cross entropy
- Focal loss
- Combined losses

---

# 103. Computer Vision Pipeline in Python

A practical workflow:

```python
import cv2
import numpy as np

image = cv2.imread("image.jpg")

# Resize
image = cv2.resize(image, (224, 224))

# Convert to RGB
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Normalize
image = image.astype(np.float32) / 255.0

# Add batch dimension
image = np.expand_dims(image, axis=0)
```

The exact preprocessing must match the model used.

---

# 104. OpenCV

OpenCV is a widely used computer-vision library.

Important capabilities:

- Image reading/writing
- Video processing
- Filtering
- Thresholding
- Edge detection
- Morphology
- Contours
- Feature detection
- Object tracking
- Camera access

Common import:

```python
import cv2
```

---

# 105. NumPy in Computer Vision

Images are commonly represented as NumPy arrays.

Useful operations:

```python
image.shape
image.dtype
image.min()
image.max()
```

Array slicing is important for:

- Cropping
- ROI extraction
- Channel manipulation

---

# 106. PyTorch / TensorFlow

Deep-learning frameworks commonly used for vision:

- PyTorch
- TensorFlow
- Keras

Typical workflow:

```text
Dataset
 ↓
DataLoader / tf.data
 ↓
Model
 ↓
Loss
 ↓
Optimizer
 ↓
Training
 ↓
Validation
 ↓
Inference
```

---

# 107. Modern Computer Vision

Modern CV includes:

- CNNs
- Vision Transformers
- Multimodal models
- Self-supervised learning
- Foundation models
- Vision-language models
- Diffusion models

---

# 108. Vision Transformers (ViT)

Vision Transformer applies transformer concepts to images.

Basic idea:

```text
Image
 ↓
Image patches
 ↓
Patch embeddings
 ↓
Transformer
 ↓
Representation
 ↓
Prediction
```

Instead of processing the entire image as a single object, an image can be divided into patches.

---

# 109. Vision-Language Models

Vision-language models combine visual and textual understanding.

Examples of tasks:

- Image captioning
- Visual question answering
- Image-text retrieval
- Visual reasoning
- Multimodal assistants

Conceptually:

```text
Image + Text
     ↓
Multimodal Model
     ↓
Text / Classification / Reasoning
```

---

# 110. OCR

OCR means:

```text
Optical Character Recognition
```

It extracts text from images.

Pipeline:

```text
Image
 ↓
Preprocessing
 ↓
Text Detection
 ↓
Text Recognition
 ↓
Post-processing
 ↓
Structured Text
```

Popular tools include:

- Tesseract
- Cloud Vision APIs
- Deep-learning OCR systems

Applications:

- Invoice processing
- ID document extraction
- Purchase orders
- Forms
- Receipts

---

# 111. Pose Estimation

Pose estimation identifies human body keypoints.

Typical keypoints:

- Nose
- Shoulders
- Elbows
- Wrists
- Hips
- Knees
- Ankles

Pipeline:

```text
Video
 ↓
Person Detection
 ↓
Pose Estimation
 ↓
Keypoints
 ↓
Feature Engineering
 ↓
Activity / Behavior Analysis
```

Popular libraries/models include:

- MediaPipe
- OpenPose
- YOLO-based pose models

---

# 112. Action Recognition

Action recognition attempts to identify human activities from images or video.

Examples:

- Walking
- Running
- Jumping
- Sitting
- Hand movements

Approaches include:

```text
Video
 ↓
Frame extraction
 ↓
Pose / CNN features
 ↓
Temporal model
 ↓
Action class
```

Temporal models can include:

- LSTM
- GRU
- 3D CNN
- Transformers

---

# 113. Real-Time Computer Vision

A real-time system typically looks like:

```text
Camera
  ↓
Frame Capture
  ↓
Preprocessing
  ↓
Detection / Tracking
  ↓
Post-processing
  ↓
Display / Alert / Storage
```

Important metrics:

### FPS

Frames processed per second.

### Latency

Time required to process one frame or request.

### Throughput

Number of inputs processed per unit time.

A model with high accuracy but excessive latency may not be suitable for real-time deployment.

---

# 114. Model Optimization

For production CV systems:

- Resize inputs appropriately
- Use smaller architectures
- Quantize models
- Prune unnecessary weights where appropriate
- Use batching where latency permits
- Use GPU acceleration
- Use ONNX/TensorRT where appropriate
- Optimize preprocessing
- Avoid unnecessary frame processing

---

# 115. Edge Deployment

Computer vision may run on:

- Cloud GPU
- Local server
- Laptop
- Mobile device
- Embedded device
- Edge accelerator

Edge inference can reduce:

- Network latency
- Bandwidth usage
- Dependence on cloud connectivity

But hardware constraints become important.

---

# 116. Production Computer Vision Architecture

A simplified architecture:

```text
Camera / Image Source
        ↓
Data Ingestion
        ↓
Preprocessing
        ↓
CV Model
        ↓
Post-processing
        ↓
Business Rules
        ↓
Database / API / Dashboard
        ↓
Monitoring
```

Monitoring should consider:

- Model latency
- Error rate
- Data drift
- Input quality
- Prediction distribution
- Hardware utilization
- Model accuracy when labels become available

---

# 117. Computer Vision Project Best Practices

## Data

- Inspect class distribution
- Remove corrupted images
- Check duplicates
- Verify labels
- Detect leakage
- Use representative samples

## Preprocessing

- Keep preprocessing consistent between training and inference.
- Record image dimensions.
- Normalize according to the model requirements.
- Handle poor-quality images.

## Training

- Use validation data correctly.
- Track metrics.
- Save checkpoints.
- Use early stopping when appropriate.
- Track experiments.

## Evaluation

Do not rely only on accuracy.

Use task-specific metrics.

## Deployment

Measure:

- Accuracy
- Latency
- FPS
- Memory
- CPU/GPU utilization

---

# 118. Common Computer Vision Mistakes

### Mistake 1: Ignoring BGR vs RGB

OpenCV loads images in BGR.

### Mistake 2: Randomly splitting video frames

Frames from the same video can be extremely similar.

### Mistake 3: Using only accuracy

Especially dangerous with class imbalance.

### Mistake 4: Data augmentation leakage

Do not let augmented versions of the same source image leak across train/test.

### Mistake 5: Wrong preprocessing

Training and inference preprocessing must match.

### Mistake 6: Ignoring image quality

Blur, lighting, occlusion and camera angle can strongly affect performance.

### Mistake 7: Using a large model unnecessarily

For real-time systems, latency and hardware constraints matter.

---

# 119. End-to-End Computer Vision Project

A strong interview explanation should follow this structure:

```text
1. Business Problem
2. Data Collection
3. Data Understanding
4. Data Labeling
5. Train/Validation/Test Split
6. Image Preprocessing
7. Data Augmentation
8. Baseline Model
9. Model Training
10. Hyperparameter Tuning
11. Evaluation
12. Error Analysis
13. Optimization
14. Deployment
15. Monitoring
```

---

# 120. Example: Human Behavior Detection Project

Suppose the objective is to detect a specific behavior from video.

### Step 1 — Input

```text
Webcam / Video
```

### Step 2 — Frame extraction

```text
Video → Frames
```

### Step 3 — Person detection

Identify people in the frame.

### Step 4 — Pose estimation

Extract body keypoints.

### Step 5 — Feature engineering

Possible features:

- Joint angles
- Joint distances
- Movement velocity
- Temporal changes
- Body-part trajectories

### Step 6 — Classification

Classify the observed behavior.

```text
Features
   ↓
ML / Deep Learning Model
   ↓
Behavior
```

### Step 7 — Evaluation

Use:

- Precision
- Recall
- F1
- Confusion matrix
- Subject-level validation

### Step 8 — Deployment

```text
Camera
 ↓
Real-time inference
 ↓
Prediction
 ↓
Alert / Dashboard
```

---

# 121. Interview-Level Questions

## Basic

### Q1. What is image processing?

Image processing manipulates digital images to enhance them, transform them, or extract useful information.

### Q2. What is computer vision?

Computer vision enables machines to interpret and understand information from images and videos.

### Q3. What is a pixel?

A pixel is the smallest addressable element of a digital image containing intensity or color information.

### Q4. What is the difference between RGB and BGR?

RGB stores channels as Red-Green-Blue, while OpenCV commonly represents images as Blue-Green-Red.

### Q5. Why convert an image to grayscale?

It reduces the representation from multiple color channels to one intensity channel, simplifying many processing tasks and reducing computation.

---

# 122. Intermediate Interview Questions

### Q6. What is convolution?

Convolution applies a kernel over local image regions to calculate feature responses.

### Q7. Why is Gaussian blur used before Canny?

It reduces noise so that the edge detector is less likely to detect noise as false edges.

### Q8. What is thresholding?

Thresholding converts pixels into classes, commonly separating foreground from background according to intensity.

### Q9. What is the difference between erosion and dilation?

Erosion shrinks foreground regions, while dilation expands them.

### Q10. What is morphological opening?

Opening is erosion followed by dilation and is commonly used to remove small noise.

### Q11. What is morphological closing?

Closing is dilation followed by erosion and is commonly used to fill small holes and gaps.

### Q12. What is ROI?

ROI is a selected region of an image relevant to the task.

---

# 123. Advanced Interview Questions

### Q13. Why are CNNs effective for image data?

CNNs exploit local spatial structure and learn hierarchical representations through convolutional filters.

### Q14. What is padding?

Padding adds pixels around an input before convolution to control output dimensions and preserve border information.

### Q15. What is stride?

Stride controls the step size with which a convolution kernel moves across the input.

### Q16. What is transfer learning?

Transfer learning adapts representations learned from a pretrained model to a new task.

### Q17. Detection vs segmentation?

Detection predicts object classes and bounding boxes; segmentation predicts pixel-level regions.

### Q18. What is NMS?

Non-Maximum Suppression removes redundant overlapping detection boxes and keeps the most confident predictions.

### Q19. What is IoU?

IoU measures overlap between predicted and reference regions using intersection divided by union.

### Q20. Why can frame-level random splitting be problematic?

Neighboring frames from the same video are highly correlated, so random frame splitting can cause leakage and overly optimistic evaluation.

---

# 124. Scenario-Based Interview Questions

### Q21. Your model has 98% accuracy but poor business performance. Why?

Possible reasons:

- Class imbalance
- Wrong evaluation metric
- Data leakage
- Poor minority-class recall
- Distribution shift
- Incorrect labels

I would inspect the confusion matrix, per-class metrics, validation strategy, and data distribution.

### Q22. Your model works in the lab but fails in production. What do you investigate?

I would investigate:

1. Lighting differences
2. Camera differences
3. Resolution changes
4. Background changes
5. Occlusion
6. Data distribution shift
7. Preprocessing mismatch
8. Label quality
9. Model latency
10. Hardware constraints

### Q23. How would you make a CV model real-time?

I would profile the entire pipeline rather than only the model. Then optimize image resolution, model architecture, preprocessing, inference runtime and hardware acceleration while measuring FPS and latency.

### Q24. How would you reduce false positives?

Depending on the task:

- Tune decision thresholds
- Improve training data
- Add hard-negative examples
- Improve preprocessing
- Use stronger validation
- Tune NMS for detection
- Analyze false-positive samples

### Q25. How would you handle insufficient training images?

I would consider:

- Transfer learning
- Data augmentation
- Better labeling
- Collection of additional representative data
- Cross-validation where appropriate
- Regularization
- Synthetic data if justified

---

# 125. Must-Know Formula Sheet

## Pixel values

```text
8-bit image → 0 to 255
```

## Number of values

```text
2^n
```

## Standardization

```text
z = (x - μ) / σ
```

## Accuracy

```text
(TP + TN) / (TP + TN + FP + FN)
```

## Precision

```text
TP / (TP + FP)
```

## Recall

```text
TP / (TP + FN)
```

## F1

```text
2PR / (P + R)
```

## IoU

```text
Intersection / Union
```

## Dice

```text
2 × Intersection / (Prediction + Ground Truth)
```

---

# 126. Practical Python/OpenCV Cheat Sheet

```python
import cv2
import numpy as np

# Read
image = cv2.imread("image.jpg")

# Shape
print(image.shape)

# Grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Resize
resized = cv2.resize(image, (224, 224))

# Gaussian blur
blur = cv2.GaussianBlur(gray, (5, 5), 0)

# Canny
edges = cv2.Canny(gray, 100, 200)

# Threshold
_, binary = cv2.threshold(
    gray, 127, 255, cv2.THRESH_BINARY
)

# Morphology
kernel = np.ones((3, 3), np.uint8)

eroded = cv2.erode(binary, kernel)
dilated = cv2.dilate(binary, kernel)

# Contours
contours, hierarchy = cv2.findContours(
    binary,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)

# Save
cv2.imwrite("output.jpg", image)
```

---

# 127. Recommended Learning Sequence

## Beginner

- Pixels
- Image dimensions
- Channels
- RGB/BGR
- Grayscale
- Resolution
- Bit depth
- Image loading
- Resizing
- Cropping
- Normalization

## Intermediate

- Histograms
- Contrast enhancement
- Filtering
- Gaussian blur
- Median filtering
- Thresholding
- Otsu
- Canny
- Sobel
- Morphology
- Contours
- Geometric transformations

## Advanced

- Convolution
- CNNs
- Transfer learning
- Object detection
- NMS
- IoU
- Segmentation
- Tracking
- Optical flow
- Feature matching
- Pose estimation
- Video analytics
- Real-time inference

## Expert / AI Engineer Level

- Vision Transformers
- Vision-language models
- Multimodal AI
- Model optimization
- Quantization
- Edge inference
- Production monitoring
- Data drift
- Model serving
- Distributed inference
- Experiment tracking
- End-to-end CV system design

---

# 128. What You Should Be Able to Explain in an Interview

By the end of this topic, you should be able to explain:

- How an image is represented in memory.
- Difference between RGB, BGR, grayscale and HSV.
- Why preprocessing is required.
- Difference between normalization and standardization.
- Why resizing is required.
- How convolution works.
- What kernels and feature maps are.
- Difference between Gaussian, median and bilateral filtering.
- How Canny edge detection works.
- Difference between erosion, dilation, opening and closing.
- Thresholding and Otsu thresholding.
- What contours are.
- Classification vs detection vs segmentation.
- IoU and NMS.
- CNN architecture.
- Padding and stride.
- Pooling.
- Transfer learning and fine-tuning.
- Data augmentation.
- Overfitting and class imbalance.
- Detection and segmentation metrics.
- Object tracking.
- Pose estimation.
- Real-time computer vision.
- Production deployment challenges.
- Data leakage in video datasets.
- How to design an end-to-end CV project.

---

# 129. Final Mental Model

Remember the complete hierarchy:

```text
IMAGE PROCESSING
│
├── Image Representation
│   ├── Pixels
│   ├── Channels
│   ├── Resolution
│   └── Color Spaces
│
├── Preprocessing
│   ├── Resize
│   ├── Crop
│   ├── Normalize
│   ├── Denoise
│   └── Augment
│
├── Classical Computer Vision
│   ├── Histograms
│   ├── Thresholding
│   ├── Filtering
│   ├── Edges
│   ├── Morphology
│   ├── Contours
│   └── Features
│
└── DEEP LEARNING COMPUTER VISION
    │
    ├── CNN
    │   ├── Convolution
    │   ├── Activation
    │   ├── Pooling
    │   └── Feature Maps
    │
    ├── Classification
    │
    ├── Object Detection
    │   ├── Bounding Boxes
    │   ├── Confidence
    │   ├── IoU
    │   └── NMS
    │
    ├── Segmentation
    │   ├── Semantic
    │   └── Instance
    │
    ├── Tracking
    ├── Pose Estimation
    ├── Optical Flow
    ├── Vision Transformers
    └── Multimodal / Vision-Language AI
```

---

# 130. Interview Preparation Strategy

For each concept, prepare four levels:

### Level 1 — Definition

Be able to define the concept in 1–2 sentences.

### Level 2 — Intuition

Explain why it exists and what problem it solves.

### Level 3 — Technical Depth

Explain:

- Formula
- Algorithm
- Parameters
- Advantages
- Limitations

### Level 4 — Real Project

Explain:

```text
Problem
→ Data
→ Preprocessing
→ Model
→ Evaluation
→ Errors
→ Optimization
→ Deployment
```

This progression is especially important for Data Scientist, ML Engineer and AI Engineer interviews because interviewers often move from a basic definition to implementation details and then to production scenarios.

---

# Top-Company Interview Preparation — Organized Q&A

> **Target roles:** Data Scientist, ML Engineer, AI/ML Engineer, AI Engineer, Computer Vision Engineer, Applied Scientist.
>
> Recent 2025–2026 interview-preparation sources consistently emphasize CV fundamentals, CNNs, object detection, segmentation, transfer learning, Python/programming, practical debugging, ML system design, and deployment trade-offs. The questions below are organized to prepare for that progression rather than as a claim that these are verbatim questions from a specific company's interview.

## 1. Interviewer's Expected Progression

Prepare every important topic at four levels:

```text
Definition
   ↓
Intuition
   ↓
Technical / Mathematical depth
   ↓
Real-world trade-off + implementation
```

For example, if asked **"What is IoU?"**, do not stop at the formula. Be ready for:

- Why is IoU needed?
- Where is it used?
- How is it used in NMS?
- How is it used for detection evaluation?
- What happens when the IoU threshold changes?
- What problems occur with tiny objects?

---

# 2. Topic Order for Interview Preparation

## Level 1 — Fundamentals

1. Image and pixel representation
2. Dimensions and channels
3. RGB, BGR, grayscale, HSV
4. Resolution and bit depth
5. NumPy arrays
6. OpenCV basics

## Level 2 — Classical Image Processing

7. Resize and interpolation
8. Crop and ROI
9. Normalization
10. Histograms
11. Contrast enhancement
12. Noise
13. Gaussian, median and bilateral filtering
14. Convolution and kernels
15. Thresholding
16. Otsu and adaptive thresholding
17. Sobel and Laplacian
18. Canny
19. Erosion and dilation
20. Opening and closing
21. Contours
22. Geometric transformations

## Level 3 — Classical Computer Vision

23. Feature detection
24. SIFT
25. ORB
26. Feature descriptors
27. Feature matching
28. Homography
29. Image registration
30. Optical flow
31. Tracking

## Level 4 — Deep Learning

32. Neural-network basics
33. CNN
34. Convolution
35. Stride
36. Padding
37. Receptive field
38. Activation functions
39. Pooling
40. Batch normalization
41. Dropout
42. Loss functions
43. Optimizers
44. Backpropagation

## Level 5 — Vision Tasks

45. Classification
46. Multi-class vs multi-label
47. Object detection
48. IoU
49. NMS
50. Precision and recall
51. AP and mAP
52. Semantic segmentation
53. Instance segmentation
54. Pose estimation
55. OCR
56. Action recognition

## Level 6 — Modern Vision

57. Transfer learning
58. Fine-tuning
59. ResNet
60. EfficientNet
61. MobileNet
62. YOLO
63. Faster R-CNN
64. Feature pyramids
65. Vision Transformers
66. Vision-language models

## Level 7 — Production and System Design

67. Data leakage
68. Class imbalance
69. Domain shift
70. Data drift
71. Error analysis
72. Latency and FPS
73. Quantization
74. Model optimization
75. Edge inference
76. Monitoring
77. End-to-end CV architecture

---

# 3. Basic Interview Questions

## Q1. What is computer vision?

**Interview-ready answer:**

Computer vision is a field of AI that enables machines to extract information and make decisions from images and videos. Typical tasks include classification, object detection, segmentation, OCR, tracking and pose estimation.

**Follow-up:** What is the difference between image processing and computer vision?

**Answer:** Image processing mainly transforms or enhances images, while computer vision focuses on extracting semantic information and making predictions from visual data. Image processing is often part of a CV pipeline.

---

## Q2. What is a pixel?

**Answer:** A pixel is a basic addressable element of a digital image. In a grayscale image it represents intensity; in a color image it stores values for multiple color channels.

---

## Q3. What does an image shape of `(224, 224, 3)` mean?

**Answer:** It means height = 224 pixels, width = 224 pixels, and 3 color channels. If represented as a batch in channels-first format, it may instead appear as `(batch, 3, 224, 224)`.

---

## Q4. RGB vs BGR?

**Answer:** RGB stores channels as Red-Green-Blue, while BGR stores Blue-Green-Red. OpenCV commonly loads color images in BGR order. This can cause incorrect colors if the array is displayed by a library expecting RGB.

```python
rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```

---

## Q5. Why convert an image to grayscale?

**Answer:** If color is not required, grayscale reduces three color channels to one intensity channel, lowering memory and computation and simplifying many classical CV operations.

---

## Q6. What is image resolution?

**Answer:** Resolution is the number of pixels used to represent an image, such as 1920×1080. Increasing resolution can preserve more detail but increases memory and computation.

---

## Q7. What is an ROI?

**Answer:** ROI means Region of Interest. It is a selected portion of an image that contains information relevant to the task. Processing an ROI can reduce computation and background noise.

---

# 4. Image Processing Questions

## Q8. Why do we resize images before a deep-learning model?

**Answer:** Models commonly require a consistent input shape. Resizing provides a fixed tensor size and controls inference cost. However, aggressive resizing can remove small-object or fine-grained information.

---

## Q9. What is interpolation?

**Answer:** Interpolation estimates pixel values when an image is resized or transformed. Common methods include nearest-neighbor, bilinear, bicubic and area interpolation.

**Follow-up:** Which is useful for downsampling?

**Answer:** `INTER_AREA` is often a good choice for downsampling in OpenCV because it uses area-based resampling.

---

## Q10. What is normalization?

**Answer:** Normalization transforms pixel values into a suitable numerical range, for example dividing 8-bit values by 255 to obtain values from 0 to 1. Deep-learning models may require specific mean/std preprocessing instead.

---

## Q11. What is convolution?

**Answer:** Convolution applies a small kernel over local image regions and calculates weighted sums. In classical image processing the kernel can be designed manually; in CNNs the filter weights are learned from training data.

---

## Q12. Why use Gaussian blur before Canny?

**Answer:** Noise can create false gradients and false edges. Gaussian smoothing suppresses high-frequency noise before gradient-based edge detection.

---

## Q13. Gaussian vs median filtering?

**Answer:** Gaussian filtering performs weighted averaging and is commonly used for general smoothing. Median filtering replaces a value with the local median and is particularly effective for salt-and-pepper noise while often preserving sharp boundaries better.

---

## Q14. What is thresholding?

**Answer:** Thresholding converts pixels into classes based on an intensity threshold, commonly separating foreground and background.

---

## Q15. Otsu vs adaptive thresholding?

**Answer:** Otsu selects a global threshold based on the histogram, while adaptive thresholding calculates a local threshold for different image regions. Adaptive thresholding is useful when illumination is uneven.

---

## Q16. Explain Canny edge detection.

**Answer:** Canny is a multi-stage edge detector. It typically performs noise reduction, gradient calculation, non-maximum suppression, double thresholding and edge tracking by hysteresis to produce thin and connected edges.

---

## Q17. Erosion vs dilation?

**Answer:** Erosion shrinks foreground regions and can remove small objects. Dilation expands foreground regions and can fill small gaps or connect nearby regions.

---

## Q18. Opening vs closing?

**Answer:** Opening is erosion followed by dilation and is commonly used to remove small noise. Closing is dilation followed by erosion and is commonly used to fill small holes and gaps.

---

# 5. CNN Interview Questions

## Q19. Why are CNNs effective for images?

**Answer:** CNNs exploit local spatial structure, use shared weights and learn hierarchical features. Early layers can learn edges and textures, while deeper layers learn shapes, object parts and semantic representations.

---

## Q20. What is a feature map?

**Answer:** A feature map is the spatial response produced by applying a filter to an input representation. It indicates where the learned or specified pattern is present.

---

## Q21. What is stride?

**Answer:** Stride is the number of pixels by which a convolution kernel moves at each step. Increasing stride generally reduces spatial dimensions and computation.

---

## Q22. What is padding?

**Answer:** Padding adds pixels around an input before convolution. It controls spatial dimensions and helps preserve information near image boundaries.

---

## Q23. What is the convolution output-size formula?

For one spatial dimension:

```text
Output = floor((N + 2P - K) / S) + 1
```

where:

- `N` = input size
- `P` = padding
- `K` = kernel size
- `S` = stride

**Example:** `32`, kernel `3`, padding `0`, stride `1` gives `30`.

---

## Q24. What is a receptive field?

**Answer:** The receptive field is the region of the original input that can influence a particular activation. Deeper layers usually have larger effective receptive fields and can capture broader context.

---

## Q25. Why use ReLU?

**Answer:** ReLU introduces non-linearity while being computationally simple and helps avoid the strong saturation behavior of sigmoid/tanh in positive regions. It is widely used in hidden layers.

---

## Q26. What is pooling?

**Answer:** Pooling summarizes local feature-map regions, reducing spatial dimensions and computation. Max pooling selects the maximum; average pooling calculates the average.

---

## Q27. What is batch normalization?

**Answer:** Batch normalization normalizes intermediate activations using batch statistics during training and learned scale/shift parameters. It can stabilize optimization and often make training easier.

**Follow-up:** Does batch normalization always prevent overfitting?

**Answer:** No. It can have regularizing effects, but its primary role is activation normalization and optimization stabilization.

---

## Q28. What is dropout?

**Answer:** Dropout randomly disables a fraction of activations during training to reduce co-adaptation and act as a regularizer. It is disabled or handled differently during inference depending on the framework.

---

# 6. Classification Questions

## Q29. Classification vs detection?

**Answer:** Classification predicts the class of an image or crop. Detection predicts the class and location of multiple objects, usually with bounding boxes.

---

## Q30. Multi-class vs multi-label classification?

**Answer:** Multi-class classification generally selects one class from mutually exclusive classes, often using softmax. Multi-label classification allows multiple labels simultaneously, commonly using independent sigmoid outputs.

---

## Q31. Why can accuracy be misleading?

**Answer:** With class imbalance, a model can achieve high accuracy while failing on the minority class. I would inspect precision, recall, F1, confusion matrices and suitable PR-based metrics.

---

# 7. Object Detection Questions

## Q32. What is object detection?

**Answer:** Object detection identifies object categories and their locations, usually using bounding boxes and confidence scores.

---

## Q33. What is IoU?

**Answer:** IoU, or Intersection over Union, measures overlap between a predicted region and a reference region:

```text
IoU = Intersection Area / Union Area
```

It is used in localization evaluation and detection post-processing such as NMS.

---

## Q34. What is NMS?

**Answer:** Non-Maximum Suppression removes redundant overlapping detections. It typically keeps the highest-confidence box and suppresses other boxes whose overlap with it exceeds a chosen criterion.

---

## Q35. YOLO vs Faster R-CNN?

**Answer:** YOLO-style detectors are generally designed for efficient one-stage prediction, while Faster R-CNN uses a two-stage proposal-and-refinement design. I would choose based on accuracy, latency, hardware, object-size distribution and business requirements rather than assuming one is universally better.

---

## Q36. What is mAP?

**Answer:** mAP means mean Average Precision. AP summarizes the precision-recall relationship for a class under a specified evaluation protocol; mAP aggregates AP across classes and, depending on the benchmark, specified IoU thresholds.

**Interview trap:** Do not say mAP always means mAP@0.5. State the exact evaluation convention.

---

## Q37. How do you handle small objects in detection?

**Answer:** I would investigate higher input resolution, multi-scale feature representations such as feature pyramids, better labels, more small-object examples and an appropriate detector. The trade-off is increased compute and latency.

---

# 8. Segmentation Questions

## Q38. Semantic vs instance segmentation?

**Answer:** Semantic segmentation assigns a class to every pixel. Instance segmentation additionally separates different object instances belonging to the same class.

---

## Q39. What is Dice score?

**Answer:** Dice measures overlap between predicted and reference regions:

```text
Dice = 2 × Intersection / (Prediction + Ground Truth)
```

It is commonly used for segmentation, especially when foreground regions are relatively small.

---

## Q40. Detection vs segmentation?

**Answer:** Detection gives object-level localization such as bounding boxes; segmentation provides pixel-level localization through masks.

---

# 9. Transfer Learning and Architecture Questions

## Q41. What is transfer learning?

**Answer:** Transfer learning reuses representations learned from a pretrained model for a new task. It is especially useful when the target dataset is limited or training a model from scratch is expensive.

---

## Q42. Feature extraction vs fine-tuning?

**Answer:** In feature extraction, the pretrained backbone is frozen and a new head is trained. In fine-tuning, some or many backbone layers are unfrozen and adapted to the target dataset.

---

## Q43. Why can fine-tuning overfit?

**Answer:** Fine-tuning updates many parameters. With a small target dataset, the model can memorize target-specific examples rather than learn generalizable features. Lower learning rates, freezing more layers, augmentation and regularization can help.

---

## Q44. Why is ResNet important?

**Answer:** ResNet introduced residual/skip connections that provide shortcut paths around layers. This makes optimization of deep networks easier and helps address degradation problems associated with simply increasing network depth.

---

## Q45. Why use MobileNet?

**Answer:** MobileNet architectures are designed for computational efficiency and are useful when inference must run on mobile or edge hardware. Depthwise separable convolutions reduce computation compared with standard convolution.

---

# 10. Modern Vision Questions

## Q46. CNN vs Vision Transformer?

**Answer:** CNNs have strong locality and translation-related inductive biases through convolution. Vision Transformers use attention over image patch representations and can model broader relationships. The choice depends on data scale, pretraining, compute, task and deployment constraints.

---

## Q47. What is a Vision Transformer?

**Answer:** A Vision Transformer divides an image into patches, converts patches into embeddings and processes them using transformer layers with attention.

```text
Image
 ↓
Patches
 ↓
Patch embeddings
 ↓
Transformer
 ↓
Representation
 ↓
Prediction
```

---

## Q48. What are vision-language models?

**Answer:** Vision-language models jointly process visual and textual information for tasks such as image captioning, visual question answering, image-text retrieval and multimodal reasoning.

---

# 11. Data and Debugging Questions

## Q49. Training accuracy is 99% but validation accuracy is 70%. What do you do?

**Answer:**

1. Check for data leakage and duplicate images.
2. Verify train/validation distribution.
3. Inspect labels.
4. Analyze difficult validation examples.
5. Check whether augmentation is realistic.
6. Add regularization or early stopping.
7. Consider a smaller model.
8. Collect more representative data.
9. Examine class-wise metrics.

---

## Q50. Why is random frame splitting dangerous?

**Answer:** Neighboring frames from the same video are highly correlated. Putting similar frames into both train and test can cause leakage and overly optimistic performance. Split by video, subject, camera or another independent unit when appropriate.

---

## Q51. Production performance is worse than validation performance. Why?

**Answer:** Possible causes include domain shift, different cameras, lighting, resolution, backgrounds, preprocessing mismatch, label mismatch and data drift. I would compare production inputs against training data and perform slice-based error analysis.

---

## Q52. The dataset is 95% normal and 5% defective. What would you do?

**Answer:** I would not optimize accuracy alone. I would inspect minority-class recall and precision, use class weighting or focal loss when appropriate, add targeted augmentation, collect more representative defect examples and tune the operating threshold according to business cost.

---

# 12. Real-Time Computer Vision Questions

## Q53. How would you improve FPS?

**Answer:** First profile the entire pipeline. Then optimize the actual bottleneck: input resolution, preprocessing, model size, runtime, precision, hardware acceleration, frame sampling or post-processing. I would benchmark FPS and latency before and after each change.

---

## Q54. Accuracy vs latency—which is more important?

**Answer:** It depends on the application. I would first define hard product constraints, such as maximum latency and minimum recall, and then optimize the model within those constraints. The objective is an acceptable accuracy-latency-cost trade-off, not maximum accuracy in isolation.

---

## Q55. How would you deploy a model on an edge device?

**Answer:**

```text
Train
 ↓
Validate
 ↓
Export
 ↓
Optimize runtime
 ↓
Quantize if appropriate
 ↓
Benchmark on target hardware
 ↓
Revalidate accuracy
 ↓
Deploy
 ↓
Monitor
```

---

# 13. Advanced System-Design Questions

## Q56. Design a real-time people-counting system.

### Strong architecture

```text
Camera
 ↓
Frame capture
 ↓
Frame sampling
 ↓
Person detector
 ↓
Tracker
 ↓
Line/zone counting logic
 ↓
Events
 ↓
Backend / Dashboard
```

### Discuss

- Camera placement
- Occlusion
- Double counting
- Tracking stability
- Day/night variation
- FPS
- Latency
- Privacy
- Storage
- Monitoring

---

## Q57. Design a manufacturing defect detection system.

### Strong architecture

```text
Industrial Camera
 ↓
Image Quality Check
 ↓
Preprocessing
 ↓
Detection / Classification / Segmentation
 ↓
Confidence + Business Rules
 ↓
Accept / Reject
 ↓
Store Event
 ↓
Monitoring
```

### Important trade-offs

- False negatives can be more expensive than false positives.
- Small defects require sufficient resolution.
- Lighting should be controlled where possible.
- Camera calibration and product positioning matter.
- Uncertain predictions may require human review.

---

# 14. Project Interview Questions

For any CV project on your resume, prepare answers to:

1. What business problem did you solve?
2. Why did you use computer vision?
3. What was the input?
4. What was the output?
5. How much data did you have?
6. How was the data labeled?
7. How did you split the dataset?
8. What preprocessing did you perform?
9. What baseline did you establish?
10. Why did you choose the model?
11. What alternatives did you consider?
12. What evaluation metrics did you use?
13. What were the main failure cases?
14. How did you reduce false positives/negatives?
15. How did you prevent leakage?
16. What was the inference latency?
17. How did you deploy it?
18. How did you monitor it?
19. What would you improve now?
20. What was the measurable business impact?

---

# 15. Follow-Up Chain Example

If you say:

> "We used YOLO for object detection."

Expect:

```text
Why YOLO?
 ↓
Why not Faster R-CNN?
 ↓
What was the input resolution?
 ↓
What was your FPS?
 ↓
What was your mAP?
 ↓
Which IoU convention?
 ↓
How did NMS work?
 ↓
How did you handle small objects?
 ↓
How did you avoid data leakage?
 ↓
How did you deploy?
 ↓
How did you monitor production errors?
```

Prepare the complete chain, not just the first answer.

---

# 16. Coding Questions to Practice

## Easy

1. Reverse an image array horizontally.
2. Convert RGB to grayscale using a luminance formula.
3. Normalize a pixel array.
4. Calculate a histogram.
5. Extract an ROI with NumPy slicing.
6. Find min/max/mean pixel intensity.
7. Implement a simple binary threshold.

## Medium

8. Implement 2D convolution.
9. Implement mean filtering.
10. Implement max pooling.
11. Calculate IoU between two bounding boxes.
12. Implement basic NMS.
13. Calculate precision and recall.
14. Calculate Dice score.
15. Implement connected components.

## Advanced

16. Implement convolution with arbitrary stride and padding.
17. Implement batched IoU.
18. Implement efficient NMS.
19. Design a streaming inference pipeline.
20. Design subject-level dataset splitting.
21. Debug an inference pipeline whose latency doubled.
22. Design an inference service with batching.

---

# 17. Must-Know Formulas

## Accuracy

```text
(TP + TN) / (TP + TN + FP + FN)
```

## Precision

```text
TP / (TP + FP)
```

## Recall

```text
TP / (TP + FN)
```

## F1

```text
2 × Precision × Recall
----------------------
Precision + Recall
```

## IoU

```text
Intersection / Union
```

## Dice

```text
2 × Intersection
-----------------
Prediction + Ground Truth
```

## Convolution output

```text
floor((N + 2P - K) / S) + 1
```

---

# 18. Final 1-Day Revision Order

If the interview is tomorrow, revise in this order:

```text
1. Image representation
2. RGB/BGR/HSV/grayscale
3. Preprocessing
4. Convolution
5. Gaussian/median filtering
6. Canny
7. Thresholding
8. Morphology
9. CNN architecture
10. Stride/padding/receptive field
11. Transfer learning
12. Classification
13. Object detection
14. YOLO
15. IoU + NMS
16. Precision/Recall + mAP
17. Segmentation
18. Tracking
19. Data leakage
20. Class imbalance
21. Domain shift
22. Real-time inference
23. Project explanation
24. CV system design
```

---

# 19. Final Interview Rule

Do not memorize computer vision as isolated definitions.

For every important topic, be able to answer:

```text
What is it?
   ↓
Why is it needed?
   ↓
How does it work?
   ↓
What are its assumptions?
   ↓
What are its limitations?
   ↓
When would I choose it?
   ↓
What alternative would I consider?
   ↓
How would I evaluate it?
   ↓
How would I deploy it?
```

That is the difference between a basic CV interview answer and an **ML Engineer / AI Engineer / Data Scientist-level engineering answer**.

---

# 20. Research Basis

The organization and emphasis of this interview guide were cross-checked against recent public interview-preparation material published/updated in 2025–2026. These sources emphasize CNNs, object detection, segmentation, transfer learning, programming, practical CV pipelines, system design and deployment trade-offs.

- Interview Query — Computer Vision Machine Learning Interview Questions, updated March 2026.
- DataInterview — Computer Vision Interview Questions, updated March 2026.
- Codefinity — Computer Vision Engineer Interview Questions and Answers, May 2026.
- TechInterview — Computer Vision interview guides, April 2026.
- Indeed — Computer Vision Interview Questions, updated December 2025.
- Coursera — Computer Vision Interview Questions, updated June 2026.

**Important:** Public preparation sites are useful for identifying recurring themes, but they do not establish that a specific company asks a specific question verbatim. Company-specific interviews vary by role, level, interviewer and team.
