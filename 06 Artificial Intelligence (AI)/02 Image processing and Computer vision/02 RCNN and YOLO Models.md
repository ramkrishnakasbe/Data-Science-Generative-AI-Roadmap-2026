# CNN and Non-CNN Computer Vision Models — Interview Preparation Notes

## 1. Overview

Computer Vision models can broadly be understood as:

```text
Computer Vision Models
│
├── Non-CNN / Classical Vision
│   ├── HOG
│   ├── SIFT
│   ├── SURF
│   ├── ORB
│   ├── Template Matching
│   └── Classical ML + Handcrafted Features
│
└── CNN-Based Deep Learning
    ├── R-CNN
    ├── Fast R-CNN
    ├── Faster R-CNN
    ├── Mask R-CNN
    └── YOLO
```

The important interview distinction is:

```text
Non-CNN
→ Handcrafted features + classical algorithms + ML

CNN
→ Automatically learns visual features from images
```

---

# PART 1 — NON-CNN / CLASSICAL COMPUTER VISION

## 2. What Does "Non-CNN" Mean?

Before deep learning became dominant, Computer Vision systems commonly used manually designed features.

Typical pipeline:

```text
Image
  ↓
Preprocessing
  ↓
Feature Extraction
  ↓
Feature Descriptor
  ↓
Machine Learning Model
  ↓
Prediction
```

Example:

```text
Image
 ↓
HOG Features
 ↓
SVM
 ↓
Person / Not Person
```

The major limitation is that the engineer must decide which features are useful.

---

# 3. HOG — Histogram of Oriented Gradients

HOG represents an image using the distribution of edge directions.

It is especially useful for detecting objects such as pedestrians.

Basic process:

```text
Image
 ↓
Grayscale
 ↓
Gradient Calculation
 ↓
Magnitude + Orientation
 ↓
Cells
 ↓
Orientation Histograms
 ↓
Block Normalization
 ↓
HOG Feature Vector
 ↓
Classifier
```

### Core idea

HOG focuses on:

```text
Shape
Edges
Gradient Directions
Local Appearance
```

It does not learn features automatically like a CNN.

### Typical classifier

```text
HOG
 ↓
SVM
 ↓
Classification
```

### Interview Question

**Q: Why was HOG useful for pedestrian detection?**

**Answer:**

HOG captures local edge and gradient structures that describe the shape of a human body. Pedestrian silhouettes contain relatively stable gradient patterns, making HOG effective when combined with classifiers such as SVM.

---

# 4. SIFT — Scale-Invariant Feature Transform

SIFT detects distinctive local features that are relatively robust to:

```text
Scale
Rotation
Moderate Illumination Changes
Local Affine Changes
```

Pipeline:

```text
Image
 ↓
Scale-Space Construction
 ↓
Keypoint Detection
 ↓
Keypoint Localization
 ↓
Orientation Assignment
 ↓
Descriptor Generation
```

The output contains:

```text
Keypoints
+
Descriptors
```

SIFT is useful for:

```text
Image Matching
Object Recognition
Image Registration
Panorama Stitching
Feature Matching
```

### Interview Question

**Q: Why is SIFT scale invariant?**

**Answer:**

SIFT detects keypoints across multiple image scales using a scale-space representation. This allows the same visual feature to be identified even when the object appears larger or smaller.

---

# 5. SURF — Speeded-Up Robust Features

SURF was designed as a faster alternative to SIFT.

It uses concepts such as:

```text
Hessian-based Interest Point Detection
Integral Images
Local Feature Descriptors
```

General pipeline:

```text
Image
 ↓
Keypoint Detection
 ↓
Orientation
 ↓
Descriptor
 ↓
Feature Matching
```

### SIFT vs SURF

| Feature            | SIFT            | SURF                      |
| ------------------ | --------------- | ------------------------- |
| Main goal          | Robust features | Faster feature extraction |
| Scale invariant    | Yes             | Yes                       |
| Rotation invariant | Yes             | Yes                       |
| Speed              | Slower          | Faster historically       |
| Descriptor         | Detailed        | More compact              |

