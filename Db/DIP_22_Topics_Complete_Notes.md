# COMPREHENSIVE NOTES ON DIGITAL IMAGE PROCESSING
## (22 Key Topics with Formulas)

**Course Level:** B.Sc. Forensic Science / Digital Forensics  
**Academic Standards:** College-approved curriculum, based on IEEE and international standards  
**Date:** December 19, 2025

---

## PART 1: SPATIAL DOMAIN METHODS

### Topic 1: Spatial Domain Method

**Definition & Overview:**
Spatial domain processing directly manipulates pixel values in the image plane. Operations are performed on the original pixel coordinates (x, y) where the image is represented as a 2D function f(x, y).

**Key Characteristics:**
- Direct manipulation of pixel values
- No transformation to other domains required
- Computationally less intensive than frequency domain methods
- Faster execution for real-time applications
- Used in forensic image enhancement and fingerprint analysis

**Process:**
For any spatial domain operation on image f(x, y), the output image g(x, y) is given by:

\[g(x, y) = T[f(x, y)]\]

Where:
- T is the transformation operator
- f(x, y) is the input pixel at coordinates (x, y)
- g(x, y) is the output pixel value

**Applications in Forensics:**
- Enhancement of fingerprint images before pattern classification
- Latent fingerprint visualization
- Iris and facial feature enhancement
- Document image enhancement in criminal records

**Advantages:**
- Immediate results without complex computations
- Suitable for real-time biometric systems
- Lower memory requirements
- Easy to implement in hardware

---

### Topic 2: Linear Transformation

**Definition:**
A linear transformation in spatial domain is characterized by a transformation that preserves linearity. If T is a linear operator and a, b are constants, then:

\[T(af_1 + bf_2) = aT(f_1) + bT(f_2)\]

**Linear Spatial Filtering Formula:**
The fundamental equation for linear spatial filtering (convolution) is:

\[g(x, y) = \sum_{s=-a}^{a} \sum_{t=-b}^{b} w(s, t) \cdot f(x+s, y+t)\]

Where:
- g(x, y) = output filtered image at pixel (x, y)
- w(s, t) = filter kernel or mask with dimensions (2a+1) × (2b+1)
- f(x+s, y+t) = input image pixel values
- s, t = coordinates within the kernel window

**Common Linear Kernels:**

**Mean Filter (Averaging):**
\[w(i, j) = \frac{1}{m \times n}\]
for all elements in m × n kernel

**Gaussian Kernel:**
\[G(x, y) = \frac{1}{2\pi\sigma^2} \exp\left(-\frac{x^2 + y^2}{2\sigma^2}\right)\]

Where σ is the standard deviation controlling blur intensity

**Sobel Filter (Gradient):**
\[G_x = \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix}, \quad G_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}\]

Gradient magnitude:
\[G = \sqrt{G_x^2 + G_y^2}\]

**Applications:**
- Fingerprint enhancement and ridge detection
- Image smoothing to remove noise
- Edge detection in forensic images

---

### Topic 3: Point Operation

**Definition:**
Point operations transform each pixel independently using a transformation function T that depends only on the intensity value of that pixel:

\[s = T(r)\]

Where:
- r = input pixel intensity (0 to L-1)
- s = output pixel intensity (0 to L-1)
- L = number of gray levels (typically 256 for 8-bit images)

**Characteristics:**
- One-to-one mapping between input and output intensities
- No spatial neighborhood consideration
- Histogram transformation function
- Used for contrast adjustment and intensity scaling

**General Formula:**
For a pixel at position (x, y):
\[g(x, y) = T(f(x, y))\]

The transformation is completely defined by the intensity mapping.

---

### Topic 4: Digital Negative

**Definition:**
Digital negative (image inversion) reverses all pixel intensity values. Dark areas become bright and bright areas become dark.

**Formula:**
\[s = (L - 1) - r\]

Where:
- s = output pixel intensity
- r = input pixel intensity
- L = maximum intensity level (L = 256 for 8-bit images)

**Mathematical Expression:**
\[g(x, y) = 255 - f(x, y)\]

(for 8-bit grayscale images)

**Complete Formula:**
\[T(r) = L - 1 - r = 255 - r\]

**Transformation Function Graph:**
The graph is a straight line with negative slope passing through:
- Point (0, 255)
- Point (255, 0)

**Applications:**
- Medical image enhancement (X-rays often displayed as negatives)
- Photograph analysis where negative reveals hidden details
- Scanning historical documents to improve visibility
- Forensic enhancement of old crime scene photographs

**Discrete Implementation:**
For 8-bit image:
```
For each pixel f(x, y):
  g(x, y) = 255 - f(x, y)
```

**Important Notes:**
- Reversible operation: applying twice returns original image
- Preserves all image data
- No information loss
- Useful when original image has poor contrast or unusual intensity distribution

---

### Topic 5: Non-linear Transformation

**Definition:**
Non-linear transformations do not follow the principle of superposition. If T is non-linear:

\[T(af_1 + bf_2) \neq aT(f_1) + bT(f_2)\]

These are intensity transformations where the output depends non-linearly on input.

**General Form:**
\[s = T(r)\]

Where the transformation function T is non-linear.

**Characteristics:**
- Complex relationship between input and output
- Different slope at different intensity levels
- Better for handling images with non-uniform intensity distribution
- Common in contrast enhancement

**Applications:**
- Fingerprint image enhancement
- Iris recognition preprocessing
- X-ray and medical image enhancement
- Correction for non-linear sensor response

---

### Topic 6: Square Function

**Definition:**
A non-linear transformation that squares the pixel intensity values.

**Formula:**
\[s = r^2\]

