Image Processing & Computer Vision — Data Science / ML / AI Engineer Notes
0. Learning Path
Follow this order:
Image fundamentals
Image representation and color spaces
Image I/O and visualization
Basic image operations
Image preprocessing
Histograms and thresholding
Edge detection
Morphological operations
Geometric transformations
Image filtering and convolution
Feature detection and description
Segmentation
Object detection
Object tracking
Feature extraction with CNNs
Transfer learning
Modern computer vision
OpenCV + Python workflow
Evaluation metrics
Deployment and production considerations
Interview questions
Practical project workflow
---
1. What Is Image Processing?
Image processing is the process of manipulating an image to improve it, extract useful information, or prepare it for further analysis.
Typical goals:
Remove noise
Improve contrast
Resize or rotate images
Detect edges
Segment regions
Extract features
Prepare images for machine learning
Example
An image captured from a camera may contain:
Noise
Poor lighting
Blur
Unwanted background
Different image sizes
Image processing can clean and transform the image before a machine-learning model receives it.
Simple pipeline
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
2. What Is Computer Vision?
Computer Vision (CV) is a broader field in which machines are trained to understand and interpret visual information from images and videos.
Image processing focuses heavily on manipulating images.
Computer vision focuses on understanding what the image contains.
Example
Image processing:
> "Remove noise from this image."
Computer vision:
> "Detect the person and identify their activity."
Relationship
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
3. Image vs Computer Vision vs Deep Learning
Concept	Main Purpose
Image Processing	Manipulate and improve images
Computer Vision	Understand visual content
Machine Learning	Learn patterns from data
Deep Learning	Learn complex representations automatically
CNN	Neural network architecture commonly used for vision
Object Detection	Locate and classify objects
Image Classification	Assign a class to an image
Segmentation	Assign labels to pixels/regions
---
4. How an Image Is Represented
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
`0` = black
`255` = white
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
5. Pixels
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
6. Image Dimensions
An image commonly has:
```text
Height × Width × Channels
```
Example:
```text
1080 × 1920 × 3
```
means:
Height = 1080 pixels
Width = 1920 pixels
Channels = 3
Important interview point
For a grayscale image:
```text
Height × Width
```
For a color image:
```text
Height × Width × Channels
```
---
7. Bit Depth
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
8. Resolution
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
Memory usage
Processing time
Storage requirements
---
9. Channels and Color Spaces
A color space defines how colors are represented.
Important color spaces:
RGB
BGR
HSV
Grayscale
LAB
YCrCb
---
10. RGB
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
11. BGR
OpenCV commonly uses BGR channel ordering instead of RGB.
```text
B → Blue
G → Green
R → Red
```
This is a very common interview question.
Important
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
12. Grayscale
A grayscale image contains one intensity channel instead of three color channels.
Typical representation:
```text
0   → black
255 → white
```
Advantages:
Lower memory usage
Faster processing
Simpler representation
Useful when color is not important
Example:
```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
---
13. HSV
HSV means:
```text
H → Hue
S → Saturation
V → Value
```
HSV is often useful for color-based segmentation because color information is separated from brightness.
Example use cases:
Detecting colored objects
Traffic-sign analysis
Color segmentation
Industrial inspection
```python
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
```
---
14. Image Acquisition
Images can originate from:
Cameras
Mobile devices
Satellites
Medical imaging systems
CCTV
Web datasets
Sensors
Video streams
A production CV system should consider:
Camera quality
Lighting
Frame rate
Resolution
Lens distortion
Camera position
---
15. Loading an Image with OpenCV
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
16. Saving an Image
```python
cv2.imwrite("output.jpg", image)
```
Always verify that:
The output path is correct.
The image is not empty.
The required format is supported.
---
17. Resizing
Images often need to be converted to a common size before ML inference.
```python
resized = cv2.resize(image, (224, 224))
```
Why resize?
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
18. Interpolation
When resizing, the algorithm estimates new pixel values.
Common interpolation methods:
Nearest Neighbor
Uses the nearest pixel.
Advantages:
Fast
Simple
Disadvantage:
Can produce blocky results
Bilinear
Uses neighboring pixels.
Generally smoother than nearest-neighbor.
Bicubic
Uses a larger neighborhood and can produce smoother results.
Area
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
19. Image Cropping
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
20. Region of Interest (ROI)
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
Lower computation
Less noise
Faster processing
More focused features
---
21. Image Normalization
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
Better numerical stability
More suitable neural-network inputs
Can improve optimization
---
22. Standardization
Standardization transforms values using:
```text
z = (x - mean) / standard_deviation
```
Unlike simple min-max normalization, standardization centers the values around zero.
For computer vision, the exact preprocessing depends on the model.
---
23. Data Augmentation
Data augmentation creates modified versions of training images.
Common transformations:
Rotation
Horizontal flip
Vertical flip
Crop
Translation
Scaling
Brightness changes
Contrast changes
Noise injection
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
Why augmentation?
It helps the model generalize to variations not seen exactly in training.
Important
Augmentation should usually be applied to training data, not blindly to validation/test data.
---
24. Noise in Images
Noise is unwanted variation in pixel values.
Common types:
Gaussian noise
Salt-and-pepper noise
Speckle noise
Sensor noise
Noise can reduce model performance and make edge/feature detection harder.
---
25. Image Filtering
Filtering modifies pixel values using neighboring pixels.
Applications:
Noise reduction
Smoothing
Sharpening
Edge detection
Common filters:
Mean filter
Gaussian filter
Median filter
Bilateral filter
---
26. Mean Filter
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
27. Gaussian Blur
Gaussian filtering applies a weighted average based on a Gaussian distribution.
```python
blur = cv2.GaussianBlur(image, (5, 5), 0)
```
Applications:
Noise reduction
Preprocessing before edge detection
Smoothing
Gaussian blur is frequently used before Canny edge detection.
---
28. Median Filter
Median filtering replaces a pixel with the median of its neighborhood.
It is particularly effective against salt-and-pepper noise.
```python
filtered = cv2.medianBlur(image, 5)
```
Mean vs Median
Filter	Typical Use
Mean	General smoothing
Gaussian	Smooth noise while preserving structure reasonably well
Median	Salt-and-pepper noise
---
29. Bilateral Filter
Bilateral filtering smooths an image while attempting to preserve edges.
```python
filtered = cv2.bilateralFilter(image, 9, 75, 75)
```
It considers:
Spatial distance
Intensity/color difference
---
30. Convolution
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
31. Kernel / Filter
A kernel is a small matrix used to detect a particular pattern.
Examples:
Horizontal edges
Vertical edges
Sharpening
Blurring
Example horizontal edge kernel:
```text
[-1 -1 -1
  0  0  0
  1  1  1]