---

# 6. ORB — Oriented FAST and Rotated BRIEF

ORB combines:

```text
FAST
+
BRIEF
```

with orientation handling.

```text
ORB
│
├── FAST → Keypoint Detection
│
└── BRIEF → Feature Description
```

ORB is popular because it is:

```text
Fast
Memory Efficient
Suitable for Real-Time Applications
```

Applications:

```text
Feature Matching
Image Registration
Visual Odometry
Object Recognition
Real-Time Vision
```

### Interview Question

**Q: Why is ORB commonly preferred in real-time applications?**

**Answer:**

ORB uses computationally efficient feature detection and binary descriptors, making it significantly faster and more memory efficient than traditional descriptors such as SIFT.

---

# 7. SIFT vs ORB

| Feature           | SIFT                           | ORB           |
| ----------------- | ------------------------------ | ------------- |
| Descriptor        | Floating-point                 | Binary        |
| Speed             | Relatively slower              | Faster        |
| Matching          | More computationally expensive | Efficient     |
| Scale handling    | Strong                         | Good          |
| Rotation handling | Strong                         | Good          |
| Real-time         | Less suitable                  | More suitable |
| Memory            | Higher                         | Lower         |

---

# 8. Classical Feature + ML Pipeline

A common traditional Computer Vision pipeline:

```text
Image
 ↓
Resize / Normalize
 ↓
Feature Extraction
 ↓
HOG / SIFT / ORB
 ↓
Feature Vector
 ↓
SVM / Random Forest / KNN
 ↓
Prediction
```

Example:

```text
Pedestrian Image
      ↓
HOG
      ↓
Feature Vector
      ↓
SVM
      ↓
Person / Not Person
```

---

# 9. Limitations of Classical Vision

Classical approaches require substantial feature engineering.

Problems include:

```text
Handcrafted Features
Poor Generalization
Sensitivity to Complex Backgrounds
Difficulty Handling Large Variations
Limited Representation Learning
Feature Engineering Effort
```

CNNs addressed many of these limitations by learning hierarchical features directly from data.

---

# PART 2 — CNN-BASED COMPUTER VISION

# 10. CNN-Based Vision Pipeline

A CNN learns visual representations automatically.

```text
Image
 ↓
Convolution
 ↓
Feature Maps
 ↓
Activation
 ↓
Pooling / Downsampling
 ↓
Deeper Features
 ↓
Prediction
```

Feature hierarchy:

```text
Early Layers
→ Edges

Middle Layers
→ Textures / Shapes

Deep Layers
→ Object Parts / Semantic Features
```

---

# 11. Object Detection

Object detection answers two questions:

```text
1. What object is present?
2. Where is the object?
```

Output generally contains:

```text
Class
+
Bounding Box
+
Confidence Score
```

Example:

```text
Image
 ↓
Detector
 ↓
Person → [x1, y1, x2, y2] → 0.96
Car    → [x1, y1, x2, y2] → 0.91
Dog    → [x1, y1, x2, y2] → 0.87
```

---

# 12. R-CNN

R-CNN stands for:

**Regions with Convolutional Neural Networks.**

It was an important early CNN-based object detection architecture.

### Architecture

```text
Image
 ↓
Region Proposals
 ↓
~2000 Candidate Regions
 ↓
CNN Feature Extraction
 ↓
SVM Classifier
 ↓
Bounding Box Regression
```

The original R-CNN used **Selective Search** to generate region proposals.

---

# 13. How R-CNN Works

### Step 1 — Region Proposal

Selective Search generates candidate regions.

```text
Image
 ↓
Selective Search
 ↓
Region Proposals
```

### Step 2 — CNN

Each region is resized and passed independently through a CNN.

```text
Region
 ↓
CNN
 ↓
Feature Vector
```

### Step 3 — Classification