Where:
- s = output pixel intensity
- r = input pixel intensity

**Normalized Formula (to keep values in valid range):**
\[s = c \cdot r^2\]

Where c is a scaling constant:
\[c = \frac{L-1}{(L-1)^2} = \frac{1}{L-1}\]

**For 8-bit images:**
\[s = \frac{r^2}{255}\]

**Full Transformation:**
\[g(x, y) = \frac{[f(x, y)]^2}{255}\]

**Characteristics:**
- Darkens the image (brightens dark areas less than bright areas)
- Reduces dynamic range in bright regions
- Amplifies contrast in dark regions
- Affects histogram by concentrating values toward lower levels

**Applications:**
- Reducing noise in bright regions
- Compression of high intensity values
- Forensic image analysis where detail in dark areas is important

---

### Topic 7: Square Root Function

**Definition:**
A non-linear transformation that applies square root to pixel intensities. This is the inverse of square function.

**Formula:**
\[s = \sqrt{r}\]

**Scaling Formula (to keep values in valid range):**
\[s = (L-1) \cdot \sqrt{\frac{r}{L-1}}\]

**For 8-bit images:**
\[s = 255 \cdot \sqrt{\frac{r}{255}} = \sqrt{255 \cdot r}\]

**Normalized Version:**
\[g(x, y) = \sqrt{255 \cdot f(x, y)}\]

**Characteristics:**
- Brightens the image
- Expands dark intensity values more than bright values
- Increases visibility in dark regions
- Opposite effect of square function

**Effects on Histogram:**
- Spreads out lower intensity values
- Compresses higher intensity values
- Increases contrast in dark areas

**Applications:**
- Enhancement of underexposed photographs
- Brightening of latent fingerprints
- Recovery of detail in dark forensic images
- X-ray image enhancement

---

### Topic 8: Logarithmic Function

**Definition:**
Logarithmic transformation compresses the dynamic range of images with large variations in pixel intensities. Mathematically expands small values and compresses large values.

**Formula:**
\[s = c \cdot \log(1 + r)\]

Where:
- c = scaling constant (typically 255/log(L))
- r = input pixel intensity
- L = maximum intensity level

**Standard Formula:**
\[s = c \log(1 + r)\]

Where:
\[c = \frac{L-1}{\log(1 + L-1)}\]

**For 8-bit images:**
\[s = \frac{255}{\log(256)} \cdot \log(1 + r) \approx 35.05 \log(1 + r)\]

**Complete Transformation:**
\[g(x, y) = c \log(1 + f(x, y))\]

**Why use (1 + r)?**
- log(0) is undefined, so add 1 to avoid mathematical error
- Ensures domain includes zero intensity

**Key Properties:**
1. Maps narrow range of dark values to broader range
2. Maps broad range of bright values to narrow range
3. Creates subjectively pleasing contrast
4. Reduces dynamic range significantly

**Transformation Characteristics:**
- Non-linear curve with decreasing slope
- Slow growth for large r values
- Steep growth for small r values

**Applications in Forensics:**
- Enhancement of radiography images (X-rays, CT scans)
- Fourier spectrum visualization (magnitude spectrum)
- Correction of overexposed photographs
- Latent fingerprint enhancement
- Revealing details in high contrast crime scene images
- Medical forensics and autopsy photography

**Inverse Operation:**
\[r = e^{s/c} - 1\]

Where e is the base of natural logarithm.

---

### Topic 9: Exponential Function

**Definition:**
Exponential transformation is the dual of logarithmic transformation. It expands the dynamic range by compressing small values and expanding large values.

**Formula:**
\[s = c(e^r - 1)\]

Or:
\[s = c(b^r - 1)\]

Where:
- c = scaling constant
- b = base (commonly e or 10)
- r = input pixel intensity

**Standard Formula:**
\[s = c[e^{kr} - 1]\]

Where:
\[c = \frac{L-1}{e^k(L-1) - 1}\]

**For 8-bit images with natural exponential:**
\[s = \frac{255}{e^{255} - 1}(e^r - 1)\]

**Practical Form:**
\[g(x, y) = c[e^{f(x,y)} - 1]\]

**Characteristics:**
- Expands bright pixel values more than dark
- Increases contrast in bright regions
- Opposite of logarithmic transformation
- Used for underexposed images

**Properties:**
- Steep increase for larger values
- Gentle increase for smaller values
- Rapidly expanding output values

**Applications:**
- Brightening underexposed photographs
- Enhancing details in dark regions of surveillance images
- Forensic enhancement of low-contrast fingerprints
- Recovery of details in dark forensic photographs

**Inverse Operation:**
\[r = \frac{1}{k}\ln\left(\frac{s}{c} + 1\right)\]

---

### Topic 10: Power Function (Gamma Correction)

**Definition:**
Power-law transformation applies a power operation to pixel intensities. Also known as gamma correction or gamma adjustment.

**Formula:**
\[s = c \cdot r^\gamma\]

Where:
- s = output intensity
- r = input intensity
- γ (gamma) = power parameter
- c = scaling constant

**Normalized Formula:**
\[s = (L-1) \left(\frac{r}{L-1}\right)^\gamma\]

**For 8-bit images:**
\[s = 255 \left(\frac{r}{255}\right)^\gamma\]

**Complete Transformation:**
\[g(x, y) = c \left[f(x, y)\right]^\gamma\]

**Value of Gamma and Effects:**

| γ value | Effect | Use |
|---------|--------|-----|
| γ < 1 | Brightens image (expansion) | Dark image enhancement |
| γ = 1 | Linear, no change | Baseline |
| γ > 1 | Darkens image (compression) | Bright image enhancement |
| γ ≈ 0.4 | Significant brightening | Very dark forensic images |
| γ ≈ 2.2 | Moderate darkening | Display correction |