```
The output indicates where corresponding patterns are present.
---
32. Image Histogram
An image histogram shows the distribution of pixel intensities.
For grayscale images:
```text
X-axis → intensity
Y-axis → frequency
```
A histogram helps understand:
Brightness
Contrast
Distribution
Saturation of intensities
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
33. Contrast
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
34. Histogram Equalization
Histogram equalization attempts to improve contrast by redistributing intensity values.
```python
equalized = cv2.equalizeHist(gray)
```
Useful for some low-contrast grayscale images.
---
35. CLAHE
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
36. Thresholding
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
37. Binary Thresholding
Produces two values:
```text
0
255
```
Useful for:
Document processing
Object separation
Simple segmentation
Shape extraction
---
38. Adaptive Thresholding
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
Documents
Uneven lighting
Text extraction
---
39. Otsu Thresholding
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
40. Edge Detection
An edge represents a significant change in image intensity.
Edges can represent:
Object boundaries
Shape boundaries
Surface changes
Common algorithms:
Sobel
Scharr
Laplacian
Canny
---
41. Sobel Operator
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
42. Laplacian Operator
Laplacian uses second-order derivatives.
```python
laplacian = cv2.Laplacian(
    gray,
    cv2.CV_64F
)
```
It can detect rapid intensity changes but may be more sensitive to noise.
---
43. Canny Edge Detection
Canny is a widely used multi-stage edge detector.
```python
edges = cv2.Canny(
    gray,
    100,
    200
)
```
Conceptual stages:
Noise reduction
Gradient calculation
Non-maximum suppression
Double thresholding
Edge tracking by hysteresis
Interview point
Canny is generally more robust than simply applying a single derivative filter because it uses multiple stages to produce thin and connected edges.
---
44. Morphological Operations
Morphological operations work mainly with binary images and a structuring element.
Important operations:
Erosion
Dilation
Opening
Closing
Applications:
Remove small noise
Fill small holes
Separate objects
Connect nearby regions
---
45. Erosion
Erosion shrinks foreground regions.
Useful for:
Removing small objects
Separating connected objects
Removing boundary pixels
```python
kernel = np.ones((3, 3), np.uint8)