The extracted features are passed to class-specific classifiers.

### Step 4 — Bounding Box Regression

The predicted bounding boxes are refined.

---

# 14. R-CNN Problems

R-CNN is conceptually important but computationally expensive.

Main problems:

```text
~2000 regions per image
        ↓
CNN runs separately on each region
        ↓
Very Slow
```

It also involved multiple training stages.

This led to Fast R-CNN.

---

# 15. Fast R-CNN

Fast R-CNN improves R-CNN by running the CNN **once for the entire image**.

Architecture:

```text
Image
 ↓
CNN
 ↓
Feature Map
 ↓
Region Proposals
 ↓
ROI Pooling
 ↓
Fully Connected Layers
 ↓
├── Classification
└── Bounding Box Regression
```

---

# 16. Why Fast R-CNN Is Faster

### R-CNN

```text
Image
 ↓
Region 1 → CNN
Region 2 → CNN
Region 3 → CNN
...
Region 2000 → CNN
```

### Fast R-CNN

```text
Image
 ↓
One CNN
 ↓
Shared Feature Map
 ↓
All Regions
```

The expensive convolutional computation is shared.

---

# 17. ROI Pooling

ROI means:

**Region of Interest**

ROI Pooling converts regions of different sizes into a fixed-size representation.

Example:

```text
Feature Map
     ↓
ROI
     ↓
ROI Pooling
     ↓
Fixed Size Feature
```

This allows the detection head to process different candidate regions using a consistent input size.

---

# 18. Fast R-CNN Limitations

Fast R-CNN still relied on external region proposal methods such as Selective Search.

Therefore:

```text
CNN → Fast
Region Proposal → Slow
```

This led to Faster R-CNN.

---

# 19. Faster R-CNN

Faster R-CNN introduced the:

**Region Proposal Network (RPN)**

The architecture becomes:

```text
Image
 ↓
Backbone CNN
 ↓
Feature Map
 ↓
Region Proposal Network
 ↓
Region Proposals
 ↓
ROI Pooling / ROI Align
 ↓
Detection Head
 ↓
Class + Bounding Box
```

The major improvement is that region proposals are generated using a neural network rather than an external algorithm such as Selective Search.

---

# 20. Region Proposal Network — RPN

RPN operates on CNN feature maps.

Conceptually:

```text
Feature Map
     ↓
Sliding Window
     ↓
Anchors
     ↓
Objectness Score
+
Bounding Box Regression
     ↓
Region Proposals
```

RPN predicts:

```text
Is there an object?
+
How should the box be adjusted?
```

---

# 21. Anchors

Traditional Faster R-CNN uses predefined reference boxes called anchors.

Different:

```text
Scales
+
Aspect Ratios
```

are used.

Example:

```text
Anchor 1 → Small + Square
Anchor 2 → Large + Square
Anchor 3 → Wide
Anchor 4 → Tall
```

The network predicts offsets to transform anchors into better bounding boxes.

---

# 22. ROI Align

ROI Align improves upon ROI Pooling by avoiding coarse coordinate quantization.

This is particularly important for pixel-level tasks such as Mask R-CNN.

Conceptually:

```text
ROI
 ↓
Precise Sampling
 ↓
Interpolation
 ↓
Fixed Feature Representation
```

### Interview Question

**Q: ROI Pooling vs ROI Align?**

**Answer:**

ROI Pooling quantizes ROI coordinates, which can introduce spatial misalignment. ROI Align avoids this quantization and uses interpolation to preserve more precise spatial information. This is especially important for segmentation tasks.

---

# 23. Faster R-CNN — Complete Flow

```text
                Input Image
                     ↓
               Backbone CNN
                     ↓
                Feature Map
                     ↓
                    RPN
                     ↓
             Region Proposals
                     ↓
                 ROI Align
                     ↓
             Detection Head
                /        \
               ↓          ↓
          Classification   Box
                           Regression
```

---

# 24. Advantages of Faster R-CNN