**Mathematical Explanation:**
- For 0 < r < 1: r^γ with γ < 1 gives larger values (brightening)
- For 0 < r < 1: r^γ with γ > 1 gives smaller values (darkening)

**Applications:**
- Monitor and display calibration (standard γ = 2.2)
- Correction for non-linear response of photographic film
- Fingerprint image enhancement
- Medical image preprocessing
- Surveillance footage enhancement
- Correction of sensor-induced non-linearities

**Common Gamma Values in Forensics:**
- γ = 0.4 to 0.6: Enhancement of very dark images
- γ = 1.0: No correction
- γ = 2.0 to 2.5: Display gamma correction

**Verification Formula:**
To verify gamma correction was applied with parameter γ₁, apply γ₂ = 1/γ₁ to recover original.

---

### Topic 11: Gamma Correlation

**Definition:**
Gamma correlation refers to the correlation between the gamma-corrected values of two images or the correlation coefficient of pixel intensities after gamma correction.

**Formula - Pearson Correlation Coefficient After Gamma Correction:**
\[r_\gamma = \frac{\sum_{i=1}^{n}(s_i - \bar{s})(t_i - \bar{t})}{\sqrt{\sum_{i=1}^{n}(s_i - \bar{s})^2} \sqrt{\sum_{i=1}^{n}(t_i - \bar{t})^2}}\]

Where:
- s_i = gamma-corrected pixel values of first image: \(s_i = c \cdot r_i^\gamma\)
- t_i = gamma-corrected pixel values of second image
- \(\bar{s}\) = mean of gamma-corrected values
- \(\bar{t}\) = mean of second set of gamma-corrected values
- n = number of pixels

**Alternative Form:**
\[\rho_\gamma = \frac{E[(f_1^\gamma - \mu_1)(f_2^\gamma - \mu_2)]}{\sigma_1 \sigma_2}\]

Where:
- E = expectation operator
- \(f_i^\gamma\) = gamma-corrected intensities
- μ = mean
- σ = standard deviation

**Application in Biometrics:**
- Matching gamma-corrected fingerprint images
- Comparing iris codes from different imaging conditions
- Assessing template quality after gamma correction
- Correlation-based matching in forensic identification

**Range:**
- -1 ≤ r_γ ≤ +1
- 1 = perfect positive correlation
- 0 = no correlation
- -1 = perfect negative correlation

**Use in Image Matching:**
Higher gamma correlation indicates better similarity between gamma-corrected templates.

---

### Topic 12: Piecewise Slicing

**Definition:**
Piecewise slicing (also called piecewise linear transformation or piecewise linear stretching) uses multiple line segments to define the transformation function. Different slopes for different intensity ranges.

**General Formula:**
For transformation defined by n points: (r₀, s₀), (r₁, s₁), ..., (rₙ, sₙ)

For input r in range [r_i, r_(i+1)]:

\[s = s_i + \frac{s_{i+1} - s_i}{r_{i+1} - r_i}(r - r_i)\]

Where:
- r_i, r_(i+1) = input intensity boundaries
- s_i, s_(i+1) = output intensity boundaries
- Slope = \(\frac{s_{i+1} - s_i}{r_{i+1} - r_i}\)

**Transformation Function:**
The complete transformation is defined piecewise:

\[T(r) = \begin{cases}
s_0 + m_0(r - r_0), & r_0 \leq r \leq r_1 \\
s_1 + m_1(r - r_1), & r_1 \leq r \leq r_2 \\
\vdots \\
s_{n-1} + m_{n-1}(r - r_{n-1}), & r_{n-1} \leq r \leq r_n
\end{cases}\]

Where m_i is the slope of the ith segment.

**Key Parameters:**
- Slope in segment i: \(m_i = \frac{\Delta s}{\Delta r}\)
- Higher slope = stronger enhancement in that range
- Lower slope = compression in that range

**Applications:**
- Selective contrast stretching in specific intensity ranges
- Forensic image enhancement targeting specific features
- Fingerprint ridge enhancement
- Highlighted specific anatomical regions in medical images

**Advantages:**
- Flexible control over different intensity ranges
- Can preserve detail in important regions
- More sophisticated than single-line stretching
- Allows multiple enhancement strategies simultaneously

---

### Topic 13: Contrast Stretching

**Definition:**
Contrast stretching (also called normalize or dynamic range adjustment) spreads narrow range of pixel intensities in input image to full utilizable range in output image.

**Basic Formula:**
\[s = \frac{L-1}{r_{max} - r_{min}}(r - r_{min})\]

Where:
- s = output pixel intensity
- r = input pixel intensity
- r_min = minimum intensity in input image
- r_max = maximum intensity in input image
- L = maximum output intensity level (256 for 8-bit)

**Expanded Formula:**
\[g(x, y) = \frac{(L-1)[f(x, y) - f_{min}]}{f_{max} - f_{min}}\]

Where:
- f(x, y) = input pixel at position (x, y)
- f_min = minimum pixel value in entire image
- f_max = maximum pixel value in entire image
- g(x, y) = output pixel value

**For 8-bit Images:**
\[g(x, y) = \frac{255[f(x, y) - f_{min}]}{f_{max} - f_{min}}\]

**Two-Point Stretching Formula:**
If choosing specific control points (r1, s1) and (r2, s2):

For r ≤ r1:
\[s = \frac{s_1}{r_1} \cdot r\]

For r1 < r < r2:
\[s = s_1 + \frac{s_2 - s_1}{r_2 - r_1}(r - r_1)\]