eroded = cv2.erode(
    binary,
    kernel,
    iterations=1
)
```
---
46. Dilation
Dilation expands foreground regions.
Useful for:
Filling gaps
Connecting nearby components
Strengthening objects
```python
dilated = cv2.dilate(
    binary,
    kernel,
    iterations=1
)
```
---
47. Opening
Opening:
```text
Erosion → Dilation
```
Useful for removing small noise while preserving larger structures.
---
48. Closing
Closing:
```text
Dilation → Erosion
```
Useful for:
Filling small holes
Closing small gaps
Connecting nearby foreground regions
---
49. Geometric Transformations
Common transformations:
Translation
Rotation
Scaling
Reflection
Affine transformation
Perspective transformation
---
50. Translation
Translation shifts an image horizontally or vertically.
Conceptually:
```text
x' = x + tx
y' = y + ty
```
---
51. Rotation
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
52. Affine Transformation
Affine transformations preserve:
Straight lines
Parallel lines
They can represent:
Translation
Rotation
Scaling
Shearing
---
53. Perspective Transformation
Perspective transformation maps points from one plane/view to another.
Useful for:
Document scanning
Bird's-eye views
Perspective correction
Example:
```text
Camera image
     ↓
Perspective transform
     ↓
Rectified document
```
---
54. Image Segmentation
Segmentation divides an image into meaningful regions.
Examples:
Foreground/background
Tumor region
Road region
Person region
Main approaches:
Thresholding
Region-based segmentation
Clustering
Contours
Semantic segmentation
Instance segmentation
---
55. Contours
Contours represent boundaries of connected regions.
```python
contours, hierarchy = cv2.findContours(
    binary,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)
```
Applications:
Shape detection
Object counting
Area calculation
Boundary analysis
---
56. Contour Area
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
57. Bounding Rectangle
```python
x, y, w, h = cv2.boundingRect(contour)
```
It gives a rectangular region around the contour.
---
58. Object Detection vs Classification
Image Classification
Answers:
> What is in the image?
Example:
```text
Image → Dog
```
Object Detection
Answers:
> What objects are present and where are they?
Example:
```text
Dog → bounding box
Cat → bounding box
Person → bounding box
```
---
59. Object Detection Pipeline
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
YOLO
SSD
Faster R-CNN
RetinaNet
DETR
---
60. YOLO
YOLO stands for:
```text
You Only Look Once
```
YOLO treats object detection largely as a single neural-network inference problem.
Advantages:
Fast
Suitable for real-time applications
Strong practical performance
Applications:
CCTV
Traffic monitoring
Industrial inspection
Retail analytics
Robotics
---
61. Non-Maximum Suppression (NMS)
A detector may produce multiple overlapping boxes for the same object.
NMS removes redundant boxes.
Basic process:
Sort boxes by confidence.
Select highest-confidence box.
Calculate overlap with remaining boxes.
Suppress boxes above an IoU threshold.
Continue.
---
62. IoU
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
63. Image Classification
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
64. Multi-Class vs Multi-Label
Multi-Class
Exactly one class is selected.
```text
Cat OR Dog OR Horse
```
Multi-Label
Multiple classes can be true simultaneously.
```text
Person + Helmet + Vehicle
```
Sigmoid outputs are commonly used for multi-label classification.
---
65. CNN Fundamentals
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
66. Why CNNs Work Well for Images
Images contain local spatial patterns.
Early CNN layers may learn:
Edges
Lines
Corners
Middle layers may learn:
Textures
Shapes
Parts
Deeper layers may learn:
Objects
Complex semantic patterns
This creates hierarchical feature learning.
---
67. Convolution in CNN
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
68. Stride
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
69. Padding
Padding adds pixels around an image before convolution.
Common types:
Valid Padding
No padding.
Spatial dimensions usually decrease.
Same Padding
Padding is selected to preserve spatial dimensions for suitable stride settings.
---
70. Pooling
Pooling reduces spatial dimensions.
Common types:
Max pooling
Average pooling
Max Pooling
Selects the maximum value in each local region.
Example:
```text
[1 3
 2 4]