```text
High Detection Accuracy
Strong Localization
Good for Small Objects
Flexible Backbone
Powerful Two-Stage Architecture
```

Common use cases:

```text
Medical Imaging
Industrial Inspection
High-Accuracy Detection
Complex Object Detection
```

---

# 25. Limitations of Faster R-CNN

```text
More Computationally Expensive
Slower Than YOLO
Complex Architecture
Higher Inference Latency
```

Therefore:

```text
Accuracy Priority
→ Faster R-CNN

Real-Time Priority
→ YOLO
```

This is a general trade-off, not an absolute rule; specific versions and hardware can change the comparison.

---

# 26. Mask R-CNN

Mask R-CNN extends Faster R-CNN to perform:

```text
Object Detection
+
Instance Segmentation
```

Architecture:

```text
Image
 ↓
Backbone
 ↓
RPN
 ↓
ROI Align
 ↓
 ┌───────────────┬───────────────┐
 ↓               ↓               ↓
Classification    Box Regression  Mask Branch
```

The third branch predicts a pixel-level mask for each detected object.

---

# 27. What Is Instance Segmentation?

Suppose an image contains:

```text
Person 1
Person 2
Person 3
```

Semantic segmentation:

```text
All persons → Person
```

Instance segmentation:

```text
Person 1 → Separate Mask
Person 2 → Separate Mask
Person 3 → Separate Mask
```

Mask R-CNN performs instance-level segmentation.

---

# 28. Mask R-CNN Mask Branch

For each detected ROI:

```text
ROI
 ↓
Mask Head
 ↓
Per-Pixel Prediction
 ↓
Object Mask
```

So each detected object gets:

```text
Class
+
Bounding Box
+
Confidence
+
Segmentation Mask
```

---

# 29. Why Mask R-CNN Uses ROI Align

Segmentation requires precise spatial alignment.

If ROI coordinates are heavily quantized:

```text
Object Boundary
      ↓
Spatial Misalignment
      ↓
Poor Mask
```

ROI Align preserves more accurate spatial information.

---

# 30. Mask R-CNN Loss

Mask R-CNN uses multiple learning objectives.

Conceptually:

```text
Total Loss
=
Classification Loss
+
Bounding Box Loss
+
Mask Loss
```

This allows the model to learn:

```text
What is the object?
Where is the object?
Which pixels belong to it?
```

---

# 31. Mask R-CNN Advantages

```text
High-Quality Instance Segmentation
Strong Object Detection
Accurate Localization
Useful for Complex Scenes
```

Applications:

```text
Medical Imaging
Robotics
Industrial Inspection
Autonomous Systems
Object-Level Image Analysis
```

---

# 32. Mask R-CNN Limitations

```text
Computationally Expensive
Higher Latency
More Memory
More Complex Than One-Stage Detectors
```

---

# 33. YOLO

YOLO stands for:

**You Only Look Once.**

YOLO is designed around fast object detection.

The central idea is to perform object detection as a largely **single-stage prediction problem** rather than first generating region proposals and then classifying them separately.

Simplified:

```text
Image
 ↓
CNN / Modern Backbone
 ↓
Feature Extraction
 ↓
Detection Head
 ↓
Bounding Boxes
+
Classes
+
Confidence
```

---

# 34. Why YOLO Is Fast

Two-stage detector:

```text
Image
 ↓
Region Proposal
 ↓
Classification
 ↓
Box Refinement
```

YOLO-style one-stage detector:

```text
Image
 ↓
Feature Extraction
 ↓
Detection Prediction
```

This avoids a separate proposal-generation stage.

---

# 35. YOLO Detection Output

For each prediction, the model estimates information such as:

```text
Bounding Box
Confidence
Class Probabilities
```

Conceptually:

```text
[x, y, width, height]
+
objectness / confidence
+
class scores
```

The exact output representation differs across YOLO generations.

---

# 36. YOLO Evolution

For interviews, understand the progression rather than memorizing every implementation detail.