For r ≥ r2:
\[s = s_2 + \frac{L-1 - s_2}{L-1 - r_2}(r - r_2)\]

**Enhancement Factor:**
\[E = \frac{s_{max} - s_{min}}{r_{max} - r_{min}} = \frac{255}{r_{max} - r_{min}}\]

Higher E means stronger contrast enhancement.

**Histogram After Stretching:**
- Input histogram confined to [r_min, r_max]
- Output histogram spreads to full [0, 255] range
- Increases separation between intensity groups

**Forensic Applications:**
- Fingerprint contrast enhancement before matching
- Latent fingerprint visualization
- Crime scene photography enhancement
- Improvement of low-contrast facial recognition images
- X-ray and radiographic image enhancement

**Linear Stretching Example:**
Input: pixel values range from 50 to 200
Output: stretched to full 0-255 range

Transformation: \[s = \frac{255(r-50)}{200-50} = 1.7(r-50)\]

**Saturation Stretching:**
Ignore extreme outliers (top and bottom 2% of histogram):

\[s = \frac{(L-1)[r - r_{2\%}]}{r_{98\%} - r_{2\%}}\]

---

### Topic 14: Gray Level Slicing

**Definition:**
Gray level slicing (also called intensity slicing or level slicing) highlights pixels within a specific intensity range while suppressing all other pixels.

**Formula - Bright Slicing (Highlight specific range):**
\[g(x, y) = \begin{cases}
L-1 & \text{if } a \leq f(x, y) \leq b \\
0 & \text{otherwise}
\end{cases}\]

Or with intermediate values:
\[g(x, y) = \begin{cases}
L-1 & \text{if } a \leq f(x, y) \leq b \\
c & \text{otherwise (background)}
\end{cases}\]

Where:
- a = lower bound of slicing range
- b = upper bound of slicing range
- L = maximum intensity level (256)
- c = background intensity value

**Formula - With Linear Transformation Outside Range:**
\[g(x, y) = \begin{cases}
L-1 & \text{if } a \leq f(x, y) \leq b \\
m \cdot f(x, y) + n & \text{otherwise}
\end{cases}\]

Where m and n define the background transformation.

**Transformation Function:**
The piecewise slicing function:

\[T(r) = \begin{cases}
L-1 & \text{for } a \leq r \leq b \\
c & \text{for all other } r
\end{cases}\]

**Multi-Level Slicing:**
For n different ranges:

\[g(x, y) = \begin{cases}
L-1 & \text{if } r \in [a_1, b_1] \cup [a_2, b_2] \cup ... \cup [a_n, b_n] \\
0 & \text{otherwise}
\end{cases}\]

**Forensic Applications:**
- Highlighting specific anatomical features in medical imagery
- Isolating specific intensity patterns in fingerprints
- Detecting anomalies in X-ray images
- Segmentation of different tissue types in radiography
- Highlighting blood stains at specific intensity levels in crime photos

**Characteristics:**
- Binary-like output (high or low values)
- Preserves fine details within sliced range
- Suppresses irrelevant information
- Often combined with other enhancements

**Example - Crime Scene:**
Enhance blood stains (typically 120-180 intensity range):
\[g(x, y) = \begin{cases}
255 & \text{if } 120 \leq f(x, y) \leq 180 \\
0 & \text{otherwise}
\end{cases}\]

---

### Topic 15: Bit Plane Slicing

**Definition:**
Bit plane slicing decomposes an image into individual bit planes, where each plane represents one bit position in the binary representation of pixel intensities.

**Bit Position Formula:**
For each pixel intensity r (0 to 255), expressed as 8-bit binary:

\[r = \sum_{k=0}^{7} b_k \cdot 2^k\]

Where:
- b_k = k-th bit (0 or 1)
- k = bit position (0 to 7)
- 2^k = positional weight

**Extraction of Bit Plane k:**
\[B_k(x, y) = \left\lfloor \frac{f(x, y)}{2^k} \right\rfloor \bmod 2\]

Or using bitwise operations:
\[B_k(x, y) = (f(x, y) >> k) \& 1\]

Where:
- >> = right bit shift operation
- & = bitwise AND operation
- 1 = mask for single bit

**Pixel Reconstruction from Bit Planes:**
To reconstruct original pixel from bit planes:

\[f(x, y) = \sum_{k=0}^{7} B_k(x, y) \cdot 2^k\]

**Example - 8-Bit Decomposition:**
For pixel value r = 167:
Binary: 10100111

Bit planes (from MSB to LSB):
- Bit 7 (MSB): 1
- Bit 6: 0
- Bit 5: 1
- Bit 4: 0
- Bit 3: 0
- Bit 2: 1
- Bit 1: 1
- Bit 0 (LSB): 1

**Significance of Bit Planes:**
- Higher bit planes (6, 7): Contain major image features and overall structure
- Lower bit planes (0, 1, 2): Contain fine details and noise

**Energy Distribution:**
- MSB (Bit 7) carries most information (1/2 of total pixel values)
- Bit k carries 1/2^(k+1) of information
- LSB carries minimal information

**Applications in Forensics:**
- Noise identification and removal
- Detection of image manipulation
- Steganalysis (hidden data detection)
- Image authentication and watermarking
- Forensic compression analysis
- Detection of forged or altered documents

**Bit Plane Images:**
Each bit plane can be viewed as a binary image where:
- 1 (white pixel) = bit position set
- 0 (black pixel) = bit position not set

**Feature Analysis:**
High bit planes show:
- Main image structure
- Primary features and objects
- Overall shape and contours