Max = 4
```
Benefits:
Reduces computation
Provides some translation tolerance
Compresses feature maps
---
71. Activation Functions in CNNs
Common functions:
ReLU
Sigmoid
Tanh
Softmax
ReLU:
```text
f(x) = max(0, x)
```
It introduces non-linearity and is widely used in hidden layers.
---
72. Transfer Learning
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
Less training data required
Faster training
Often better performance
Common pretrained families:
ResNet
VGG
EfficientNet
MobileNet
ConvNeXt
Vision Transformers
---
73. Feature Extraction vs Fine-Tuning
Feature Extraction
Freeze most pretrained layers and train a new classifier.
```text
Backbone → Frozen
Head → Trainable
```
Fine-Tuning
Unfreeze some or many backbone layers and continue training.
```text
Backbone → Partially trainable
Head → Trainable
```
Fine-tuning can produce better task-specific representations when sufficient data is available.
---
74. ResNet
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
75. MobileNet
MobileNet architectures are designed for efficient computation.
Useful for:
Mobile devices
Edge devices
Real-time applications
They use depthwise separable convolutions to reduce computation compared with standard convolution.
---
76. Semantic Segmentation
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
77. Instance Segmentation
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
78. Semantic vs Instance Segmentation
Task	Output
Classification	Class
Detection	Class + Bounding Box
Semantic Segmentation	Class per pixel
Instance Segmentation	Object instance + pixel mask
---
79. Object Tracking
Tracking follows an object across video frames.
Example:
```text
Frame 1 → Person ID 7
Frame 2 → Person ID 7
Frame 3 → Person ID 7
```
Important components:
Detection
Motion estimation
Association
Identity management
Popular approaches include:
SORT
Deep SORT
ByteTrack
---
80. Optical Flow
Optical flow estimates apparent motion of pixels between frames.
Applications:
Motion analysis
Tracking
Video stabilization
Action analysis
Common methods:
Lucas-Kanade
Farneback
---
81. Feature Detection
Feature detection identifies distinctive points or regions.
Examples:
Corners
Blobs
Keypoints
Common algorithms:
Harris Corner Detector
FAST
SIFT
ORB
---
82. SIFT
SIFT stands for:
```text
Scale-Invariant Feature Transform
```
It detects and describes local image features.
It is designed to provide robustness to:
Scale changes
Rotation
Some illumination/viewpoint changes
Typical stages:
Scale-space construction
Keypoint detection
Keypoint localization
Orientation assignment
Descriptor generation
---
83. ORB
ORB means:
```text
Oriented FAST and Rotated BRIEF
```
It is designed to be computationally efficient.
Advantages:
Fast
Suitable for real-time applications
Useful for feature matching
---
84. Feature Matching
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
Image stitching
Object recognition
Image registration
Tracking
---
85. Homography
Homography describes a projective transformation between two planes.
It is commonly used when matching points between images of the same planar surface.
Applications:
Panorama stitching
Document alignment
Perspective correction
---
86. Image Registration
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
Medical imaging
Satellite imagery
Change detection
---
87. Video Processing
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
FPS
Latency
Resolution
Model inference time
Hardware acceleration
---
88. Computer Vision Evaluation Metrics
Classification
Important metrics:
Accuracy
Precision
Recall
F1-score
ROC-AUC
PR-AUC
Accuracy
```text
Accuracy =
Correct Predictions
-------------------
Total Predictions
```
Accuracy can be misleading for imbalanced datasets.
---
89. Precision
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
90. Recall
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
91. F1 Score
```text
F1 =
2 × Precision × Recall
----------------------
Precision + Recall
```
F1 balances precision and recall.
---
92. Detection Metrics
Important metrics:
IoU
Precision
Recall
AP
mAP
AP
Average Precision summarizes the precision-recall relationship for a class.
mAP
Mean Average Precision averages AP across classes.
Depending on the benchmark, mAP may be reported at different IoU thresholds.
Always specify the evaluation convention.
---
93. Segmentation Metrics
Common metrics:
Pixel Accuracy
Percentage of correctly classified pixels.
IoU / Jaccard
```text
IoU = Intersection / Union
```
Dice Coefficient
```text
Dice =
2 × Intersection
-----------------
Prediction + Ground Truth
```
Dice is widely used in medical and segmentation tasks.
---
94. Confusion Matrix for Vision Classification
For binary classification:
```text
                 Actual
              Pos       Neg

