# Level 1: Fundamentals of Digital Image Processing

Welcome to **Level 1** of the Computer Vision & Image Processing Masterclass. This guide covers image processing concepts from beginner foundations to advanced mathematical principles, complete with practical Python code snippets.

---

## 📌 Table of Contents
1. [1. Digital Image Representation & Color Spaces](#1-digital-image-representation--color-spaces)
2. [2. Point Operations & Intensity Transformations](#2-point-operations--intensity-transformations)
3. [3. Histogram Processing & Contrast Enhancement](#3-histogram-processing--contrast-enhancement)
4. [4. Spatial Filtering & Image Enhancement](#4-spatial-filtering--image-enhancement)
5. [5. Frequency Domain Processing](#5-frequency-domain-processing)
6. [6. Image Restoration & Noise Models](#6-image-restoration--noise-models)
7. [7. Geometric Transformations & Image Registration](#7-geometric-transformations--image-registration)
8. [8. Morphological Image Processing](#8-morphological-image-processing)
9. [❓ Deep-Dive Interview Questions & Answers](#-deep-dive-interview-questions--answers)

---

## 1. Digital Image Representation & Color Spaces

### 1.1 Sampling and Quantization
* **Sampling:** Digitizing spatial coordinates $(x, y)$. Determines spatial resolution (e.g., $1920 	imes 1080$).
* **Quantization:** Digitizing amplitude/intensity values $I(x,y)$. Determines tonal resolution (e.g., 8-bit depth $= 256$ intensity levels $[0-255]$).
* **Nyquist-Shannon Sampling Theorem in 2D:** The sampling frequency must be at least twice the maximum spatial frequency present in the image to prevent **aliasing**.

```python
import cv2
import numpy as np

# Downsampling (Spatial Reduction) & Quantization (Bit-depth Reduction)
img = cv2.imread('input.jpg', cv2.IMREAD_GRAYSCALE)
downsampled = cv2.resize(img, (img.shape[1] // 2, img.shape[0] // 2), interpolation=cv2.INTER_AREA)
quantized_4bit = (img // 16) * 16  # Reduce 8-bit (256 levels) to 4-bit (16 levels)
```

### 1.2 Color Models & Spaces
* **RGB (Red, Green, Blue):** Additive color space used in digital displays. Channels are highly correlated.
* **HSV / HSL (Hue, Saturation, Value / Lightness):**
  * **Hue ($H$):** Dominant wavelength / color type ($0^\circ-360^\circ$).
  * **Saturation ($S$):** Purity / color richness ($0-100\%$).
  * **Value ($V$):** Brightness ($0-100\%$).
  * *Use Case:* Color-based segmentation (e.g., green screen removal) under varying lighting.
* **YCbCr / YUV:**
  * **$Y$:** Luminance (brightness).
  * **$Cb, Cr$:** Chrominance (blue-difference, red-difference).
  * *Use Case:* JPEG / MPEG video compression (exploits human visual system's lower sensitivity to color detail vs. brightness).
* **CIE $L^*a^*b^*$:** Perceptually uniform color space. Euclidean distance $\Delta E$ directly corresponds to human visual perception of color difference.

```python
# Color Space Transformations in OpenCV
bgr_img = cv2.imread('input.jpg')
hsv_img = cv2.cvtColor(bgr_img, cv2.COLOR_BGR2HSV)
lab_img = cv2.cvtColor(bgr_img, cv2.COLOR_BGR2LAB)

# Color-based Masking in HSV (Extracting Red Region)
lower_red = np.array([0, 120, 70])
upper_red = np.array([10, 255, 255])
red_mask = cv2.inRange(hsv_img, lower_red, upper_red)
```

---

## 2. Point Operations & Intensity Transformations

Point operations modify pixel values independently based solely on their current value: $s = T(r)$.

### 2.1 Common Transformations
* **Image Negative:** $s = L - 1 - r$ (enhances white/grey detail in dark backgrounds).
* **Log Transformation:** $s = c \cdot \log(1 + r)$ (expands dark pixel values, compresses bright values; useful for dynamic range compression in Fourier spectra).
* **Power-Law (Gamma Correction):** $s = c \cdot r^\gamma$
  * $\gamma < 1$: Expands dark regions (brightens image).
  * $\gamma > 1$: Expands bright regions (darkens image).

```python
# Gamma Correction Implementation
def gamma_correction(image, gamma=1.0):
    inv_gamma = 1.0 / gamma
    table = np.array([((i / 255.0) ** inv_gamma) * 255 for i in np.arange(0, 256)]).astype("uint8")
    return cv2.LUT(image, table)

brightened = gamma_correction(img, gamma=0.5) # Gamma < 1
```

---

## 3. Histogram Processing & Contrast Enhancement

### 3.1 Histogram Equalization (HE)
Transforms image intensity values using the Cumulative Distribution Function (CDF) so that the output histogram is approximately uniform, maximizing global contrast.

$$	ext{CDF}(k) = \sum_{j=0}^{k} p_r(r_j), \quad s_k = (L - 1) \cdot 	ext{CDF}(k)$$

### 3.2 Adaptive Histogram Equalization & CLAHE
Global HE over-amplifies noise in homogeneous areas and distorts regions with localized brightness variations.
* **CLAHE (Contrast Limited Adaptive Histogram Equalization):**
  1. Divides image into contextual regions ($8 	imes 8$ tiles).
  2. Computes local histogram per tile.
  3. Clips histogram at a threshold (e.g., clipLimit=2.0) to limit noise amplification; redistributes clipped pixels.
  4. Uses bilinear interpolation to stitch tile boundaries seamlessly.

```python
# CLAHE Implementation
clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8, 8))
clahe_img = clahe.apply(img)
```

---

## 4. Spatial Filtering & Image Enhancement

Spatial filtering involves moving a mask/kernel $h(m,n)$ across an image $f(x,y)$.

### 4.1 Linear Filtering (Convolution vs Correlation)
* **2D Cross-Correlation:** $g(x,y) = \sum_{m} \sum_{n} f(x+m, y+n) h(m,n)$
* **2D Convolution:** Kernel is rotated $180^\circ$: $g(x,y) = \sum_{m} \sum_{n} f(x-m, y-n) h(m,n)$
* **Gaussian Blur:** Isotropic spatial smoothing kernel $G(x,y) = rac{1}{2\pi\sigma^2} e^{-rac{x^2+y^2}{2\sigma^2}}$.

### 4.2 Non-Linear Edge-Preserving Filters
* **Median Filter:** Replaces target pixel with the median of neighboring pixels. Highly effective against **impulse (salt-and-pepper) noise**.
* **Bilateral Filter:** Edge-preserving smoothing combining spatial distance and range intensity difference:

$$I^{	ext{filtered}}(p) = rac{1}{W_p} \sum_{q \in S} I(q) \cdot g_{\sigma_s}(\|p - q\|) \cdot g_{\sigma_r}(|I(p) - I(q)|)$$

```python
# Smoothing Operations
gaussian = cv2.GaussianBlur(img, (5, 5), sigmaX=1.0)
median = cv2.medianBlur(img, 5) # Excellent for impulse noise
bilateral = cv2.bilateralFilter(img, d=9, sigmaColor=75, sigmaSpace=75) # Edge-preserving
```

---

## 5. Frequency Domain Processing

By taking the Discrete Fourier Transform (DFT), spatial details are mapped to spatial frequencies.

### 5.1 2D Discrete Fourier Transform (DFT)
$$F(u,v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x,y) e^{-j2\pi \left(rac{ux}{M} + rac{vy}{N}ight)}$$

* **Low Spatial Frequencies:** Smooth regions, homogeneous areas, general shape (center of shifted spectrum).
* **High Spatial Frequencies:** Edges, noise, fine details, sharp intensity transitions (outer regions of spectrum).

### 5.2 Frequency Domain Filtering Steps
1. Compute 2D DFT of image $f(x,y) 	o F(u,v)$.
2. Shift zero-frequency component to center.
3. Multiply element-wise by Filter Transfer Function $H(u,v)$: $G(u,v) = F(u,v) \cdot H(u,v)$.
4. Inverse shift and Inverse DFT back to spatial domain.

```python
# Frequency Domain Low-Pass Filtering
dft = np.fft.fft2(img)
dft_shift = np.fft.fftshift(dft)

# Create Low-Pass Filter Mask
rows, cols = img.shape
crow, ccol = rows // 2, cols // 2
mask = np.zeros((rows, cols), np.uint8)
r = 30 # Cutoff radius
cv2.circle(mask, (ccol, crow), r, 1, thickness=-1)

# Apply Mask & Inverse DFT
fshift = dft_shift * mask
f_ishift = np.fft.ifftshift(fshift)
img_back = np.abs(np.fft.ifft2(f_ishift))
```

---

## 6. Image Restoration & Noise Models

### 6.1 Common Noise Distributions
* **Gaussian Noise:** Additive white noise originating from sensor heating/electronic circuits. Removed via Gaussian/Mean filtering.
* **Salt-and-Pepper (Impulse) Noise:** Random black/white pixels from transmission errors or faulty pixels. Removed via Median filtering.
* **Speckle Noise:** Multiplicative noise common in Radar/Ultrasound imaging.

### 6.2 Image Degradation & Restoration
Degradation Model: $g(x,y) = f(x,y) * h(x,y) + \eta(x,y)$ where $h$ is Point Spread Function (PSF) and $\eta$ is noise.
* **Wiener Deconvolution:** Minimizes mean square error between original and restored image under degradation:

$$H_{	ext{Wiener}}(u,v) = rac{H^*(u,v)}{|H(u,v)|^2 + rac{S_\eta(u,v)}{S_f(u,v)}}$$

---

## 7. Geometric Transformations & Image Registration

Geometric operations alter spatial relationships between pixels.

### 7.1 Affine vs Projective Transformations
* **Affine Transformation (6 Degrees of Freedom):** Preserves parallel lines (translation, rotation, scale, shear).
  $$egin{bmatrix} x' \ y' \end{bmatrix} = egin{bmatrix} a_1 & a_2 \ a_3 & a_4 \end{bmatrix} egin{bmatrix} x \ y \end{bmatrix} + egin{bmatrix} t_x \ t_y \end{bmatrix}$$
* **Homography / Projective (8 Degrees of Freedom):** Preserves straight lines, but parallel lines intersect.

```python
# Affine & Perspective Transformations
# 1. Rotation by 45 degrees
M_rot = cv2.getRotationMatrix2D((cols/2, rows/2), 45, scale=1.0)
rotated = cv2.warpAffine(img, M_rot, (cols, rows))

# 2. Homography / Perspective Transform
pts1 = np.float32([[56, 65], [368, 52], [28, 387], [389, 390]])
pts2 = np.float32([[0, 0], [300, 0], [0, 300], [300, 300]])
H = cv2.getPerspectiveTransform(pts1, pts2)
warped = cv2.warpPerspective(img, H, (300, 300))
```

---

## 8. Morphological Image Processing

Morphological operations modify binary/grayscale shapes based on a **Structuring Element (SE)**.

### 8.1 Fundamental Operations
* **Erosion ($A \ominus B$):** Removes boundary pixels of foreground objects (shrinks shapes).
* **Dilation ($A \oplus B$):** Adds boundary pixels to foreground objects (expands shapes).

### 8.2 Compound Operations
* **Opening ($A \circ B = (A \ominus B) \oplus B$):** Erosion followed by dilation. Removes small noise artifacts without altering object size.
* **Closing ($A ullet B = (A \oplus B) \ominus B$):** Dilation followed by erosion. Fills small holes and bridges narrow gaps.
* **Morphological Gradient ($Dilation - Erosion$):** Extracts object boundaries.

```python
# Morphological Filtering
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))
opened = cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel) # Remove noise
closed = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel) # Fill holes
gradient = cv2.morphologyEx(img, cv2.MORPH_GRADIENT, kernel) # Edge outline
```

---

## ❓ Deep-Dive Interview Questions & Answers

### Q1: Why is a Gaussian filter separable, and what computational benefit does it offer?
**Answer:** A 2D Gaussian kernel $G(x,y) = rac{1}{2\pi\sigma^2} e^{-rac{x^2+y^2}{2\sigma^2}}$ can be factorized into two 1D Gaussian kernels: $G(x,y) = G_1(x) \cdot G_2(y)$.
* **Complexity without separability:** 2D convolution with an $N 	imes N$ kernel requires $O(W \cdot H \cdot N^2)$ scalar multiplications.
* **Complexity with separability:** Applying a 1D horizontal pass followed by a 1D vertical pass requires $O(W \cdot H \cdot 2N)$ scalar operations.
* **Impact:** For a $15 	imes 15$ kernel, separable convolution reduces computation by $\sim 7.5	imes$.

---

### Q2: How does the Bilateral Filter differ from a traditional Gaussian Blur?
**Answer:**
* **Gaussian Blur** weights pixels strictly by spatial distance $d(p, q) = \|p - q\|$:
  $$W_s = \exp\left(-rac{\|p - q\|^2}{2\sigma_s^2}ight)$$
  This blurs across object edges indiscriminately.
* **Bilateral Filter** incorporates a second range kernel based on pixel intensity difference $r(p, q) = |I(p) - I(q)|$:
  $$W_r = \exp\left(-rac{|I(p) - I(q)|^2}{2\sigma_r^2}ight)$$
  When the filter encounters an edge ($|I(p) - I(q)|$ is large), the range weight drops to near zero, preventing pixels across the boundary from influencing the target pixel and preserving crisp edges.

---

### Q3: What causes aliasing during image downsampling, and how do you mathematically mitigate it?
**Answer:**
* **Cause:** Downsampling decreases spatial sampling frequency $f_s$. According to the Nyquist theorem, if $f_s < 2 f_{\max}$ (where $f_{\max}$ is the highest spatial frequency component in the image), high-frequency signals fold into lower frequency bands, creating false patterns/moiré artifacts.
* **Mitigation:** Apply a spatial **Low-Pass Filter (Gaussian Blur)** prior to downsampling to attenuate spatial frequencies above $rac{f_s}{2}$.

---

### Q4: Why does standard Histogram Equalization perform poorly on natural outdoor scenes with mixed lighting?
**Answer:** Standard HE computes a global Cumulative Distribution Function (CDF). In scenes with contrasting lighting (e.g., bright sky and dark foreground shadows), global HE stretches intensities based on the overall distribution, causing over-saturation in bright regions and noise amplification in dark areas. 
* **Solution:** Use **CLAHE** (Contrast Limited Adaptive Histogram Equalization), which operates on local sub-tiles and caps histogram counts to prevent excessive local contrast expansion.

---
*Created for Data Science, ML & AI Technical Interview Preparation.*