```text
YOLOv1
 ↓
YOLOv2
 ↓
YOLOv3
 ↓
YOLOv4
 ↓
YOLOv5
 ↓
YOLOv6
 ↓
YOLOv7
 ↓
YOLOv8
 ↓
Newer YOLO-family implementations
```

Different YOLO versions and implementations introduced improvements in:

```text
Backbone
Neck
Detection Head
Loss Functions
Training Strategy
Data Augmentation
Anchor Design
Anchor-Free Detection
Speed
Accuracy
Deployment
```

---

# 37. YOLO Architecture — High Level

Modern YOLO-style architectures can be understood through:

```text
Input
 ↓
Backbone
 ↓
Neck
 ↓
Detection Head
 ↓
Predictions
```

### Backbone

Extracts visual features.

```text
Image
 ↓
Feature Maps
```

### Neck

Combines features from different scales.

```text
Low-Level Features
+
High-Level Features
 ↓
Multi-Scale Features
```

### Head

Produces final predictions.

```text
Class
+
Bounding Box
+
Confidence
```

---

# 38. Why Multi-Scale Detection Matters

Objects can have different sizes.

```text
Large Object
Medium Object
Small Object
```

A detector needs features at different resolutions.

```text
High Resolution Feature Map
→ Small Objects

Medium Resolution
→ Medium Objects

Low Resolution
→ Large Objects
```

Feature Pyramid Network-style designs and related multi-scale feature aggregation are therefore important concepts in modern detection.

---

# 39. YOLO Advantages

```text
Fast Inference
Real-Time Applications
Single-Stage Detection
Good Accuracy-Speed Trade-off
Simple Deployment
```

Applications:

```text
Surveillance
Traffic Detection
Retail Analytics
Industrial Inspection
People Counting
Autonomous Systems
Video Analytics
```

---

# 40. YOLO Limitations

Historically, one-stage detectors could struggle more with certain small-object and dense-object scenarios compared with high-accuracy two-stage methods.

Other considerations:

```text
Small Object Detection Can Be Challenging
Dense Scenes Can Be Difficult
Accuracy Depends on Model Version
Latency Depends on Model Size and Hardware
```

Modern YOLO variants have significantly improved these limitations.

---

# 41. R-CNN Family vs YOLO

| Feature          | R-CNN            | Fast R-CNN       | Faster R-CNN          | Mask R-CNN            | YOLO              |
| ---------------- | ---------------- | ---------------- | --------------------- | --------------------- | ----------------- |
| Type             | Two-stage        | Two-stage        | Two-stage             | Two-stage             | One-stage         |
| Region Proposals | Selective Search | Selective Search | RPN                   | RPN                   | No separate RPN   |
| Detection        | Yes              | Yes              | Yes                   | Yes                   | Yes               |
| Segmentation     | No               | No               | No                    | Yes                   | Detection-focused |
| Speed            | Very Slow        | Faster           | Faster                | Relatively Slow       | Fast              |
| Accuracy         | Good             | Good             | High                  | High                  | High              |
| Real-Time        | No               | Limited          | Usually less suitable | Usually less suitable | Strong            |
| Main Idea        | CNN per region   | Shared CNN       | Learned proposals     | Detection + masks     | Direct detection  |

---

# 42. R-CNN Evolution — Interview Flow

Memorize this sequence:

```text
R-CNN
 │
 ├── Selective Search
 ├── CNN per Region
 └── SVM
      ↓
Fast R-CNN
 │
 ├── CNN Once
 ├── Shared Feature Map
 └── ROI Pooling
      ↓
Faster R-CNN
 │
 ├── CNN Once
 ├── RPN
 └── ROI Pooling / ROI Align
      ↓
Mask R-CNN
 │
 ├── Faster R-CNN
 ├── ROI Align
 └── Mask Branch
```

The key improvement is:

```text
R-CNN
→ Expensive region-wise CNN computation

Fast R-CNN
→ Shared CNN computation

Faster R-CNN
→ Learned region proposals

Mask R-CNN
→ Detection + Instance Segmentation
```

---

# 43. Two-Stage vs One-Stage Detectors

## Two-Stage

```text
Image
 ↓
Proposal Generation
 ↓
Object Classification
 ↓
Bounding Box Refinement
```

Examples:

```text
Faster R-CNN
Mask R-CNN
```

Advantages:

```text
Strong Localization
High Accuracy
Good Complex-Scene Performance
```

Disadvantages:

```text
More Computation
Higher Latency
More Complex
```

---

# 44. One-Stage

```text
Image
 ↓
Detection Network
 ↓
Predictions
```

Examples:

```text
YOLO
SSD
RetinaNet
```

Advantages:

```text
Fast
Simple Inference Pipeline
Suitable for Real-Time Applications
```

---

# 45. Object Detection Metrics

## IoU

Intersection over Union:

```text
IoU =
Area of Intersection
--------------------
Area of Union
```

Higher IoU:

```text
Better Bounding Box Overlap
```

---

# 46. Precision

```text
Precision =
TP
---------
TP + FP
```

High precision means:

```text
Few False Positives
```

Useful when false detections are costly.

---

# 47. Recall

```text
Recall =
TP
---------
TP + FN
```

High recall means:

```text
Few Missed Objects
```

Useful when missing an object is costly.

---

# 48. mAP

mAP stands for:

**mean Average Precision**

It evaluates object detection performance across classes and confidence thresholds according to a specified evaluation protocol.

Conceptually:

```text
Predictions
 ↓
Precision-Recall Curve
 ↓
Average Precision
 ↓
Mean Across Classes
 ↓
mAP
```

Important interview distinction:

```text
AP → Average Precision for a class

mAP → Mean AP across classes
```

---

# 49. NMS — Non-Maximum Suppression

A detector may produce several overlapping boxes for one object.

Example:

```text
Object
 ↓
Box A → 0.95
Box B → 0.89
Box C → 0.71
```

NMS:

```text
Keep highest-confidence box
        ↓
Calculate IoU
        ↓
Suppress highly overlapping boxes
        ↓
Repeat
```

---

# 50. Confidence Threshold vs IoU Threshold

### Confidence Threshold

Controls:

```text
How confident must the model be
before keeping a prediction?
```

Increasing it generally:

```text
↓ False Positives
↓ Recall
```

though the exact effect depends on the model/data.

### NMS IoU Threshold

Controls:

```text
How much overlap is allowed
between retained predictions?
```

A lower NMS IoU threshold generally suppresses overlapping boxes more aggressively.

---

# 51. Anchor-Based vs Anchor-Free Detection

### Anchor-Based

Uses predefined reference boxes.

Examples historically include many versions of:

```text
Faster R-CNN
YOLO
SSD
```

### Anchor-Free

Predicts object locations without predefined anchor boxes.

The design simplifies the detection formulation.

Modern detectors increasingly use anchor-free approaches.

---

# 52. Small Object Detection

Small objects are challenging because they occupy few pixels.

Possible approaches:

```text
Higher Input Resolution
Multi-Scale Features
Feature Pyramid Networks
Better Data Augmentation
Small-Object-Specific Training
Appropriate Detection Head
```

Interview answer:

> I would first inspect the object-size distribution, feature-map resolution, annotation quality, and recall for small objects. Then I would evaluate higher input resolution, multi-scale features, suitable augmentation, and an architecture optimized for small-object detection.

---

# 53. Class Imbalance in Detection

Example:

```text
Person → 100,000 instances
Helmet → 2,000 instances
```

Potential approaches:

```text
Data Collection
Oversampling
Targeted Augmentation
Class-Aware Sampling
Focal Loss
Hard Example Mining
Threshold Tuning
```

---

# 54. Focal Loss

Focal Loss was introduced to address extreme class imbalance in dense object detection.