Pred Pos       TP        FP
Pred Neg       FN        TN
```
Use it to understand which errors the model is making.
---
95. Class Imbalance in Computer Vision
Example:
```text
Normal images = 95%
Defect images = 5%
```
A model predicting "Normal" for every image could achieve 95% accuracy but be useless.
Solutions:
Data augmentation
Class weighting
Oversampling
Undersampling
Focal loss
Better evaluation metrics
---
96. Data Leakage in Computer Vision
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
Medical imaging
Face recognition
Human behavior analysis
Video datasets
---
97. Image Dataset Splitting
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
98. Overfitting in Computer Vision
Overfitting occurs when a model performs well on training data but poorly on unseen data.
Symptoms:
```text
Training accuracy → very high
Validation accuracy → significantly lower
```
Solutions:
More data
Data augmentation
Regularization
Dropout
Early stopping
Transfer learning
Reduce model complexity
---
99. Underfitting
Underfitting occurs when the model fails to learn the training patterns sufficiently.
Symptoms:
```text
Training performance → poor
Validation performance → poor
```
Possible solutions:
Increase model capacity
Improve features
Train longer
Reduce excessive regularization
Improve preprocessing
---
100. Batch Size, Epochs and Learning Rate
Batch Size
Number of samples processed before one parameter update.
Epoch
One complete pass through the training dataset.
Learning Rate
Controls how large parameter updates are during optimization.
These hyperparameters strongly affect training behavior.
---
101. CNN Training Workflow
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
102. Common Loss Functions
Binary Classification
Binary Cross Entropy:
```text
BCE
```
Multi-Class Classification
Categorical Cross Entropy is commonly used.
Multi-Label Classification
Binary cross entropy is commonly used independently across labels.
Object Detection
Detection models generally use combinations of classification, localization, and sometimes objectness losses.
Segmentation
Common losses:
Cross entropy
Dice loss
Binary cross entropy
Focal loss
Combined losses
---
103. Computer Vision Pipeline in Python
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
104. OpenCV
OpenCV is a widely used computer-vision library.
Important capabilities:
Image reading/writing
Video processing
Filtering
Thresholding
Edge detection
Morphology
Contours
Feature detection
Object tracking
Camera access
Common import:
```python
import cv2
```
---
105. NumPy in Computer Vision
Images are commonly represented as NumPy arrays.
Useful operations:
```python
image.shape
image.dtype
image.min()
image.max()
```
Array slicing is important for:
Cropping
ROI extraction
Channel manipulation
---
106. PyTorch / TensorFlow
Deep-learning frameworks commonly used for vision:
PyTorch
TensorFlow
Keras
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
107. Modern Computer Vision
Modern CV includes:
CNNs
Vision Transformers
Multimodal models
Self-supervised learning
Foundation models
Vision-language models
Diffusion models
---
108. Vision Transformers (ViT)
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
109. Vision-Language Models
Vision-language models combine visual and textual understanding.
Examples of tasks:
Image captioning
Visual question answering
Image-text retrieval
Visual reasoning
Multimodal assistants
Conceptually:
```text
Image + Text
     ↓
Multimodal Model
     ↓