Low bit planes show:
- Subtle textures
- Noise patterns
- Fine details
- Potential compression artifacts

---

## PART 2: FREQUENCY DOMAIN METHODS

### Topic 16: Frequency Domain

**Definition:**
The frequency domain is an alternative representation of an image where pixel intensities are decomposed into spatial frequency components using the Fourier Transform. Instead of spatial coordinates (x, y), the domain is represented by frequency coordinates (u, v).

**Fourier Transform - 2D Discrete Fourier Transform (DFT):**

\[F(u, v) = \frac{1}{M \times N} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) e^{-j2\pi(ux/M + vy/N)}\]

Where:
- F(u, v) = frequency domain representation (complex number)
- f(x, y) = spatial domain pixel value at (x, y)
- M × N = image dimensions
- u, v = frequency coordinates (0 to M-1, 0 to N-1)
- j = imaginary unit (\(\sqrt{-1}\))
- e^(-j·) = complex exponential (Euler's formula)

**Inverse DFT - Reconstruction:**

\[f(x, y) = \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u, v) e^{j2\pi(ux/M + vy/N)}\]

**Complex Representation:**
\[F(u, v) = R(u, v) + jI(u, v)\]

Where:
- R(u, v) = real part (cosine components)
- I(u, v) = imaginary part (sine components)

**Magnitude Spectrum:**
\[|F(u, v)| = \sqrt{R^2(u, v) + I^2(u, v)}\]

Represents strength of frequency component (u, v)

**Phase Spectrum:**
\[\phi(u, v) = \arctan\left(\frac{I(u, v)}{R(u, v)}\right)\]

Represents phase information of frequency component.

**Power Spectrum:**
\[P(u, v) = |F(u, v)|^2 = R^2(u, v) + I^2(u, v)\]

**Key Frequency Components:**

1. **Zero Frequency (DC Component):**
   - F(0, 0) represents the average intensity
   - Largest component for most natural images
   - Located at center after frequency shifting

2. **Low Frequencies:**
   - Clustered near center (u, v) ≈ (0, 0)
   - Represent smooth regions, gradual changes
   - Contain overall image structure
   - Important for image recognition

3. **High Frequencies:**
   - Located away from center
   - Represent edges, fine details, noise
   - Correspond to rapid intensity changes
   - Contain sharp transitions

**Frequency Shifting - Centering Zero Frequency:**

To move DC component to center for visualization:

\[G(u, v) = F(u - M/2, v - N/2) \cdot (-1)^{x+y}\]

Or using exponential:
\[g(x, y) = f(x, y) \cdot e^{j\pi(x+y)}\]

**Fast Fourier Transform (FFT):**
Efficient algorithm to compute DFT with complexity O(N log N) instead of O(N²)

**Advantages of Frequency Domain Processing:**
- Filtering becomes multiplication instead of convolution
- Global operations easily implemented
- Intuitive understanding of image characteristics
- Efficient computation using FFT
- Direct relationship to filter design theory

**Forensic Applications:**
- Removal of periodic noise (compression artifacts)
- Detection of image manipulation patterns
- Analysis of JPEG compression artifacts
- Fingerprint ridge frequency analysis
- Iris texture frequency characteristics
- Steganalysis and hidden information detection

**Convolution Theorem:**
Critical relationship between domains:

Spatial domain convolution ↔ Frequency domain multiplication

\[f(x, y) * h(x, y) \leftrightarrow F(u, v) \cdot H(u, v)\]

Where * denotes convolution.

**Important Properties:**
1. **Linearity:** \[a \cdot f_1(x, y) + b \cdot f_2(x, y) \leftrightarrow a \cdot F_1(u, v) + b \cdot F_2(u, v)\]

2. **Shift Theorem:** \[f(x - a, y - b) \leftrightarrow F(u, v) \cdot e^{-j2\pi(au/M + bv/N)}\]

3. **Scaling:** \[f(ax, by) \leftrightarrow \frac{1}{|ab|} F(u/a, v/b)\]

---

### Topic 17: Low Pass Filter

**Definition:**
A low pass filter (LPF) attenuates high-frequency components while preserving low-frequency components. Results in smoothing, blurring, and noise reduction.

**General Low Pass Filter Transfer Function:**

\[H_{LP}(u, v) = \frac{1}{1 + D(u, v)^{2n} / D_0^{2n}}\]

Where:
- D(u, v) = distance from center frequency (0, 0)
- D_0 = cutoff frequency (in pixels)
- n = filter order

**Distance Formula:**
\[D(u, v) = \sqrt{(u - M/2)^2 + (v - N/2)^2}\]

**Frequency Response:**
- H_LP(0, 0) ≈ 1 (low frequencies pass)
- H_LP increases with distance = high frequencies attenuate

**Filtering in Frequency Domain:**
\[G(u, v) = H_{LP}(u, v) \cdot F(u, v)\]

**Smoothing Properties:**
- Removes high-frequency noise
- Blurs edges and details
- Preserves overall structure
- Reduces dynamic range

**Applications:**
- Noise reduction in forensic images
- Fingerprint image smoothing before analysis
- Removal of sensor noise from biometric samples
- Medical image preprocessing
- De-noising old forensic photographs

**Spatial Domain Equivalent:**
Low pass filtering in frequency domain = convolution with smoothing kernel in spatial domain

Examples:
- Averaging kernel
- Gaussian kernel
- Median filter

---

### Topic 18: High Pass Filter

**Definition:**
A high pass filter (HPF) attenuates low-frequency components while preserving high-frequency components. Results in edge enhancement, sharpening, and detail extraction.

**General High Pass Filter Transfer Function:**

\[H_{HP}(u, v) = 1 - H_{LP}(u, v)\]