It reduces the relative contribution of easy examples and focuses training more on difficult examples.

Conceptually:

```text
Easy Example
→ Lower Weight

Hard Example
→ Higher Relative Weight
```

This is particularly associated with RetinaNet.

---

# 55. Detection Loss

A modern object detector may optimize multiple components:

```text
Total Loss
=
Classification Loss
+
Localization / Box Loss
+
Objectness / Confidence Loss
```

The exact formulation depends on the architecture.

---

# 56. When Would You Choose Faster R-CNN?

Choose Faster R-CNN when:

```text
Accuracy is more important than latency
Objects are difficult to localize
High-quality detection is required
Real-time inference is not the primary constraint
```

Example:

```text
Medical Image Analysis
Industrial Inspection
Research Applications
```

---

# 57. When Would You Choose YOLO?

Choose YOLO when:

```text
Real-Time Inference is Important
Low Latency is Required
Video Processing is Required
Deployment Efficiency Matters
```

Example:

```text
Traffic Monitoring
CCTV Analytics
People Counting
Industrial Cameras
Retail Analytics
```

---

# 58. When Would You Choose Mask R-CNN?

Choose Mask R-CNN when the requirement is:

```text
Object Detection
+
Individual Object Masks
```

Example:

```text
Detect every person
+
Generate a separate mask for each person
```

Applications:

```text
Medical Segmentation
Robotics
Instance-Level Analysis
Industrial Inspection
```

---

# 59. Model Selection Interview Scenario

### Question

**You need to detect people from a live CCTV camera at 30 FPS. Which model would you consider?**

### Interview Answer

I would start with a real-time one-stage detector such as a suitable YOLO variant. I would benchmark the selected model on the target hardware because FPS depends on input resolution, model size, preprocessing, post-processing, and hardware. I would evaluate both detection quality and latency rather than selecting the model based only on benchmark numbers.

---

# 60. Scenario — High Accuracy Required

### Question

**You need extremely accurate object localization for an industrial inspection system. Real-time inference is not mandatory.**

Possible starting point:

```text
Faster R-CNN
```

Then compare against suitable modern detectors using:

```text
mAP
Recall
Precision
IoU
Latency
False Positive Rate
False Negative Rate
```

---

# 61. Scenario — Detection + Segmentation

### Question

**You need to detect every object and generate a separate mask for every object.**

Answer:

```text
Mask R-CNN
```

because it extends the Faster R-CNN detection framework with an additional mask prediction branch.

---

# 62. Scenario — Classical Vision vs CNN

### Question

**You have a controlled industrial environment where objects have fixed shapes and lighting is stable. Would you always use a CNN?**

No.

A classical approach may be sufficient if:

```text
Environment is Controlled
Object Appearance is Stable
Background is Predictable
Rules are Well Defined
Data is Limited
Latency Requirements Favor Simple Algorithms
```

Possible solution:

```text
Thresholding
+
Morphology
+
Contours
+
Shape Features
```

or:

```text
HOG / ORB
+
SVM
```

This can be simpler, faster, and easier to maintain.

---

# 63. CNN vs Classical Computer Vision

| Aspect              | Classical CV      | CNN                         |
| ------------------- | ----------------- | --------------------------- |
| Feature Engineering | High              | Low                         |
| Feature Learning    | Manual            | Automatic                   |
| Data Requirement    | Often Lower       | Usually Higher              |
| Compute             | Often Lower       | Usually Higher              |
| Generalization      | Problem dependent | Strong with sufficient data |
| Interpretability    | Often easier      | More complex                |
| Complex Images      | Limited           | Strong                      |
| Real-Time           | Often excellent   | Depends on model/hardware   |

---

# 64. Most Important Interview Questions

## Non-CNN

1. What is HOG?
2. How does HOG work?
3. Why is HOG useful for pedestrian detection?
4. What is SIFT?
5. Why is SIFT scale invariant?
6. What is ORB?
7. Why is ORB faster than SIFT?
8. SIFT vs ORB?
9. What are keypoints and descriptors?
10. When would you use classical CV instead of CNN?