Text / Classification / Reasoning
```
---
110. OCR
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
Tesseract
Cloud Vision APIs
Deep-learning OCR systems
Applications:
Invoice processing
ID document extraction
Purchase orders
Forms
Receipts
---
111. Pose Estimation
Pose estimation identifies human body keypoints.
Typical keypoints:
Nose
Shoulders
Elbows
Wrists
Hips
Knees
Ankles
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
MediaPipe
OpenPose
YOLO-based pose models
---
112. Action Recognition
Action recognition attempts to identify human activities from images or video.
Examples:
Walking
Running
Jumping
Sitting
Hand movements
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
LSTM
GRU
3D CNN
Transformers
---
113. Real-Time Computer Vision
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
FPS
Frames processed per second.
Latency
Time required to process one frame or request.
Throughput
Number of inputs processed per unit time.
A model with high accuracy but excessive latency may not be suitable for real-time deployment.
---
114. Model Optimization
For production CV systems:
Resize inputs appropriately
Use smaller architectures
Quantize models
Prune unnecessary weights where appropriate
Use batching where latency permits
Use GPU acceleration
Use ONNX/TensorRT where appropriate
Optimize preprocessing
Avoid unnecessary frame processing
---
115. Edge Deployment
Computer vision may run on:
Cloud GPU
Local server
Laptop
Mobile device
Embedded device
Edge accelerator
Edge inference can reduce:
Network latency
Bandwidth usage
Dependence on cloud connectivity
But hardware constraints become important.
---
116. Production Computer Vision Architecture
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
Model latency
Error rate
Data drift
Input quality
Prediction distribution
Hardware utilization
Model accuracy when labels become available
---
117. Computer Vision Project Best Practices
Data
Inspect class distribution
Remove corrupted images
Check duplicates
Verify labels
Detect leakage
Use representative samples
Preprocessing
Keep preprocessing consistent between training and inference.
Record image dimensions.
Normalize according to the model requirements.
Handle poor-quality images.
Training
Use validation data correctly.
Track metrics.
Save checkpoints.
Use early stopping when appropriate.
Track experiments.
Evaluation
Do not rely only on accuracy.
Use task-specific metrics.
Deployment
Measure:
Accuracy
Latency
FPS
Memory
CPU/GPU utilization
---
118. Common Computer Vision Mistakes
Mistake 1: Ignoring BGR vs RGB
OpenCV loads images in BGR.
Mistake 2: Randomly splitting video frames
Frames from the same video can be extremely similar.
Mistake 3: Using only accuracy
Especially dangerous with class imbalance.
Mistake 4: Data augmentation leakage
Do not let augmented versions of the same source image leak across train/test.
Mistake 5: Wrong preprocessing
Training and inference preprocessing must match.
Mistake 6: Ignoring image quality
Blur, lighting, occlusion and camera angle can strongly affect performance.
Mistake 7: Using a large model unnecessarily
For real-time systems, latency and hardware constraints matter.
---
119. End-to-End Computer Vision Project
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
120. Example: Human Behavior Detection Project
Suppose the objective is to detect a specific behavior from video.
Step 1 — Input
```text
Webcam / Video
```
Step 2 — Frame extraction
```text
Video → Frames
```
Step 3 — Person detection
Identify people in the frame.
Step 4 — Pose estimation
Extract body keypoints.
Step 5 — Feature engineering
Possible features:
Joint angles
Joint distances
Movement velocity
Temporal changes
Body-part trajectories
Step 6 — Classification
Classify the observed behavior.
```text
Features
   ↓
ML / Deep Learning Model
   ↓