Or directly:
\[H_{HP}(u, v) = \frac{D(u, v)^{2n}}{D(u, v)^{2n} + D_0^{2n}}\]

**Characteristics:**
- H_HP(0, 0) = 0 (removes DC component)
- H_HP increases away from center (enhances high frequencies)
- High values at edges and detailed regions

**Frequency Response:**
- Emphasizes rapid intensity changes
- Enhances edges and boundaries
- Reduces smooth regions
- Sharpens image details

**Filtering Process:**
\[G(u, v) = H_{HP}(u, v) \cdot F(u, v)\]

**Sharpening Formula:**
Enhanced image = Original + Scaled high-pass result

\[g(x, y) = f(x, y) + \alpha \cdot HPF[f(x, y)]\]

Where α is enhancement strength (typically 0.5 to 1.5)

**Unsharp Masking Using High Pass Filter:**
\[g(x, y) = f(x, y) + \lambda [f(x, y) - LPF(f)]\]

Where λ is sharpening parameter.

**Applications in Forensics:**
- Edge detection in forensic images
- Fingerprint ridge enhancement and clarity
- Detection of boundaries in latent prints
- Enhancement of fine details in photographs
- Iris border localization
- Facial feature extraction
- Detection of document alterations

**Spatial Domain Equivalents:**
HPF in frequency → Laplacian, Sobel, or Prewitt in spatial domain

**Edge Detection Using HPF:**
Strong response at:
- Fingerprint ridge endings
- Bifurcations
- Boundaries between different regions

---

### Topic 19: Ideal Filter

**Definition:**
An ideal filter has a sharp cutoff frequency D_0, with complete transmission below cutoff and complete rejection above cutoff. Theoretical construct rarely implemented due to ringing artifacts.

**Ideal Low Pass Filter (ILPF):**

\[H(u, v) = \begin{cases}
1 & \text{if } D(u, v) \leq D_0 \\
0 & \text{if } D(u, v) > D_0
\end{cases}\]

Where D(u, v) is distance from center.

**Ideal High Pass Filter (IHPF):**

\[H(u, v) = \begin{cases}
0 & \text{if } D(u, v) \leq D_0 \\
1 & \text{if } D(u, v) > D_0
\end{cases}\]

Or simply: H_HP = 1 - H_LP

**Ideal Band Pass Filter (IBPF):**

\[H(u, v) = \begin{cases}
1 & \text{if } D_1 \leq D(u, v) \leq D_2 \\
0 & \text{otherwise}
\end{cases}\]

**Ideal Band Reject (Notch) Filter:**

\[H(u, v) = \begin{cases}
0 & \text{if } D_1 \leq D(u, v) \leq D_2 \\
1 & \text{otherwise}
\end{cases}\]

**Distance Formula (Euclidean):**
\[D(u, v) = \sqrt{(u - M/2)^2 + (v - N/2)^2}\]

**Practical Example:**
For 256×256 image with D_0 = 50 pixels:

\[H(u, v) = \begin{cases}
1 & \text{if } \sqrt{(u-128)^2 + (v-128)^2} \leq 50 \\
0 & \text{otherwise}
\end{cases}\]

**Characteristics:**
- Sharp transition at cutoff frequency
- Complete pass/reject behavior
- Theoretical approximation
- Causes ringing artifacts (Gibbs phenomenon)

**Ringing Problem:**
Ideal filters produce oscillations near edges in spatial domain - distortion artifacts

**Disadvantages:**
- Excessive ringing and oscillations
- Overshoot at boundaries
- Visually unpleasant results
- Unrealistic sharp cutoff

**Advantages:**
- Mathematically simple
- Useful for theoretical analysis
- Good understanding baseline

**Applications (Limited):**
- Theoretical studies
- Baseline comparisons
- Understanding filter behavior
- Educational purposes

**Real Implementation:**
Rarely used in practice; replaced by Butterworth or Gaussian filters with gradual rolloff.

---

### Topic 20: Butterworth Filter

**Definition:**
Butterworth filter provides smooth rolloff between passband and stopband, eliminating sharp cutoff problems of ideal filters while maintaining simple form.

**Butterworth Low Pass Filter (BLPF):**

\[H(u, v) = \frac{1}{1 + [D(u, v)/D_0]^{2n}}\]

Where:
- D(u, v) = distance from center (0, 0)
- D_0 = cutoff frequency (in pixels)
- n = order of filter (n = 1, 2, 3, ...)

**Butterworth High Pass Filter (BHPF):**

\[H(u, v) = \frac{1}{1 + [D_0/D(u, v)]^{2n}}\]

Or equivalently:
\[H_{HP}(u, v) = 1 - H_{LP}(u, v)\]

**Key Parameters:**

1. **Cutoff Frequency D_0:**
   - At D(u, v) = D_0: H(D_0) = 0.5 (50% attenuation)
   - Approximately -3dB point

2. **Order n:**
   - n = 1: Gradual rolloff (first-order)
   - n = 2: Moderate rolloff (second-order)
   - n = 4: Steep rolloff
   - Higher n → sharper cutoff (approaches ideal)

**Butterworth Band Pass Filter:**

\[H_{BP}(u, v) = \frac{D(u, v) \cdot W}{D^2(u, v) + D_1 \cdot D_2}\]

Where:
- D_1, D_2 = inner and outer radii
- W = bandwidth

**Characteristics:**
- Smooth transition at cutoff
- Monotonic magnitude response (no ripples)
- No ringing artifacts
- Natural frequency response

**Advantages Over Ideal:**
1. No ringing
2. Smooth transition
3. Better visual quality
4. Flexible via order parameter
5. Practical implementation