## R-CNN

11. What is R-CNN?
12. How does R-CNN work?
13. Why is R-CNN slow?
14. What is Selective Search?
15. Why was Fast R-CNN introduced?

## Fast R-CNN

16. How does Fast R-CNN improve R-CNN?
17. What is ROI Pooling?
18. Why does Fast R-CNN still have a bottleneck?

## Faster R-CNN

19. What is Faster R-CNN?
20. What is RPN?
21. What are anchors?
22. How does RPN work?
23. Faster R-CNN vs Fast R-CNN?
24. Why is Faster R-CNN called a two-stage detector?

## Mask R-CNN

25. What is Mask R-CNN?
26. Faster R-CNN vs Mask R-CNN?
27. Why does Mask R-CNN use ROI Align?
28. What is instance segmentation?
29. Detection vs semantic segmentation vs instance segmentation?

## YOLO

30. What is YOLO?
31. Why is YOLO fast?
32. YOLO vs Faster R-CNN?
33. What are one-stage and two-stage detectors?
34. What is the role of backbone, neck, and head?
35. Why are multi-scale features important?
36. What is NMS?
37. What is IoU?
38. What is mAP?
39. What is anchor-free detection?
40. How would you improve small-object detection?

---

# 65. High-Frequency Comparison Questions

### Q1. R-CNN vs Fast R-CNN

```text
R-CNN
→ CNN separately for each region

Fast R-CNN
→ CNN once for entire image
→ ROI Pooling
```

---

### Q2. Fast R-CNN vs Faster R-CNN

```text
Fast R-CNN
→ External region proposals

Faster R-CNN
→ RPN generates region proposals
```

---

### Q3. Faster R-CNN vs Mask R-CNN

```text
Faster R-CNN
→ Detection

Mask R-CNN
→ Detection + Instance Segmentation
```

---

### Q4. Faster R-CNN vs YOLO

```text
Faster R-CNN
→ Two-stage
→ Accuracy-oriented
→ Usually higher latency

YOLO
→ One-stage
→ Speed-oriented
→ Real-time friendly
```

---

### Q5. Semantic Segmentation vs Instance Segmentation

```text
Semantic:
Every pixel gets a class.

Instance:
Every individual object gets a separate mask.
```

---

# 66. Complete Model Selection Cheat Sheet

```text
Simple / Controlled Problem
        ↓
Classical CV
        ↓
HOG + SVM
ORB / SIFT
Contours
Thresholding


Object Detection
        ↓
 ┌───────────────┐
 ↓               ↓
Speed          Accuracy
 ↓               ↓
YOLO        Faster R-CNN


Detection
+
Instance Masks
        ↓
Mask R-CNN
```

---

# 67. Final Interview Mental Model

```text
                 COMPUTER VISION
                       │
        ┌──────────────┴──────────────┐
        ↓                             ↓
 Classical / Non-CNN                CNN
        │                             │
        ├── HOG                       │
        ├── SIFT                      │
        ├── SURF                      │
        └── ORB                       │
                                      ↓
                              Object Detection
                                      │
                    ┌─────────────────┴────────────────┐
                    ↓                                  ↓
               Two-Stage                            One-Stage
                    │                                  │
             ┌──────┴──────┐                          │
             ↓             ↓                          ↓
          Faster          Mask                      YOLO
          R-CNN           R-CNN
             │             │
        Detection      Detection
                         +
                    Instance Mask
```

## One-Line Revision

```text
HOG       → Shape/gradient features + classical ML
SIFT      → Robust local keypoints + descriptors
ORB       → Fast keypoints + binary descriptors
R-CNN     → Region proposals + CNN per region
Fast R-CNN → Shared CNN + ROI Pooling
Faster R-CNN → RPN + detection
Mask R-CNN → Faster R-CNN + instance masks
YOLO      → Fast one-stage object detection
```