Behavior
```
Step 7 — Evaluation
Use:
Precision
Recall
F1
Confusion matrix
Subject-level validation
Step 8 — Deployment
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
121. Interview-Level Questions
Basic
Q1. What is image processing?
Image processing manipulates digital images to enhance them, transform them, or extract useful information.
Q2. What is computer vision?
Computer vision enables machines to interpret and understand information from images and videos.
Q3. What is a pixel?
A pixel is the smallest addressable element of a digital image containing intensity or color information.
Q4. What is the difference between RGB and BGR?
RGB stores channels as Red-Green-Blue, while OpenCV commonly represents images as Blue-Green-Red.
Q5. Why convert an image to grayscale?
It reduces the representation from multiple color channels to one intensity channel, simplifying many processing tasks and reducing computation.
---
122. Intermediate Interview Questions
Q6. What is convolution?
Convolution applies a kernel over local image regions to calculate feature responses.
Q7. Why is Gaussian blur used before Canny?
It reduces noise so that the edge detector is less likely to detect noise as false edges.
Q8. What is thresholding?
Thresholding converts pixels into classes, commonly separating foreground from background according to intensity.
Q9. What is the difference between erosion and dilation?
Erosion shrinks foreground regions, while dilation expands them.
Q10. What is morphological opening?
Opening is erosion followed by dilation and is commonly used to remove small noise.
Q11. What is morphological closing?
Closing is dilation followed by erosion and is commonly used to fill small holes and gaps.
Q12. What is ROI?
ROI is a selected region of an image relevant to the task.
---
123. Advanced Interview Questions
Q13. Why are CNNs effective for image data?
CNNs exploit local spatial structure and learn hierarchical representations through convolutional filters.
Q14. What is padding?
Padding adds pixels around an input before convolution to control output dimensions and preserve border information.
Q15. What is stride?
Stride controls the step size with which a convolution kernel moves across the input.
Q16. What is transfer learning?
Transfer learning adapts representations learned from a pretrained model to a new task.
Q17. Detection vs segmentation?
Detection predicts object classes and bounding boxes; segmentation predicts pixel-level regions.
Q18. What is NMS?
Non-Maximum Suppression removes redundant overlapping detection boxes and keeps the most confident predictions.
Q19. What is IoU?
IoU measures overlap between predicted and reference regions using intersection divided by union.
Q20. Why can frame-level random splitting be problematic?
Neighboring frames from the same video are highly correlated, so random frame splitting can cause leakage and overly optimistic evaluation.
---
124. Scenario-Based Interview Questions
Q21. Your model has 98% accuracy but poor business performance. Why?
Possible reasons:
Class imbalance
Wrong evaluation metric
Data leakage
Poor minority-class recall
Distribution shift
Incorrect labels
I would inspect the confusion matrix, per-class metrics, validation strategy, and data distribution.
Q22. Your model works in the lab but fails in production. What do you investigate?
I would investigate:
Lighting differences
Camera differences
Resolution changes
Background changes
Occlusion
Data distribution shift
Preprocessing mismatch
Label quality
Model latency
Hardware constraints
Q23. How would you make a CV model real-time?
I would profile the entire pipeline rather than only the model. Then optimize image resolution, model architecture, preprocessing, inference runtime and hardware acceleration while measuring FPS and latency.
Q24. How would you reduce false positives?
Depending on the task:
Tune decision thresholds
Improve training data
Add hard-negative examples
Improve preprocessing
Use stronger validation
Tune NMS for detection
Analyze false-positive samples
Q25. How would you handle insufficient training images?
I would consider:
Transfer learning
Data augmentation
Better labeling
Collection of additional representative data
Cross-validation where appropriate
Regularization
Synthetic data if justified
---
125. Must-Know Formula Sheet
Pixel values
```text
8-bit image → 0 to 255
```
Number of values
```text
2^n
```
Standardization
```text
z = (x - μ) / σ
```
Accuracy
```text
(TP + TN) / (TP + TN + FP + FN)
```
Precision
```text
TP / (TP + FP)
```
Recall
```text
TP / (TP + FN)
```
F1
```text
2PR / (P + R)
```
IoU
```text
Intersection / Union
```
Dice
```text
2 × Intersection / (Prediction + Ground Truth)
```
---
126. Practical Python/OpenCV Cheat Sheet
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
127. Recommended Learning Sequence
Beginner
Pixels
Image dimensions
Channels
RGB/BGR
Grayscale
Resolution
Bit depth
Image loading
Resizing
Cropping
Normalization
Intermediate
Histograms
Contrast enhancement
Filtering
Gaussian blur
Median filtering
Thresholding
Otsu
Canny
Sobel
Morphology
Contours
Geometric transformations
Advanced
Convolution
CNNs
Transfer learning
Object detection
NMS
IoU
Segmentation
Tracking
Optical flow
Feature matching
Pose estimation
Video analytics
Real-time inference
Expert / AI Engineer Level
Vision Transformers
Vision-language models
Multimodal AI
Model optimization
Quantization
Edge inference
Production monitoring
Data drift
Model serving
Distributed inference
Experiment tracking
End-to-end CV system design
---
128. What You Should Be Able to Explain in an Interview
By the end of this topic, you should be able to explain:
How an image is represented in memory.
Difference between RGB, BGR, grayscale and HSV.
Why preprocessing is required.
Difference between normalization and standardization.
Why resizing is required.
How convolution works.
What kernels and feature maps are.
Difference between Gaussian, median and bilateral filtering.
How Canny edge detection works.
Difference between erosion, dilation, opening and closing.
Thresholding and Otsu thresholding.
What contours are.
Classification vs detection vs segmentation.
IoU and NMS.
CNN architecture.
Padding and stride.
Pooling.
Transfer learning and fine-tuning.
Data augmentation.
Overfitting and class imbalance.
Detection and segmentation metrics.
Object tracking.
Pose estimation.
Real-time computer vision.
Production deployment challenges.
Data leakage in video datasets.
How to design an end-to-end CV project.
---
129. Final Mental Model
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
130. Interview Preparation Strategy
For each concept, prepare four levels:
Level 1 — Definition
Be able to define the concept in 1–2 sentences.
Level 2 — Intuition
Explain why it exists and what problem it solves.
Level 3 — Technical Depth
Explain:
Formula
Algorithm
Parameters
Advantages
Limitations
Level 4 — Real Project
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