**Design Equations:**
For specified -3dB frequency ω_c:

\[\omega_c = \frac{1}{\sqrt[2n]{1 + \epsilon^2}}\]

For ripple-free passband with passband ripple ε_p and stopband attenuation ε_s:

\[n \geq \frac{\log_{10}[(10^{0.1\alpha_s} - 1)/(10^{0.1\alpha_p} - 1)]}{2\log_{10}(\omega_s/\omega_p)}\]

**Forensic Applications:**
- Fingerprint enhancement with controlled blur
- Selective noise removal in biometric images
- Iris image preprocessing
- Crime scene photography enhancement
- Medical imaging (X-rays, CT scans)

**Comparison with Other Filters:**

| Filter | Transition | Ripple | Ringing | Simplicity |
|--------|-----------|--------|---------|-----------|
| Ideal | Sharp | None | Severe | Simple |
| Butterworth | Smooth | None | Minor | Moderate |
| Chebyshev | Sharp | Yes | Minimal | Moderate |
| Gaussian | Smooth | None | Minimal | Simple |

---

### Topic 21: Gaussian Filter

**Definition:**
Gaussian filter uses Gaussian function to define frequency response. Provides smoothest possible transition without ringing artifacts.

**Gaussian Low Pass Filter (GLPF):**

\[H(u, v) = e^{-D^2(u,v)/(2D_0^2)}\]

Where:
- D(u, v) = distance from origin
- D_0 = standard deviation (cutoff parameter)

**Alternative Form:**
\[H(u, v) = e^{-D^2(u,v)/2\sigma^2}\]

Where σ = D_0

**Gaussian High Pass Filter (GHPF):**

\[H(u, v) = 1 - e^{-D^2(u,v)/(2D_0^2)}\]

**Mathematical Properties:**
- At D_0: H(D_0) ≈ 0.606 (60.6% of maximum)
- Smooth exponential decay
- No discontinuities

**Gaussian Kernel in Spatial Domain:**
2D Gaussian kernel for convolution:

\[G(x, y) = \frac{1}{2\pi\sigma^2} \exp\left(-\frac{x^2 + y^2}{2\sigma^2}\right)\]

**Relationship Between Domains:**
Gaussian in frequency domain ↔ Gaussian in spatial domain

Fourier transform property:
\[\text{FT}[e^{-\pi x^2}] = e^{-\pi u^2}\]

**Characteristics:**
1. **No Ringing:** Smooth exponential transition
2. **Minimal Artifacts:** Unlike ideal filters
3. **Optimal Resolution:** Best frequency localization
4. **Simplicity:** Easy to compute and implement
5. **Controllable:** Single parameter σ controls bandwidth

**Practical Implementation:**
Spatial domain convolution with Gaussian kernel:

\[g(x, y) = \sum_{s=-k}^{k} \sum_{t=-k}^{k} G(s, t) \cdot f(x+s, y+t)\]

Where 3σ determines kernel size k.

**Parameter Selection:**
- Small σ (e.g., 0.5): Minimal blur, preserves detail
- Medium σ (e.g., 1.0): Balanced smoothing
- Large σ (e.g., 2.0): Strong blur, removes detail and noise

**Forensic Applications:**
- Fingerprint image smoothing with minimal artifacts
- Iris image preprocessing
- Noise reduction in forensic photographs
- Latent fingerprint enhancement
- Medical image smoothing
- Document image preprocessing

**Advantages:**
- No ringing or oscillations
- Smooth, natural appearance
- Fast computation
- Well-understood mathematical properties
- Optimal for Gaussian noise removal

**Wiener Filtering with Gaussian:**
When noise is Gaussian distributed:

\[H_W(u, v) = \frac{1}{1 + S_n(u,v)/S_f(u,v)}\]

Where S_n = noise power spectrum, S_f = image power spectrum.

**Common Applications:**
1. **Preprocessing:** Before fingerprint matching
2. **Denoising:** Reduction of sensor noise
3. **Normalization:** Before histogram equalization
4. **Detail Preservation:** Low σ maintains edges

---

### Topic 22: Image Segmentation (Intensity, Gray Level, Frequency, Pixel Value Based)

**Definition:**
Image segmentation partitions an image into multiple regions or objects based on specific criteria. Goal is to simplify image representation for easier analysis.

## A) INTENSITY-BASED SEGMENTATION

**Threshold-Based (Global Thresholding):**

\[g(x, y) = \begin{cases}
1 & \text{if } f(x, y) \geq T \\
0 & \text{if } f(x, y) < T
\end{cases}\]

Where:
- T = threshold value
- f(x, y) = input image pixel
- g(x, y) = segmented binary image

**Otsu's Method for Optimal Threshold:**
Maximize between-class variance:

\[\sigma_B^2(T) = \omega_0(T)[\mu_0(T) - \mu_T]^2 + \omega_1(T)[\mu_1(T) - \mu_T]^2\]

Where:
- ω_0, ω_1 = class probabilities
- μ_0, μ_1 = class means
- μ_T = total mean

**Multi-Level Thresholding:**

\[g(x, y) = \begin{cases}
0 & \text{if } f(x, y) < T_1 \\
1 & \text{if } T_1 \leq f(x, y) < T_2 \\
2 & \text{if } T_2 \leq f(x, y) < T_3 \\
\vdots \\
k & \text{if } f(x, y) \geq T_k
\end{cases}\]

## B) GRAY LEVEL VALUE-BASED SEGMENTATION

**Gray Level Slicing (Already Covered in Topic 14):**

\[g(x, y) = \begin{cases}
L-1 & \text{if } a \leq f(x, y) \leq b \\
0 & \text{otherwise}
\end{cases}\]

**Histogram-Based Segmentation:**
Analyze histogram peaks and valleys:

\[H(i) = \text{count of pixels with gray level } i\]

Segments separated by histogram valleys (local minima).

**K-Means Clustering (Gray Level):**
Partition pixels into K clusters based on gray level:

\[\text{Minimize: } J = \sum_{k=1}^{K} \sum_{i \in C_k} (f_i - \mu_k)^2\]

Where:
- C_k = cluster k
- μ_k = mean gray level of cluster k
- f_i = gray level of pixel i

**Cluster Centers Update:**
\[\mu_k^{(t+1)} = \frac{1}{|C_k|} \sum_{i \in C_k} f_i\]

## C) FREQUENCY-BASED SEGMENTATION

**Frequency Domain Filtering for Segmentation:**

1. Apply FFT:
\[F(u, v) = \text{FFT}[f(x, y)]\]

2. Apply filter:
\[G(u, v) = H(u, v) \cdot F(u, v)\]

3. Extract edges:
\[|G(u, v)| > T_f\]

4. Inverse FFT:
\[g(x, y) = \text{IFFT}[G(u, v)]\]

**High Pass Filtering for Edge Detection:**
Use HPF to extract edges in frequency domain:

\[E(u, v) = H_{HP}(u, v) \cdot F(u, v)\]

## D) PIXEL VALUE-BASED CLUSTERING SEGMENTATION

**Distance-Based Segmentation:**
Segment based on pixel value distance:

\[d(f(x, y), \mu_k) = |f(x, y) - \mu_k|\]

Assign pixel to cluster with minimum distance.

**Region Growing:**
Start with seed point, grow region by adding adjacent pixels with similar values:

\[R = \{(x, y) : |f(x, y) - f(x_0, y_0)| < T\}\]

**Fuzzy C-Means Clustering:**
Soft clustering allowing partial membership:

\[\text{Minimize: } J = \sum_{i=1}^{N} \sum_{k=1}^{C} u_{ik}^m ||f_i - \mu_k||^2\]

Where:
- u_ik = membership degree (0 to 1)
- m = fuzziness parameter (typically 2)

**Watershed Segmentation:**
Treat image as topographic map:

\[\text{Watershed} = \text{ridge lines between catchment basins}\]

**Morphological Segmentation:**
Using erosion and dilation operations:

\[\text{Opening: } f \circ g = (f \ominus g) \oplus g\]
\[\text{Closing: } f \bullet g = (f \oplus g) \ominus g\]

Where ⊖ = erosion, ⊕ = dilation

## E) FORENSIC APPLICATIONS OF SEGMENTATION

**Fingerprint Segmentation:**
- Separate foreground (fingerprint) from background
- Extract region of interest
- Remove noisy borders

**Iris Segmentation:**
- Localize iris region between sclera and pupil
- Remove eyelids and eyelashes
- Normalize for recognition

**Face Segmentation:**
- Extract facial region from background
- Identify facial features
- Remove non-face regions

**Blood/Stain Detection:**
- Segment based on intensity ranges
- Identify biological evidence
- Quantify affected areas

## F) PERFORMANCE METRICS FOR SEGMENTATION

**Dice Similarity Coefficient:**
\[D = \frac{2|A \cap B|}{|A| + |B|}\]

**Jaccard Index:**
\[J = \frac{|A \cap B|}{|A \cup B|}\]

Where A and B are segmented regions.

---

## SUMMARY TABLE: IMAGE PROCESSING TECHNIQUES

| Topic | Domain | Type | Typical Use |
|-------|--------|------|------------|
| Linear Transformation | Spatial | Enhancement | General contrast adjustment |
| Point Operations | Spatial | Modification | Intensity mapping |
| Digital Negative | Spatial | Transformation | Inversion/detail reveal |
| Logarithmic | Spatial | Non-linear | Dynamic range compression |
| Exponential | Spatial | Non-linear | Dynamic range expansion |
| Power/Gamma | Spatial | Non-linear | Display correction |
| Contrast Stretching | Spatial | Enhancement | Utilize full range |
| Gray Level Slicing | Spatial | Segmentation | Feature isolation |
| Bit Plane Slicing | Spatial | Analysis | Noise/detail separation |
| Low Pass Filter | Frequency | Smoothing | Noise removal |
| High Pass Filter | Frequency | Sharpening | Edge enhancement |
| Butterworth | Both | Practical filter | Balanced approach |
| Gaussian | Both | Optimal filter | Best noise reduction |
| Segmentation | Both | Partitioning | Region extraction |

---

## FORENSIC APPLICATION SUMMARY

**Common Biometric Enhancement Workflow:**

1. Acquisition → Raw image
2. Histogram Equalization → Improved contrast
3. Gaussian Low Pass → Noise reduction
4. High Pass Enhancement → Detail emphasis
5. Contrast Stretching → Utilize full range
6. Threshold/Segmentation → Feature extraction
7. Bit plane analysis → Compression detection
8. Matching → Identification

**Quality Assessment:**
- Signal-to-Noise Ratio (SNR)
- Peak Signal-to-Noise Ratio (PSNR)
- Structural Similarity Index (SSIM)

---

**References:**
- IEEE Signal Processing Society Standards
- Digital Image Processing (Gonzalez & Woods)
- Indian Biometric Standards (UIDAI, BIS)
- Forensic Science Digital Evidence Standards
- ISO/IEC Image Processing Standards

**Document Prepared For:** B.Sc. Forensic Science Students  
**Examination Level:** College/University Entrance and Semester Exams  
**Year:** 2025