# 22 IMAGE PROCESSING TECHNIQUES: COMPLETE GUIDE WITH FORMULAS

## OVERVIEW

This document provides comprehensive coverage of 22 essential image processing techniques organized into three main categories:
- **Spatial Domain Methods** (Topics 1-15): Point operations and transformations applied directly to pixel values
- **Frequency Domain Methods** (Topics 16-21): Filtering operations based on Fourier transforms
- **Image Segmentation** (Topic 22): Pixel classification based on intensity, gray level, frequency, and other characteristics

---

## SPATIAL DOMAIN METHODS (Topics 1-15)

### Topic 1: Spatial Domain Method

**Definition:**
Spatial domain refers to image processing operations performed directly on pixel coordinates (x, y) and their intensity values. These operations modify pixel values based on their original intensities and spatial positions.

**Mathematical Representation:**
```
g(x, y) = T[f(x, y)]
```

**Where:**
- f(x, y) = input image
- g(x, y) = output image (processed)
- T = transformation operator
- (x, y) = pixel coordinates

**Characteristics:**
→ Operations performed directly on pixel values
→ Computationally simpler than frequency domain methods
→ Results visible immediately in spatial representation
→ Suitable for local and global image modifications

**Applications:**
- Contrast enhancement
- Image smoothing and sharpening
- Edge detection
- Image restoration
- Noise reduction

**Advantages:**
- Direct relationship between input and output
- Easy to understand and implement
- Real-time processing possible
- Preserves spatial resolution

---

### Topic 2: Linear Transformation

**Definition:**
Linear transformation is an intensity transformation where the input-output relationship follows a linear function.

**Basic Formula:**
```
s = ar + b
```

**Where:**
- s = output gray level
- r = input gray level
- a = slope (gradient)
- b = y-intercept
- Range: 0 ≤ r, s ≤ L-1 (where L = 256 for 8-bit images)

**General Linear Transformation:**
```
s = (s₂ - s₁)/(r₂ - r₁) × (r - r₁) + s₁
```

**Where:**
- (r₁, s₁) = first control point
- (r₂, s₂) = second control point

**Matrix Form (for multiple pixels):**
```
[g(x,y)]   [a  b] [f(x,y)]
[  1   ] = [0  1] [  1   ]
```

**Special Cases:**

**Identity Transformation:**
```
s = r (a = 1, b = 0)
```
Output image identical to input; no change.

**Scaling:**
```
s = a × r
- If a > 1: Image brightens
- If 0 < a < 1: Image darkens
```

**Translation:**
```
s = r + b
- If b > 0: Image brightens
- If b < 0: Image darkens
```

**Applications:**
- Brightness adjustment
- Contrast modification
- Linear stretching
- Simple image enhancement

**Example:**
For image with input range [50, 200] stretched to output range [0, 255]:
```
s = (255 - 0)/(200 - 50) × (r - 50) + 0
s = (255/150) × (r - 50)
s = 1.7 × (r - 50)
```

---

### Topic 3: Point Operation

**Definition:**
Point operation processes each pixel independently, applying a transformation based solely on that pixel's intensity value, regardless of its neighbors or spatial position.

**General Formula:**
```
g(x, y) = T(f(x, y))
```

**Where:**
- T = transformation function (non-parametric mapping)
- f(x, y) = input pixel at coordinates (x, y)
- g(x, y) = output pixel

**Transformation Lookup Table:**
For any intensity value r, look up corresponding output value s:
```
LUT[r] = s

Example: LUT[0] = 255, LUT[1] = 254, ..., LUT[255] = 0 (for image negative)
```

**Key Characteristics:**
→ Output depends only on input intensity (not spatial position)
→ Fast computation (O(n) where n = number of pixels)
→ Can be implemented using lookup tables
→ No pixel neighborhood required

**Types of Point Operations:**
1. Linear transformations
2. Non-linear transformations
3. Thresholding
4. Intensity level slicing
5. Bit plane slicing

**Advantages:**
- Fastest transformation method
- No spatial information loss
- Reversible if inverse function exists
- Efficient memory usage

**Example:**
```
For pixel value r = 100:
g(100) = T(100)

If T is logarithmic: g(100) = c × log(1 + 100)
If T is power law: g(100) = c × 100^γ
```

---

### Topic 4: Digital Negative

**Definition:**
Digital negative inverts gray levels, creating a photographic negative effect. High intensity values become low, and vice versa.

**Mathematical Formula:**
```
s = L - 1 - r
```

**Where:**
- s = output gray level (negative)
- r = input gray level (original)
- L = number of gray levels (typically 256 for 8-bit images)

**Expanded Formula for 8-bit Images:**
```
s = 255 - r
```

**Pixel-wise Operation:**
```
For r = 0: s = 255 - 0 = 255 (black → white)
For r = 128: s = 255 - 128 = 127 (mid-gray remains mid-gray)
For r = 255: s = 255 - 255 = 0 (white → black)
```

**Matrix Representation:**
```
Transform Matrix T:
T[0] = 255
T[1] = 254
T[2] = 253
...
T[255] = 0
```

**Graphical Representation:**
- Input range: [0, L-1]
- Output range: [L-1, 0]
- Linear relationship with negative slope = -1
- Passes through midpoint (L-1)/2

**Applications:**
- Photographic negative creation
- Enhancing white/gray detail in dark regions
- Digital mammography analysis
- Document enhancement
- Highlighting concealed features

**Example Application:**
Original medical image with faint details in dark areas → Apply digital negative → Enhanced visibility of previously hidden structures

**Implementation:**
```
For every pixel f(x,y) in input image:
  g(x,y) = 255 - f(x,y)
```

**Properties:**
- Involutive operation: Applying twice recovers original (g(g(r)) = r)
- Preserves contrast magnitude
- Reverses intensities uniformly

---

### Topic 5: Non-linear Transformation

**Definition:**
Non-linear transformation applies a non-linear function to pixel intensities, where the relationship between input and output is not a straight line.

**General Formula:**
```
s = T(r)
where T is a non-linear function
```

**Characteristics:**
- Input-output relationship is curved (not linear)
- Rates of change vary across intensity range
- More flexible than linear transformations
- Can provide enhanced contrast in specific regions

**Common Non-linear Functions:**
1. Logarithmic: s = c × log(1 + r)
2. Exponential: s = c × (e^r - 1)
3. Power law: s = c × r^γ
4. Square: s = r²
5. Square root: s = √r
6. Sigmoid: s = 1 / (1 + e^(-r))

**Mathematical Properties:**
```
First Derivative (rate of change):
ds/dr ≠ constant (non-linear characteristic)

Second Derivative (curvature):
d²s/dr² ≠ 0 (indicates non-linearity)
```

**Advantages Over Linear:**
- Better contrast enhancement in specific regions
- Can compress dynamic range
- Gamma correction capability
- More natural appearance

**Example Graph Characteristics:**
- Logarithmic: Steep for low r, flattens for high r
- Exponential: Flattens for low r, steep for high r
- Power law (γ < 1): Compresses dark values, expands bright values
- Power law (γ > 1): Expands dark values, compresses bright values

---

### Topic 6: Square Function

**Definition:**
Square function applies a quadratic transformation to pixel intensities: s = r²

**Mathematical Formula:**
```
s = r²
```

**Normalized (0-1 range):**
```
s = (r/L)² × L
where L = 256
```

**For 8-bit Images (0-255 range):**
```
s = (r²/256) × 256 = r²/256 × 256

Example values:
r = 0: s = 0
r = 16: s = 256/256 = 1
r = 128: s = 16384/256 = 64
r = 255: s = 65025/256 = 254
```

**Characteristics:**
→ Non-linear transformation
→ Parabolic curve (U-shaped)
→ Output range smaller than input
→ Darkens midtones, brightens bright values
→ Amplifies differences in bright regions

**Graphical Properties:**
- Vertex at origin (0, 0)
- Symmetric around y-axis (r = 0)
- Steep slope for high r values
- Gradual slope for low r values

**Output Range Mapping:**
```
Input [0, 255] → Output [0, 65025] → Normalized to [0, 255]
```

**Derivative (Rate of Change):**
```
ds/dr = 2r

At r = 0: rate = 0 (minimal change)
At r = 128: rate = 256 (moderate change)
At r = 255: rate = 510 (maximum change)
```

**Applications:**
- Contrast enhancement (bright regions)
- Noise amplification (dark regions)
- Gamma correction preprocessing
- Highlight detection

**Inverse Function:**
```
r = √s
```

**Effect on Image:**
- Brightens the image overall
- Increases contrast in bright regions
- Decreases visibility in dark regions
- Potential noise amplification in dark areas

---

### Topic 7: Square Root Function

**Definition:**
Square root function applies a square root transformation to pixel intensities: s = √r

**Mathematical Formula:**
```
s = √r
```

**Normalized Formula (0-1 range):**
```
s = √(r/L) × L
where L = 256
```

**For 8-bit Images (0-255 range):**
```
s = √r

Example values:
r = 0: s = 0
r = 4: s = 2
r = 16: s = 4
r = 64: s = 8
r = 128: s = 11.3
r = 255: s = 15.97 ≈ 16
```

**Mapping with Full Range Preservation:**
```
s = (√r / √255) × 255

r = 0: s = 0
r = 64: s = 64/16 × 255 = 64
r = 128: s = 11.3/16 × 255 = 179
r = 255: s = 16/16 × 255 = 255
```

**Characteristics:**
→ Non-linear transformation
→ Inverse of square function
→ Concave curve (∩-shaped)
→ Brightens dark regions significantly
→ Compresses bright regions
→ Expands output range in dark areas

**Graphical Properties:**
- Starts at origin (0, 0)
- Steep slope for low r values
- Gradual slope for high r values
- Concave upward shape

**Derivative (Rate of Change):**
```
ds/dr = 1/(2√r)

At r → 0: rate → ∞ (very steep)
At r = 64: rate = 1/16 = 0.0625
At r = 255: rate = 1/32 ≈ 0.0313
```

**Applications:**
- Dark image enhancement
- Dynamic range compression
- Detail preservation in shadows
- Preprocessing for histogram equalization
- Gamma correction (γ = 0.5)

**Inverse Function:**
```
r = s²
```

**Effect on Image:**
- Significantly brightens dark regions
- Reveals hidden details in shadows
- Compresses bright values
- Enhances mid-tones visibility
- Reduces contrast in bright areas

**Comparison with Linear Brightening:**
```
Linear s = 1.5r: Uniform brightness increase
Square root s = √r: More brightening in dark regions
```

---

### Topic 8: Logarithmic Function

**Definition:**
Logarithmic transformation compresses the dynamic range by applying logarithmic function to pixel intensities.

**Basic Formula:**
```
s = c × log(1 + r)
```

**Where:**
- c = constant for scaling output to desired range
- r = input intensity (≥ 0)
- log = natural logarithm (base e) or base-10

**Scaled to Full Output Range [0, L-1]:**
```
s = (L-1) / log(1 + L-1) × log(1 + r)

For 8-bit images (L = 256):
s = 255 / log(256) × log(1 + r)
s = 255 / 5.545 × log(1 + r)
s ≈ 46 × log(1 + r)
```

**Example Values (using natural log):**
```
r = 0: s = c × log(1) = 0
r = 1: s = c × log(2) ≈ 0.693c
r = 10: s = c × log(11) ≈ 2.398c
r = 100: s = c × log(101) ≈ 4.615c
r = 255: s = c × log(256) ≈ 5.545c
```

**Important Note (Avoiding Negative Log):**
```
log(r) would be undefined for r = 0
Solution: Always use log(1 + r) or log(c + r)
This shifts domain so that log argument ≥ 1
```

**Characteristics:**
→ Non-linear transformation
→ Compresses dynamic range
→ Brightens dark regions significantly
→ Compresses bright regions moderately
→ Logarithmic curve (concave)

**Graphical Properties:**
- Steep slope at low r values
- Gradual slope at high r values
- Concave downward shape
- Passes through origin

**Derivative (Rate of Change):**
```
ds/dr = c / (1 + r)

At r = 0: rate = c (maximum)
At r = 10: rate = c/11 (decreased)
At r = 100: rate = c/101 (further decreased)
At r = 255: rate = c/256 (minimal)
```

**Applications:**
- Fourier spectrum visualization
- Dynamic range compression
- Enhanced visualization of low-intensity features
- Medical image enhancement
- Satellite image processing
- Detail preservation in dark regions

**Common Constant Values:**
```
c = 1.0: Minimal scaling
c = 25.0: Moderate dynamic range compression
c = 46.0: Full range utilization [0, 255]
```

**Inverse Function:**
```
r = e^(s/c) - 1
```

**Effect on Image:**
- Dramatically brightens dark areas
- Reveals hidden details in shadows
- Reduces contrast in bright areas
- Compresses overall dynamic range
- Natural appearance for many images

---

### Topic 9: Exponential Function

**Definition:**
Exponential transformation applies exponential function to pixel intensities, providing inverse effect of logarithmic transformation.

**Basic Formula:**
```
s = c × (e^r - 1)
```

**Where:**
- c = constant for scaling output range
- r = input intensity
- e = Euler's number (≈ 2.71828)

**Scaled to Output Range [0, L-1]:**
```
s = (L-1) / (e^(L-1) - 1) × (e^r - 1)

For 8-bit images (L = 256):
s = 255 / (e^255 - 1) × (e^r - 1)

Note: e^255 is extremely large (≈ 10^110)
Practical limitation: r typically limited to range where computation is feasible
```

**Example Values (scaled version):**
```
r = 0: s = c × (1 - 1) = 0
r = 1: s = c × (e - 1) ≈ 1.718c
r = 2: s = c × (e² - 1) ≈ 6.389c
r = 5: s = c × (e⁵ - 1) ≈ 147.4c
r = 7: s ≈ 1096c (exceeds 8-bit range)
```

**Characteristics:**
→ Non-linear transformation
→ Inverse of logarithmic transformation
→ Darkens image substantially
→ Brightens bright regions significantly
→ Exponential curve (convex)
→ Highly sensitive to input variations

**Graphical Properties:**
- Gradual slope at low r values
- Extremely steep slope at high r values
- Convex upward shape
- Rapid growth rate

**Derivative (Rate of Change):**
```
ds/dr = c × e^r

At r = 0: rate = c
At r = 1: rate ≈ 2.718c
At r = 2: rate ≈ 7.389c
At r = 5: rate ≈ 148.4c
```

**Limitations:**
- Exponential growth very rapid
- Output exceeds 8-bit range for small r
- Practical use limited to normalized inputs
- Numerical stability concerns for large r

**Modified Exponential (Practical Form):**
```
s = c × (e^(r/k) - 1)

where k = scaling factor to control growth rate
Example: k = 50
s = c × (e^(r/50) - 1)
```

**Applications:**
- Dark image darkening
- Contrast reduction
- Gamma correction (γ > 1)
- Edge suppression
- Noise amplification (bright regions)
- Specialized medical imaging

**Inverse Function:**
```
r = ln(s/c + 1)
```

**Effect on Image:**
- Darkens entire image significantly
- Compresses bright values dramatically
- Expands dark values minimally
- Overall contrast reduction
- Detail loss in bright regions

**Comparison with Logarithmic:**
```
Log: Brightens dark → Compresses bright
Exp: Darkens dark → Expands bright
```

---

### Topic 10: Power Function (Gamma Correction)

**Definition:**
Power function transformation applies a power law to pixel intensities, commonly used for gamma correction to adjust display characteristics.

**Basic Formula:**
```
s = c × r^γ
```

**Where:**
- c = constant (typically 1 for normalized input/output)
- r = input intensity (normalized to [0, 1])
- γ (gamma) = exponent controlling transformation curve

**For 8-bit Images (0-255 range):**
```
s = (L-1) × (r/(L-1))^γ

s = 255 × (r/255)^γ
```

**Physical Interpretation:**
```
γ < 1: Brightens image (brightening power law)
γ = 1: Linear (identity transformation)
γ > 1: Darkens image (darkening power law)
```

**Example Values (γ = 0.4):**
```
r = 0: s = 255 × (0/255)^0.4 = 0
r = 64: s = 255 × (0.251)^0.4 ≈ 119
r = 128: s = 255 × (0.502)^0.4 ≈ 170
r = 192: s = 255 × (0.753)^0.4 ≈ 210
r = 255: s = 255 × (1)^0.4 = 255
```

**Example Values (γ = 2.2):**
```
r = 0: s = 0
r = 64: s = 255 × (0.251)^2.2 ≈ 13
r = 128: s = 255 × (0.502)^2.2 ≈ 55
r = 192: s = 255 × (0.753)^2.2 ≈ 167
r = 255: s = 255
```

**Gamma Ranges:**
```
0 < γ < 1: Expansion (brightening)
γ = 1: No change (identity)
γ > 1: Compression (darkening)

Typical display gamma: γ_display ≈ 2.2
Inverse gamma correction: γ_correction = 1/2.2 ≈ 0.45
```

**Characteristics:**
→ Non-linear transformation
→ Power law relationship
→ Curve shape depends on γ value
→ Standard for display calibration
→ Inverse operation easily computed

**Graphical Properties (γ < 1):**
- Concave curve (∩-shaped)
- Brightens primarily dark regions
- Compresses bright regions slightly
- Steeper slope at low r

**Graphical Properties (γ > 1):**
- Convex curve (∪-shaped)
- Darkens primarily bright regions
- Compresses dark regions
- Steeper slope at high r

**Derivative (Rate of Change):**
```
ds/dr = c × γ × r^(γ-1)

For γ = 0.5:
ds/dr = 0.5 × r^(-0.5) = 0.5/√r
- Decreases as r increases
- Maximum rate at r → 0

For γ = 2:
ds/dr = 2r
- Increases as r increases
- Maximum rate at high r values
```

**Inverse Function:**
```
r = s^(1/γ)
```

**Display Gamma Correction:**
```
Monitor receives: s = r^(1/γ)
Monitor applies gamma: output = (r^(1/γ))^γ = r (original)

Workflow:
Original image r → Apply inverse gamma (1/γ) → Transmit/store s
Monitor (γ = 2.2) → Apply gamma → Output ≈ r (corrected)
```

**Applications:**
- Display calibration
- Monitor/camera gamma correction
- Contrast adjustment
- Medical image enhancement
- Photography workflow (RAW processing)
- Video color grading

**Common Gamma Values:**
```
γ = 0.4-0.5: Brightening (used for dark images)
γ = 1.0-1.5: Slight brightening
γ = 2.2-2.4: Standard display gamma
γ = 3.0+: Heavy darkening
```

**Mathematical Properties:**
```
Associative: (r^γ₁)^γ₂ = r^(γ₁×γ₂)
Commutative in cascade: Effect of γ₁ then γ₂ = γ₁×γ₂
```

---

### Topic 11: Gamma Correlation

**Definition:**
Gamma correlation refers to the relationship between image gamma values and their perceptual impact, involving correction and adjustment of gamma for optimal display and perception.

**Theoretical Basis:**
Human vision follows approximately logarithmic response to light intensity (Weber-Fechner law).

**Formula:**
```
Perceived_brightness ∝ log(Intensity)
```

**Gamma Relationship:**
```
Output_display = Input^(1/γ_display)

Typical monitor gamma: γ_display ≈ 2.2

For proper display:
Transmitted signal = Original^(1/2.2) = Original^0.4545
```

**Gamma Encoding/Decoding Chain:**
```
Original Image (linear) 
  ↓ [Apply γ = 0.4545 (encode)]
Gamma-corrected Image (stored/transmitted)
  ↓ [Apply γ = 2.2 (decode/monitor)]
Display Output (linear perceived)
```

**Standard Gamma Values Worldwide:**
```
sRGB standard: γ = 2.2
Macintosh (older): γ = 1.8
Television (NTSC): γ ≈ 2.2
Digital cinema: γ ≈ 2.6
```

**Mathematical Relationship:**
```
For proper correction:
γ_encode × γ_decode = 1
γ_decode = 1/γ_encode

If γ_decode = 2.2, then γ_encode = 1/2.2 ≈ 0.4545
```

**Components of Gamma:**
```
Total system gamma: γ_system = γ_camera × γ_transmission × γ_display

Typical: γ_system = 1.0 (balanced/linear reproduction)

If γ_camera = 0.4545 and γ_display = 2.2:
γ_system = 0.4545 × 2.2 = 1.0 (correct)
```

**Gamma Correlation Effects:**
```
γ > 1: Image appears darker than original
γ < 1: Image appears brighter than original
γ = 1: Linear (no perceptual change)
```

**Correction Procedure:**
```
1. Measure camera/sensor gamma: γ_measured
2. Measure display gamma: γ_display
3. Calculate correction: γ_correct = γ_display^(-1)
4. Apply to captured image: corrected = image^γ_correct
5. Result: linear appearance on display
```

**Practical Application in Cameras:**
```
Linear sensor output → Apply γ ≈ 0.45 → sRGB image
This makes image appear perceptually linear on monitors
```

**Gamma Correction Formula:**
```
Corrected_image(x,y) = [Image(x,y)^(1/γ)] × constant

Where constant ensures output range [0, 255]
```

**Applications:**
- Camera calibration
- Monitor calibration
- Image preprocessing
- Perceptual quality optimization
- Cross-platform image consistency
- Video/cinema workflows

**Impact on Perception:**
```
Uncorrected (linear sensor output):
- Appears too dark on standard displays
- Doesn't match human perception

Corrected (γ ≈ 0.4545 applied):
- Appears natural on displays
- Matches perceptual brightness
- Optimal visibility of image details
```

---

### Topic 12: Piecewise Linear Transformation

**Definition:**
Piecewise linear transformation applies different linear functions to different gray level ranges, creating a multi-segment transformation curve.

**General Representation:**
```
        ⎧ a₁×r + b₁,        if r₀ ≤ r < r₁
        ⎪ a₂×r + b₂,        if r₁ ≤ r < r₂
s = T(r) = ⎨ a₃×r + b₃,        if r₂ ≤ r < r₃
        ⎪ ...
        ⎪ aₙ×r + bₙ,        if rₙ₋₁ ≤ r ≤ L-1
        ⎩
```

**Where:**
- r₀, r₁, r₂, ..., rₙ = control points (breakpoints)
- a₁, a₂, ..., aₙ = slopes of each segment
- b₁, b₂, ..., bₙ = y-intercepts of each segment

**Two-Segment Example (Contrast Stretching):**
```
        ⎧ (s₁/r₁) × r,              if r < r₁
s = T(r) = ⎨
        ⎪ (s₂ - s₁)/(r₁ - r₂) × (r - r₁) + s₁,  if r ≥ r₁
        ⎩

Where:
- (r₁, s₁) = first breakpoint
- (r₂, s₂) = second breakpoint
```

**Three-Segment Example:**
```
s = ⎧ (a×r),                           if 0 ≤ r < r₁
    ⎪ (b×r + c),                       if r₁ ≤ r < r₂
    ⎨ (d×r + e),                       if r₂ ≤ r ≤ L-1
    ⎩
```

**Continuity Requirement (Smooth Transitions):**
```
For smooth piecewise function:
s₁⁻ = s₁⁺ (left limit = right limit at breakpoint)

At r₁:
Left segment at r₁: a₁×r₁ + b₁
Right segment at r₁: a₂×r₁ + b₂
Must satisfy: a₁×r₁ + b₁ = a₂×r₁ + b₂
```

**Slope Calculation Between Control Points:**
```
Slope of segment: a = (s₂ - s₁)/(r₂ - r₁)

Y-intercept calculation: b = s₁ - a×r₁
or: b = s₂ - a×r₂
```

**Matrix Form (2-segment):**
```
For r in [0, r₁):      [s₀]   [a₁ b₁] [r₁]
                       [1 ] = [0  1] [1]

For r in [r₁, L-1]:    [s₁]   [a₂ b₂] [r₂]
                       [1 ] = [0  1] [1]
```

**Characteristics:**
→ Flexible and versatile
→ Combines properties of multiple functions
→ Can create any desired curve with sufficient segments
→ Computationally efficient (simple linear operations)
→ Easy to understand and implement

**Advantages:**
- User-defined control points
- Local adjustment capability
- Preserves gradient continuity (if designed properly)
- Efficient implementation
- Intuitive adjustment mechanism

**Applications:**
- Contrast stretching
- Shadow/highlight adjustment
- Tone mapping
- Histogram matching
- Flexible image enhancement
- Custom transfer curves (photography software)

**Example: Brightness and Contrast Adjustment**
```
Original image with control points:
(0, 0), (128, 120), (255, 255)

Segment 1 [0, 128): 
  a = (120 - 0)/(128 - 0) = 0.9375
  s = 0.9375×r

Segment 2 [128, 255]:
  a = (255 - 120)/(255 - 128) = 1.055
  s = 1.055×r - 15
```

---

### Topic 13: Contrast Stretching

**Definition:**
Contrast stretching (or contrast expansion) expands the narrow dynamic range of an input image to cover a wider range, improving visual quality and revealing hidden details.

**Problem Addressed:**
```
Input image range: [r_min, r_max] where r_max - r_min << L-1
This results in low contrast and poor visibility

Solution: Stretch to [0, L-1] to maximize available range
```

**Linear Contrast Stretching Formula:**
```
s = (s_max - s_min)/(r_max - r_min) × (r - r_min) + s_min

Typically: s_min = 0, s_max = L-1 = 255

Simplified:
s = (L-1)/(r_max - r_min) × (r - r_min)
s = 255/(r_max - r_min) × (r - r_min)
```

**Two-Point Control:**
```
Control points: (r₁, s₁) and (r₂, s₂)

General formula:
s = (s₂ - s₁)/(r₂ - r₁) × (r - r₁) + s₁

If r₁ = 0, s₁ = 0, r₂ = r_max, s₂ = L-1:
s = (L-1)/r_max × r
```

**Graphical Representation:**
```
Original narrow range [r_min, r_max]
    |-------|               (narrow)
Stretched to full range [0, L-1]
|-----------|-----------|   (full width)
```

**Calculating Stretching Parameters:**
```
Step 1: Find minimum and maximum intensities
r_min = min(f(x,y)) for all (x,y)
r_max = max(f(x,y)) for all (x,y)

Step 2: Calculate scaling factor
k = (L-1)/(r_max - r_min)

Step 3: Apply transformation
s(x,y) = k × (f(x,y) - r_min)

Verification:
- r_min → 0
- r_max → L-1
```

**Example Calculation:**
```
Original image: intensity range [50, 200]
Target range: [0, 255]

k = 255/(200 - 50) = 255/150 = 1.7

For pixel r = 50: s = 1.7 × (50 - 50) = 0
For pixel r = 125: s = 1.7 × (125 - 50) = 127.5
For pixel r = 200: s = 1.7 × (200 - 50) = 255
```

**Characteristics:**
→ Linear relationship (piecewise)
→ Expands dark regions
→ Expands bright regions
→ Preserves relative gray level relationships
→ No information loss (invertible)

**Contrast Enhancement Metrics:**
```
Original contrast: C_original = r_max - r_min
Stretched contrast: C_stretched = L - 1

Contrast enhancement ratio: C_stretched/C_original = (L-1)/(r_max - r_min)

Example: 255/(200-50) = 255/150 = 1.7×
Contrast improved by factor of 1.7
```

**Handling Edge Cases:**
```
If r_max = r_min (all pixels same intensity):
Division by zero error
Solution: Check condition, handle constant images separately
Result: Output uniform image at intensity (L-1)/2
```

**Cumulative Distribution Function (CDF) Method:**
```
P(r ≤ k) = (number of pixels ≤ k) / (total pixels)

Stretching via CDF:
s = P(r) × (L-1)

Provides more sophisticated stretching based on distribution
```

**Applications:**
- Low-contrast image enhancement
- Satellite image enhancement
- Medical image preprocessing
- Microscopy image analysis
- Surveillance camera footage enhancement
- Standardizing image histograms

**Advantages:**
- Simple and fast to compute
- Preserves image structure
- Invertible (original can be recovered)
- No parameter tuning required
- Effective for most images

**Limitations:**
- May amplify noise
- Can create artifacts if image has outliers
- Not optimal for all image types
- Doesn't consider human perception

---

### Topic 14: Gray Level Slicing

**Definition:**
Gray level slicing highlights specific ranges of gray levels while suppressing or darkening others. Used to emphasize regions of interest (ROI) in an image.

**Two Approaches:**

**Approach 1: With Background Retention**
```
        ⎧ s_high (e.g., white),  if r_low ≤ r ≤ r_high
s = T(r) = ⎨
        ⎩ r (original value),     otherwise

Purpose: Highlight specific gray levels while keeping background visible
```

**Approach 2: Without Background Retention**
```
        ⎧ s_high (e.g., white),  if r_low ≤ r ≤ r_high
s = T(r) = ⎨
        ⎩ s_low (e.g., black),   otherwise

Purpose: Extract only specific gray levels, suppress everything else
```

**Mathematical Formulation (Without Retention):**
```
s = ⎧ L-1,  if r_low ≤ r ≤ r_high    (display white)
    ⎨ 0,    otherwise                (display black)
    ⎩
```

**Intensity Range Definition:**
```
Region of interest: [r_low, r_high]
r_low = lower gray level threshold
r_high = upper gray level threshold

Thickness of slice = r_high - r_low
```

**Example: Highlighting Dark Regions**
```
r_low = 0, r_high = 85

Pixels with intensity [0, 85] → displayed as white (255)
Pixels with intensity (85, 255] → displayed as black (0)

Effect: Isolates dark regions for analysis
```

**Example: Highlighting Bright Regions**
```
r_low = 170, r_high = 255

Pixels with intensity [170, 255] → displayed as white (255)
Pixels with intensity [0, 170) → displayed as black (0)

Effect: Isolates bright regions for analysis
```

**With Background Retention Formula:**
```
s = ⎧ L-1,  if r_low ≤ r ≤ r_high    (highlight range)
    ⎨ r,    otherwise                (keep original)
    ⎩
```

**Slicing Band Definition:**
```
If slicing a narrow band:
r_low = 100, r_high = 120
Band width = 20 gray levels

Pixels in [100, 120] highlighted
All others retained or suppressed based on approach
```

**Multiple Slicing Bands:**
```
s = ⎧ L-1,  if r∈[r₁_low, r₁_high] OR r∈[r₂_low, r₂_high]
    ⎨ 0,    otherwise
    ⎩

Allows highlighting multiple non-contiguous intensity ranges
```

**Graphical Representation:**
```
Intensity [0]---[r_low]---[r_high]---[255]
              |  SLICE  |
              
Without retention: Only slice shown as white
With retention: Slice white, rest shown at original value
```

**Mathematical Representation (Lookup Table):**
```
LUT[0..r_low-1] = 0
LUT[r_low..r_high] = 255
LUT[r_high+1..255] = 0

For each pixel:
output = LUT[intensity]
```

**Characteristics:**
→ Binary or selective output
→ Isolates specific intensity ranges
→ Non-reversible operation (information loss)
→ Simple threshold-based operation
→ Fast implementation

**Applications:**
- Medical image analysis (isolating tissue types)
- Object detection (specific intensity objects)
- Quality control (defect detection at specific gray levels)
- Industrial inspection
- Document analysis
- Thermal imaging
- Microscopy image analysis

**Parameters:**
- r_low: Lower threshold of slice
- r_high: Upper threshold of slice
- Retention mode: With or without background

**Advantages:**
- Simple to implement
- Fast computation
- User-adjustable parameters
- Effective for targeted analysis
- No complex calculations

**Limitations:**
- Loses information outside slice
- Requires prior knowledge of target intensity range
- Binary output loses gradation
- Not suitable for continuous tone analysis

---

### Topic 15: Bit Plane Slicing

**Definition:**
Bit plane slicing decomposes a grayscale image into its constituent bit planes (binary layers), where each bit plane represents a specific bit position in the pixel's binary representation.

**Bit Position Definition:**
```
For 8-bit pixel value:
Bit 7 (MSB):   2^7 = 128
Bit 6:         2^6 = 64
Bit 5:         2^5 = 32
Bit 4:         2^4 = 16
Bit 3:         2^3 = 8
Bit 2:         2^2 = 4
Bit 1:         2^1 = 2
Bit 0 (LSB):   2^0 = 1

Total: 128+64+32+16+8+4+2+1 = 255
```

**Bit Extraction Formula:**
```
Bit_plane_k = (r >> k) & 1

Where:
- >> = right shift operator
- & = bitwise AND operator
- k = bit position (0-7)

Result: Binary value (0 or 1) for bit position k
```

**Example: Extracting Bit Planes from Pixel Value 179**
```
179 in binary: 10110011

Bit 7 (MSB): (179 >> 7) & 1 = (1) & 1 = 1
Bit 6:       (179 >> 6) & 1 = (2) & 1 = 0
Bit 5:       (179 >> 5) & 1 = (5) & 1 = 1
Bit 4:       (179 >> 4) & 1 = (11) & 1 = 1
Bit 3:       (179 >> 3) & 1 = (22) & 1 = 0
Bit 2:       (179 >> 2) & 1 = (44) & 1 = 0
Bit 1:       (179 >> 1) & 1 = (89) & 1 = 1
Bit 0 (LSB): (179 >> 0) & 1 = (179) & 1 = 1

Binary plane: 10110011 (matches original)
```

**Image Reconstruction from Bit Planes:**
```
Original image = Σ(Bit_plane_k × 2^k) for k = 0 to 7

reconstructed = Bit7×128 + Bit6×64 + Bit5×32 + Bit4×16 
              + Bit3×8 + Bit2×4 + Bit1×2 + Bit0×1
```

**Binary Display of Bit Plane k:**
```
For display (0-255 range):
Display_value = Bit_plane_k × 255

If Bit_plane_k = 1: Display as white (255)
If Bit_plane_k = 0: Display as black (0)

Result: Binary image of specific bit plane
```

**Significance of Bit Planes:**
```
Higher-order bits (7, 6, 5, 4):
- Contribute most to image structure
- Visible detail, main features
- Major intensity variations
- Important for perception

Lower-order bits (3, 2, 1, 0):
- Finer details, texture
- Subtle intensity variations
- More susceptible to noise
- Can reveal hidden data
```

**Characteristics:**
→ Decomposes image into binary layers
→ 8 bit planes for 8-bit grayscale image
→ Progressive loss of detail from MSB to LSB
→ Reversible operation (can reconstruct)
→ Important for data analysis and compression

**Binary Representation Matrix:**
```
For M×N image with P bit planes:
Each bit plane is M×N binary matrix
Total storage: M × N × 8 bits
Original image storage: M × N × 8 bits (same)
```

**Information Content:**
```
Bit plane 7 (MSB): ~Carries ~93.3% of image information
Bit plane 6:       ~Carries ~3.1% additional information
Bit plane 5:       ~Carries ~1.6% additional information
...
Bit plane 0 (LSB): ~Carries noise and least information
```

**Partial Reconstruction:**
```
Reconstruct from planes [7, 6, 5, 4] only:
s = Bit7×128 + Bit6×64 + Bit5×32 + Bit4×16

Result: Approximation using 4 most significant planes
Data compression: Uses 50% of original bits
Quality: Usually acceptable for most purposes
```

**Reconstruction Error Calculation:**
```
Error = Σ(Discarded_bits × 2^k)
       = Bit3×8 + Bit2×4 + Bit1×2 + Bit0×1

Maximum error using 4 MSBs: 8+4+2+1 = 15
Maximum relative error: 15/255 ≈ 5.9%
```

**Applications:**
- Image compression (discard LSBs)
- Feature extraction
- Image segmentation
- Texture analysis
- Steganography (hiding data in LSBs)
- Noise analysis (concentrate noise in LSBs)
- Image quality assessment
- Document analysis

**Steganography Example:**
```
Original message bits stored in LSB of image:
Image pixel = 10110010 (original)
Message bit = 1 (to hide)
Result = 10110011 (imperceptible change)

To extract message:
Read Bit0 of each pixel
Reconstruct message from collected bits
```

**Image Compression Technique:**
```
Keep MSBs, discard LSBs:
8 bits → 4 bits: 50% compression
8 bits → 6 bits: 25% compression
8 bits → 7 bits: 12.5% compression

Trade-off: Compression vs. Quality
```

**Characteristics of Each Plane:**
```
Plane 7: Clear structure, main features
Plane 6: Detailed structure, boundaries
Plane 5: Fine details, textures
Plane 4: Texture details
Plane 3: Subtle variations, noise beginning
Plane 2: Mostly noise
Plane 1: Noise-like patterns
Plane 0: Random noise (LSB)
```

---

## FREQUENCY DOMAIN METHODS (Topics 16-21)

### Topic 16: Frequency Domain

**Definition:**
Frequency domain represents images as combinations of frequency components. Transformation from spatial domain to frequency domain performed using Fourier Transform.

**Fundamental Concept:**
Any spatial image can be decomposed into sum of sinusoidal functions of varying frequencies.

**Fourier Transform (2D):**
```
F(u, v) = ∫∫ f(x, y) × e^(-i2π(ux + vy)) dx dy

Where:
- f(x, y) = spatial domain image
- F(u, v) = frequency domain representation
- u, v = frequency variables
- i = imaginary unit
- e^(-i2π(ux+vy)) = complex exponential (basis functions)
```

**Discrete Fourier Transform (DFT):**
```
F(u, v) = (1/MN) × Σ Σ f(x, y) × e^(-i2π(ux/M + vy/N))

where:
x = 0 to M-1, y = 0 to N-1
u = 0 to M-1, v = 0 to N-1
M × N = image dimensions
```

**Inverse DFT:**
```
f(x, y) = Σ Σ F(u, v) × e^(i2π(ux/M + vy/N))

Reconstructs spatial image from frequency components
```

**Fast Fourier Transform (FFT):**
```
Efficient algorithm for computing DFT
Time complexity: O(N log N) instead of O(N²)
Reduces computation from hours to milliseconds
Standard implementation: Cooley-Tukey algorithm
```

**Frequency Components:**
```
Low frequencies (u, v near 0):
- Represent overall image structure
- Contain most image energy
- Correspond to smooth regions

High frequencies (u, v large):
- Represent sharp variations, edges
- Contain less energy
- Correspond to detail and edges
```

**Magnitude Spectrum:**
```
|F(u, v)| = √(Real² + Imaginary²)

Represents amplitude of each frequency component
Displayed as image showing frequency content
Bright pixels = high frequency energy
Dark pixels = low frequency energy
```

**Phase Spectrum:**
```
∠F(u, v) = arctan(Imaginary / Real)

Represents phase angle of each frequency component
Critical for image reconstruction
Less visually informative than magnitude
```

**Power Spectrum:**
```
P(u, v) = |F(u, v)|²

Represents power (energy) at each frequency
Used for frequency analysis
Logarithmic display: log(1 + |F(u, v)|) for visibility
```

**Spectrum Centering:**
```
Raw DFT output:
- Zero frequency at corners
- High frequencies scattered

Centered spectrum:
- Zero frequency at center
- Radial frequency arrangement
- More intuitive visualization

Implementation: Multiply by (-1)^(x+y) before FFT
or use FFT shift function
```

**Frequency Coordinates:**
```
Distance from center: D(u, v) = √(u² + v²)

D = 0: DC component (average image intensity)
Small D: Low frequencies (smooth regions)
Large D: High frequencies (edges, details)
```

**Convolution Theorem:**
```
Spatial convolution = Frequency multiplication

f(x, y) * h(x, y) ↔ F(u, v) × H(u, v)

Benefit: 
- Multiplication faster than convolution for large kernels
- FFT approach: O(N log N) vs. O(N²) for direct convolution
```

**Filtering in Frequency Domain:**
```
1. Input image f(x, y)
2. Apply FFT: F(u, v) = FFT(f)
3. Design filter H(u, v)
4. Apply filter: G(u, v) = H(u, v) × F(u, v)
5. Apply IFFT: g(x, y) = IFFT(G)
6. Output image g(x, y)
```

**Advantages of Frequency Domain:**
- Efficient for large kernels
- Intuitive understanding of image content
- Easy filter design and modification
- Fast global operations
- Straightforward implementation

**Disadvantages:**
- Requires FFT computation
- Circular convolution boundary effects
- Loss of spatial localization
- Complex-valued outputs
- More difficult interpretation for some applications

**Applications:**
- Image filtering (low/high pass)
- Image compression
- Pattern recognition
- Texture analysis
- Noise reduction
- Image enhancement
- Motion detection

---

### Topic 17: Low Pass Filter

**Definition:**
Low pass filter attenuates high frequencies while preserving low frequencies, resulting in image smoothing and blur.

**Purpose:**
- Reduce high-frequency noise
- Smooth image texture
- Blur details and edges
- Remove fine details

**Ideal Low Pass Filter (ILPF):**
```
H(u, v) = 1,     if D(u, v) ≤ D₀
H(u, v) = 0,     if D(u, v) > D₀

Where:
- D(u, v) = √(u² + v²) = distance from center
- D₀ = cutoff frequency
```

**Cutoff Frequency Selection:**
```
D₀ large: Preserve more high frequencies (less blur)
D₀ small: Remove more high frequencies (more blur)
D₀ = 0: Completely black image (extreme blur)
D₀ = ∞: Original image (no smoothing)
```

**Magnitude Response of ILPF:**
```
Ideal Low Pass Filter produces characteristic shape:
Constant = 1 inside radius D₀
Sharp drop to 0 outside radius D₀
Sharp transition (ideal, unrealistic)
```

**Problem with Ideal Filter:**
```
Sharp frequency cutoff creates ringing artifacts
Spatial domain equivalent has side lobes
Results in visible ripples around edges (Gibbs phenomenon)
```

**Filter Implementation (Frequency Domain):**
```
1. Input image f(x, y)
2. Pad image to size ≥ 2M × 2N
3. Compute FFT: F(u, v)
4. Apply ILPF: G(u, v) = H(u, v) × F(u, v)
5. Compute IFFT: g(x, y) = IFFT(G)
6. Extract original region (M × N)
```

**Spatial Domain Implementation (Convolution):**
```
Kernel size determines smoothing extent
3×3 kernel: Light smoothing
5×5 kernel: Moderate smoothing
7×7 kernel: Heavy smoothing

Gaussian kernel example (3×3):
[1  2  1]
[2  4  2] / 16
[1  2  1]
```

**Mathematical Relationship:**
```
Frequency domain filtering:
g(x, y) = f(x, y) * h(x, y)

where h(x, y) is spatial kernel corresponding to H(u, v)

For ideal LPF:
h(x, y) = sinc function (causes ringing)
sinc(x) = sin(πx) / (πx)
```

**Cutoff Frequency Parameter (D₀):**
```
Small D₀ (e.g., 10):
- Strong blur
- Removes fine details
- High smoothing effect

Large D₀ (e.g., 100):
- Weak blur
- Preserves details
- Low smoothing effect

Relationship: Larger D₀ = Less blurring
```

**Applications:**
- Noise reduction
- Image smoothing
- Pre-processing for downsampling
- Aliasing prevention
- Image blur effects
- Preprocessing before edge detection
- Preparation for feature extraction

**Effects on Different Image Components:**
```
Smooth regions: Minimally affected
Fine details: Removed or blurred
Edges: Blurred or softened
Noise: Reduced (noise is high frequency)
```

**Frequency Analysis:**
```
Original image spectrum: Contains all frequencies [0, ∞)
After low pass filter: Only frequencies [0, D₀] preserved
Removed frequencies: (D₀, ∞)

Energy reduction: Some image energy lost
Edge blurring: High-frequency edges attenuated
Contrast reduction: Overall contrast decreased
```

---

### Topic 18: High Pass Filter

**Definition:**
High pass filter attenuates low frequencies while preserving high frequencies, resulting in edge enhancement and detail sharpening.

**Purpose:**
- Enhance edges and fine details
- Sharpen images
- Detect edges and boundaries
- Highlight rapid intensity changes
- Remove smooth variations (DC components)

**Ideal High Pass Filter (IHPF):**
```
H(u, v) = 0,     if D(u, v) ≤ D₀
H(u, v) = 1,     if D(u, v) > D₀

Where:
- D(u, v) = √(u² + v²) = distance from center
- D₀ = cutoff frequency
```

**Relationship with Low Pass:**
```
H_highpass(u, v) = 1 - H_lowpass(u, v)

They are complementary filters
```

**Cutoff Frequency Selection:**
```
D₀ large: Preserve more low frequencies (less sharpening)
D₀ small: Remove more low frequencies (more sharpening)
D₀ → 0: Enhance all details (noise amplification)
```

**Magnitude Response of IHPF:**
```
Characteristic shape:
Sharp rise from 0 to 1 at frequency D₀
Constant = 1 for frequencies > D₀
Sharp transition (ideal, unrealistic)
```

**Filter Implementation (Frequency Domain):**
```
1. Input image f(x, y)
2. Pad image to size ≥ 2M × 2N
3. Compute FFT: F(u, v)
4. Apply IHPF: G(u, v) = H(u, v) × F(u, v)
5. Compute IFFT: g(x, y) = IFFT(G)
6. Extract original region
```

**High Pass Sharpening Effect:**
```
For edge pixels (rapid intensity change):
Frequency content high
Filter passes these components
Result: Edge enhancement

For smooth pixels (slow intensity change):
Frequency content low
Filter suppresses these components
Result: Minimal change to smooth areas
```

**Spatial Domain Kernels for High Pass:**
```
Roberts operator (2×2):
[-1  0]  and  [0  -1]
[0   1]       [1   0]

Sobel operator (3×3):
[-1 -2 -1]
[0   0  0]
[1   2  1]

Laplacian (3×3):
[0  -1  0]
[-1 4  -1]
[0  -1  0]
```

**Sharpening Formula:**
```
Unsharp masking: g(x, y) = f(x, y) + k × [f(x, y) - blur(f(x, y))]

Where:
k = sharpening strength (typically 0.5-2.0)
blur(f) = low pass filtered version
f - blur = high pass filtered version
```

**High Pass Filtered Image Interpretation:**
```
Raw high pass output: Typically gray (near zero)
Edges appear as:
- Dark lines on dark side of edge
- Bright lines on bright side of edge

To enhance visibility:
Add 128 to all pixels: displays as centered image
Edges become clear white/black lines
```

**Frequency Band Selection:**
```
For edge detection: D₀ = small (preserve fine edges only)
For sharpening: D₀ = moderate (preserve some smooth regions)
For detail enhancement: D₀ = variable (adaptive)
```

**Noise Amplification:**
```
High pass filtering amplifies noise
Reason: Noise is high frequency
Solution: Use Butterworth or Gaussian high pass
(smooth transitions reduce noise amplification)
```

**Applications:**
- Image sharpening
- Edge detection
- Feature extraction
- Detail enhancement
- Bone enhancement in medical images
- Document enhancement
- Texture analysis
- Contrast improvement

**Effects on Different Components:**
```
Smooth regions: Suppressed
Edges: Enhanced
Fine details: Enhanced
Noise: Amplified
Overall brightness: Reduced (DC removed)
```

**Relationship to Edge Detection:**
```
High pass filter output ≈ Derivative image
Laplacian (high pass): ∇²f = ∂²f/∂x² + ∂²f/∂y²
Sobel (high pass approximation): Directional derivatives
```

---

### Topic 19: Ideal Filter

**Definition:**
Ideal filter has sharp frequency cutoff, preserving all frequencies within cutoff and completely attenuating frequencies beyond cutoff.

**Ideal Low Pass Filter (ILPF):**
```
H(u, v) = 1,  if D(u, v) ≤ D₀
H(u, v) = 0,  if D(u, v) > D₀
```

**Ideal High Pass Filter (IHPF):**
```
H(u, v) = 0,  if D(u, v) ≤ D₀
H(u, v) = 1,  if D(u, v) > D₀
```

**Ideal Band Pass Filter (IBPF):**
```
H(u, v) = 1,  if D₁ ≤ D(u, v) ≤ D₂
H(u, v) = 0,  otherwise

Where:
D₁ = lower cutoff frequency
D₂ = upper cutoff frequency
```

**Ideal Band Stop (Notch) Filter:**
```
H(u, v) = 0,  if D₁ ≤ D(u, v) ≤ D₂
H(u, v) = 1,  otherwise
```

**Distance Calculation:**
```
Euclidean distance: D(u, v) = √(u² + v²)

For centered frequency domain:
u_c = u - M/2
v_c = v - N/2
D(u_c, v_c) = √(u_c² + v_c²)
```

**Mathematical Characteristics:**
```
Magnitude spectrum:
- Constant 1 (or K) within passband
- Constant 0 outside passband
- Discontinuous jump at cutoff

Phase spectrum:
- Linear (or constant) within passband
- Undefined at discontinuity
```

**Filter in Spatial Domain:**
```
Ideal frequency domain filter
↓ [Inverse Fourier Transform]
Sinc function in spatial domain
h(x, y) = (2πD₀)/(2πD₀)² × sin(2πD₀√(x²+y²)) / √(x²+y²)

Sinc function extends infinitely
Has negative side lobes
```

**Ringing Artifact Problem:**
```
Cause: Sharp frequency cutoff creates sinc function
Side lobes create rings around edges (Gibbs phenomenon)

Manifestation:
- Oscillations near edges
- Loss of sharpness at boundaries
- Visible rings around strong edges

Solution: Use Butterworth or Gaussian filters
(smooth transitions eliminate ringing)
```

**Visualization of Ideal Filter:**
```
Frequency domain:
    1 |-------|
      |       |
    0 |_______|________

    D₀  →  cutoff frequency

Spatial domain:
    +
  0 |    |\  /|  /\  /|\
    |   /  \/ \/  \/ |
   -|_/______________|__
    0    D₀
```

**Cutoff Frequency Definition:**
```
D₀ = radius in frequency domain

In terms of spatial relationships:
D₀ small: Fine spatial details preserved, blur strong
D₀ large: Coarse spatial structure preserved, less blur

Critical frequency D_c = cutoff frequency
Nyquist frequency = D_max (image corner frequency)
```

**Order of Filter:**
```
Ideal filter: Infinite order (discontinuous)
Butterworth: Specified order (n = 1, 2, 3, ...)
Gaussian: Infinite order (smooth)

Higher order → Sharper cutoff → More ringing
Lower order → Gradual cutoff → Less ringing
```

**Advantage of Ideal Filter:**
- Simple mathematical definition
- Easy to understand conceptually
- Exact frequency separation

**Disadvantages of Ideal Filter:**
- Causes ringing artifacts
- Not realizable in practice
- Sharp discontinuities problematic
- Not optimal for most applications

**Comparison with Other Filters:**
```
Ideal:       Sharp cutoff, ringing artifacts
Butterworth: Smooth cutoff, no ringing, trade-off
Gaussian:    Smoothest cutoff, no ringing, gradual transition
```

**Applications (Limited):**
- Theoretical analysis
- Educational purposes
- Baseline comparison
- Mathematical studies

**Practical Use:**
Rarely used in practice; Butterworth or Gaussian filters preferred

---

### Topic 20: Butterworth Filter

**Definition:**
Butterworth filter provides smooth frequency response without ringing artifacts, offering compromise between sharp cutoff and smooth transition.

**Butterworth Low Pass Filter (BLPF):**
```
H(u, v) = 1 / (1 + (D(u, v)/D₀)^(2n))

Where:
- D(u, v) = √(u² + v²) distance from center
- D₀ = cutoff frequency (3dB point)
- n = order of filter (n = 1, 2, 3, ...)
- (2n) appears in denominator
```

**Butterworth High Pass Filter (BHPF):**
```
H(u, v) = 1 / (1 + (D₀/D(u, v))^(2n))

Alternative form:
H(u, v) = 1 - BLPF(u, v)
```

**Mathematical Characteristics:**

**Order n = 1:**
```
H(u, v) = 1 / (1 + (D/D₀)²)

At D = D₀: H = 0.5 (-3dB point)
D >> D₀: H → 0 (gradual roll-off)
D << D₀: H → 1 (flat passband)
```

**Order n = 2:**
```
H(u, v) = 1 / (1 + (D/D₀)⁴)

Sharper cutoff than n=1
At D = D₀: H = 0.5 (-3dB)
Steeper slope
```

**Order n = 3:**
```
H(u, v) = 1 / (1 + (D/D₀)⁶)

Even sharper cutoff
Closer to ideal filter
Still no ringing
```

**General Pattern:**
```
Higher n:
- Sharper frequency cutoff
- Closer to ideal filter
- Smoother transition (no ringing)
- More computational cost

Typical choice: n = 2 or n = 3
Balance between sharpness and smoothness
```

**Magnitude Response Properties:**
```
At frequency D = D₀:
All Butterworth filters: |H(D₀)| = 0.5 (-3dB)

This is defining property regardless of order n
Called -3dB cutoff frequency

For D << D₀: H ≈ 1 (passband)
For D >> D₀: H ≈ (D₀/D)^(2n) (stopband)

Stopband attenuation:
-20n dB/decade (n × 20 dB/decade)
For n=2: -40 dB/decade
For n=3: -60 dB/decade
```

**Spatial Domain Filter:**
```
Butterworth filter inverse Fourier transform
Results in spatial kernel:
- Smooth, well-behaved function
- No significant side lobes
- No ringing artifacts
- Efficient computation
```

**Filter Design Procedure:**
```
1. Specify D₀ (cutoff frequency)
2. Specify n (filter order)
3. For each (u, v), calculate:
   D(u, v) = √(u² + v²)
4. Calculate H(u, v) using formula
5. Apply to frequency spectrum: G = H × F
6. IFFT to get filtered image
```

**Practical Cutoff Frequency Selection:**
```
D₀ = 10-50: Strong filtering
D₀ = 50-100: Moderate filtering
D₀ = 100+: Light filtering

D₀ ≈ image_size/10 is typical starting point
```

**Order Selection:**
```
n = 1: Very smooth roll-off (wide transition)
n = 2: Moderate (typical choice)
n = 3: Sharp roll-off (narrow transition)
n ≥ 4: Very sharp (approaches ideal)
```

**Advantages of Butterworth:**
- No ringing artifacts
- Smooth frequency response
- Well-defined cutoff frequency
- Efficient computation
- Mathematical elegance

**Disadvantages:**
- Not as sharp cutoff as ideal
- Some overshoot possible
- May blur edges more than ideal

**Applications:**
- General image smoothing
- Noise reduction
- Pre-processing for detection
- Image enhancement
- Photography post-processing

**Comparison:**
```
Ideal:       Sharp cutoff, ringing
Butterworth: Smooth cutoff, no ringing ✓
Gaussian:    Smoothest cutoff, no ringing
```

**Effect on Different Orders:**
```
n=1: Gradual transition (widest)
n=2: Medium transition (typical)
n=3: Sharp transition (narrow)

All without ringing artifacts
```

---

### Topic 21: Gaussian Filter

**Definition:**
Gaussian filter applies Gaussian probability distribution to frequency response, providing smoothest transition and best edge preservation.

**Gaussian Low Pass Filter (GLPF):**
```
H(u, v) = e^(-D²(u,v)/(2σ²))

Where:
- D(u, v) = √(u² + v²) distance from center
- σ = standard deviation (controls bandwidth)
```

**Alternative Formulation (Using Cutoff D₀):**
```
H(u, v) = e^(-D²(u,v)/(2D₀²))

At D = D₀:
H(D₀) = e^(-1/2) ≈ 0.606

Cutoff frequency D₀ is at 60.6% amplitude point
(not -3dB as in Butterworth)
```

**Gaussian High Pass Filter (GHPF):**
```
H(u, v) = 1 - e^(-D²(u,v)/(2σ²))

or

H(u, v) = 1 - e^(-D²(u,v)/(2D₀²))
```

**Band Pass Gaussian Filter:**
```
H(u, v) = e^(-(D(u,v)-D_c)²/(2σ²))

Where:
- D_c = center frequency
- σ = bandwidth
```

**Mathematical Properties:**

**Gaussian in Frequency Domain:**
```
H(u, v) = e^(-D²/(2σ²))

At D = 0:    H = 1 (maximum)
At D = σ:    H = e^(-1/2) ≈ 0.606
At D = 2σ:   H = e^(-2) ≈ 0.135
At D = 3σ:   H = e^(-4.5) ≈ 0.011
At D = ∞:    H → 0
```

**Gaussian in Spatial Domain:**
```
h(x, y) = (1/(2πσ²)) × e^(-(x²+y²)/(2σ²))

Same Gaussian form in both domains
This is unique property of Gaussian

Spatial kernel size ≈ 6σ (contains ~99.7% energy)
Truncated to practical size for computation
```

**Standard Deviation Interpretation:**
```
σ large:
- Wide frequency distribution (smooth)
- Gentle roll-off
- Preserves more frequencies
- Less smoothing in spatial domain

σ small:
- Narrow frequency distribution (sharp)
- Sharp roll-off (still smooth)
- Removes more frequencies
- More smoothing in spatial domain
```

**Relationship to Cutoff Frequency:**
```
Given cutoff D₀ (at 60.6% amplitude):
D₀ = σ

σ = D₀
σ = D₀/√2 (alternative definition)

Relationship varies by definition
Specify D₀ or σ clearly
```

**Butterworth vs. Gaussian Comparison:**
```
At same -3dB cutoff D₀:

Butterworth H(D₀) = 0.5
Gaussian    H(D₀) = 0.606

Gaussian rolls off more gradually
Butterworth has sharper cutoff
But Gaussian still smooth (no ringing)
```

**Advantages of Gaussian:**
- No ringing artifacts
- Smoothest possible transition
- Excellent edge preservation
- Same form in spatial and frequency domains
- Natural mathematical properties
- Optimal for Wiener filtering

**Disadvantages:**
- Not as sharp cutoff as Butterworth
- Requires understanding of σ parameter
- Slightly more computational cost

**Applications:**
- Image smoothing (most common)
- Blur effects
- Gaussian pyramid construction
- Scale space analysis
- Detail-preserving smoothing
- Preprocessing for feature detection
- Medical image filtering
- Photography blur effects

**Spatial Implementation (Gaussian Kernel):**
```
1D Gaussian: G(x) = (1/(σ√(2π))) × e^(-x²/(2σ²))

2D Gaussian kernel (5×5 example with σ=1.0):
[1   4   7   4  1]
[4  16  26  16  4]
[7  26  41  26  7] × (1/273)
[4  16  26  16  4]
[1   4   7   4  1]

Sum of all elements = 273
Normalized to sum = 1
Preserves image brightness
```

**Practical σ Selection:**
```
σ = 0.5: Very light smoothing
σ = 1.0: Standard smoothing (default)
σ = 2.0: Moderate smoothing
σ = 3.0+: Heavy smoothing

Larger σ = More blur effect
```

**Separability Property:**
```
2D Gaussian = 1D Gaussian × 1D Gaussian

H(u,v) = H(u) × H(v)

Computational advantage:
2D convolution → Two sequential 1D convolutions
O(N²) → O(N) complexity
```

**Frequency Domain Equivalence:**
```
Spatial convolution with Gaussian kernel
Equivalent to:
Multiplication by Gaussian in frequency domain

Saves computation for large kernel sizes
```

**Scale Space Theory:**
```
Gaussian pyramid:
Level 0: Original image
Level 1: Convolved with σ=1.0 Gaussian
Level 2: Convolved with σ=2.0 Gaussian
Level 3: Convolved with σ=4.0 Gaussian

Progressive smoothing at different scales
Used for multi-scale feature detection
```

---

## IMAGE SEGMENTATION (Topic 22)

### Topic 22: Image Segmentation

**Definition:**
Image segmentation is the process of dividing a digital image into multiple regions (segments) based on similarity criteria. Each segment represents meaningful objects or areas in the image.

**Overall Goal:**
Partition pixels into groups where:
- Pixels within same group are similar
- Pixels in different groups are dissimilar

**Segmentation Criteria:**
Pixels grouped based on:
1. **Intensity (Gray Level Value)**
2. **Frequency characteristics**
3. **Texture patterns**
4. **Color information**
5. **Spatial proximity**

---

#### **Sub-Topic 22.1: Intensity-Based Segmentation**

**Definition:**
Segment image by grouping pixels with similar intensity values.

**Principle:**
```
Pixels with intensity r grouped together if:
|r₁ - r₂| ≤ threshold

Different intensity ranges → Different segments
```

**Intensity Range Determination:**
```
Find natural clusters in intensity distribution:
Low intensity cluster: [0, I₁) → Segment 1 (dark regions)
Mid intensity cluster: [I₁, I₂) → Segment 2 (mid-gray)
High intensity cluster: [I₂, 255] → Segment 3 (bright regions)
```

**Histogram-Based Approach:**
```
1. Compute histogram h(r) of image
2. Identify peaks (high frequency gray levels)
3. Identify valleys (low frequency gray levels)
4. Valleys mark threshold values for segmentation
5. Pixels assigned to nearest peak cluster
```

**Thresholding-Based Segmentation:**
```
Binary segmentation:
Segment_1: {(x,y) | f(x,y) < T}
Segment_2: {(x,y) | f(x,y) ≥ T}

Multi-level:
Segment_1: {(x,y) | f(x,y) < T₁}
Segment_2: {(x,y) | T₁ ≤ f(x,y) < T₂}
Segment_3: {(x,y) | f(x,y) ≥ T₂}
```

**Otsu's Method for Optimal Threshold:**
```
Maximize between-class variance:
σ²_b = ω₁(T) × ω₂(T) × [μ₁(T) - μ₂(T)]²

Where:
ω₁ = proportion of pixels in segment 1
ω₂ = proportion of pixels in segment 2
μ₁ = mean intensity of segment 1
μ₂ = mean intensity of segment 2

Select T maximizing σ²_b
```

**Applications:**
- Binary object-background separation
- Separating tissue types in medical images
- Document analysis (text vs. background)
- Industrial defect detection

---

#### **Sub-Topic 22.2: Gray Level Segmentation**

**Definition:**
Segment image by identifying specific gray level ranges and extracting regions containing those gray levels.

**Basic Concept:**
```
Interest in specific gray levels:
Segment = {(x,y) | g_low ≤ f(x,y) ≤ g_high}

Pixels outside range discarded or marked differently
```

**Multi-Range Segmentation:**
```
Multiple regions of interest:

Segment_1: {(x,y) | g₁_low ≤ f(x,y) ≤ g₁_high}
Segment_2: {(x,y) | g₂_low ≤ f(x,y) ≤ g₂_high}
Segment_3: {(x,y) | g₃_low ≤ f(x,y) ≤ g₃_high}

Non-overlapping ranges
Covers entire gray level range
```

**Gray Level Histogram Analysis:**
```
Histogram shows frequency of each gray level:
Peak regions: High concentration (potential segments)
Valley regions: Low concentration (boundaries)

Segment identified by peaks in histogram
```

**Example: Medical Image Segmentation**
```
Brain tissue classification:
Gray matter: [90, 120] gray levels
White matter: [150, 180] gray levels
CSF: [30, 60] gray levels
Air: [0, 20] gray levels

Each range identified and extracted separately
```

**Connected Component Analysis:**
```
After initial gray level selection:
1. Identify pixels in target gray range
2. Group connected pixels
3. Label each connected component
4. Extract individual objects

Connected = adjacent pixels in 4-connectivity or 8-connectivity
```

**Morphological Post-Processing:**
```
After gray level segmentation:
- Fill small holes within segments
- Remove small isolated regions
- Smooth segment boundaries
- Close gaps in segmentation
```

**Advantages:**
- Simple to understand and implement
- Fast computation
- User-defined gray level ranges
- Effective for uniform regions

**Limitations:**
- Doesn't consider spatial relationships
- Poor for low-contrast images
- Sensitive to noise
- Difficulty with overlapping gray levels

---

#### **Sub-Topic 22.3: Frequency-Based Segmentation**

**Definition:**
Segment image by analyzing frequency domain characteristics, separating regions with different frequency content.

**Principle:**
```
Different regions have different frequency characteristics:
Smooth regions: Dominated by low frequencies
Textured regions: Contain high frequencies
Edge regions: Sharp frequency transitions
```

**Frequency Domain Filtering:**
```
1. Transform image to frequency domain (FFT)
2. Extract frequency characteristics in local regions
3. Classify regions based on frequency content
4. Create segmentation map
```

**Band Pass Frequency Analysis:**
```
Extract specific frequency bands:

Low frequency band: F_low = LPF(image)
Represents smooth, overall structure

Mid frequency band: F_mid = extracted intermediate frequencies
Represents texture and patterns

High frequency band: F_high = HPF(image)
Represents edges and fine details

Segmentation based on band dominance
```

**Texture Segmentation via Frequency:**
```
Periodic texture: Sharp peaks in frequency domain
Random texture: Distributed frequency energy
Smooth region: Concentrated low-frequency energy

Classify regions by frequency distribution pattern
```

**Wavelet-Based Segmentation:**
```
Decompose image into frequency and scale:
Coarse scale (low frequency): Overall structure
Medium scale: Texture patterns
Fine scale (high frequency): Details and edges

Combine information across scales for segmentation
```

**Filter Bank Approach:**
```
Apply bank of filters at multiple frequencies:
Each filter responds differently to different regions
Combination of responses → Segmentation features
Classify based on filter response pattern
```

**Applications:**
- Texture segmentation
- Document analysis
- Defect detection (deviations from expected frequency)
- Pattern recognition
- Material classification

**Advantages:**
- Sensitive to periodic patterns
- Captures texture information
- Global view of frequency content
- Robust to local variations

**Limitations:**
- Computationally expensive
- Complex implementation
- Requires understanding of frequency characteristics
- Boundary detection difficult

---

#### **Sub-Topic 22.4: Pixel Value-Based Segmentation**

**Definition:**
Segment image by grouping pixels with similar values, considering pixel intensity magnitude without regard to spatial location.

**Basic Approach:**
```
Feature vector per pixel: f = [intensity, color, texture, ...]

Distance metric: d(f₁, f₂) measures pixel similarity

Segmentation groups pixels with d < threshold
```

**K-Means Clustering:**
```
Algorithm:
1. Initialize K cluster centers randomly
2. Assign each pixel to nearest cluster center
3. Recalculate cluster centers as mean of assigned pixels
4. Repeat steps 2-3 until convergence

Output: Segmentation map with K segments
```

**K-Means Distance Formula:**
```
Assign pixel p to cluster i if:
d(p, center_i) = min(d(p, center_j)) for all j

Euclidean distance:
d(p, c) = √(Σ(p_k - c_k)²) for all feature dimensions k
```

**Fuzzy C-Means:**
```
Softer assignment than K-means
Each pixel has membership degree (0 to 1) in each cluster

Membership μᵢⱼ ∈ [0,1]
Σ μᵢⱼ = 1 (sum of memberships = 1)

Pixel belongs partially to multiple clusters
```

**Histogram Quantization:**
```
Simplest pixel-value segmentation:
1. Reduce gray level resolution
2. Quantize 256 levels to K levels
3. Original: 8-bit = 256 levels
   Quantized: log₂(K) bits = K levels

For K=4: Quantize 256 levels to 4 levels
Quantized_level = round(r × (K-1) / 255)
```

**Color-Based Segmentation (RGB):**
```
For color images, pixel value = [R, G, B]
Vector distance:
d([R₁,G₁,B₁], [R₂,G₂,B₂]) = √((R₁-R₂)² + (G₁-G₂)² + (B₁-B₂)²)

Segment pixels with similar color vectors
```

**Statistical Clustering:**
```
Gaussian Mixture Models (GMM):
Assume pixels drawn from mixture of Gaussians
Each Gaussian = one segment

EM algorithm:
E-step: Assign pixels to most likely Gaussian
M-step: Update Gaussian parameters

Iteratively refine until convergence
```

**Applications:**
- Color-based object detection
- Skin detection
- Object recognition
- Leaf/plant phenotyping
- Anomaly detection

**Advantages:**
- Flexible for multi-dimensional features
- Effective for distinct clusters
- Can incorporate multiple features
- Well-established algorithms

**Limitations:**
- Must specify number of clusters K
- Sensitive to outliers
- Initialization dependent
- Computationally expensive for large images

---

## SUMMARY TABLE: 22 TECHNIQUES

| Topic | Method | Input | Output | Primary Use |
|-------|--------|-------|--------|-------------|
| 1 | Spatial Domain | Pixel (x,y) | Modified pixel | Point operations |
| 2 | Linear Transform | Intensity r | s = ar+b | Brightness/contrast |
| 3 | Point Operation | Pixel intensity | Transformed intensity | Lookup table |
| 4 | Digital Negative | Pixel r | 255-r | Photographic negative |
| 5 | Non-linear Transform | Intensity | Curved mapping | Flexible enhancement |
| 6 | Square Function | Intensity r | r² | Darkening |
| 7 | Square Root | Intensity r | √r | Brightening shadows |
| 8 | Logarithmic | Intensity r | log(1+r) | Dynamic range compression |
| 9 | Exponential | Intensity r | e^r | Darkening (limited) |
| 10 | Power Function | Intensity r | r^γ | Gamma correction |
| 11 | Gamma Correlation | Intensity | Corrected intensity | Display calibration |
| 12 | Piecewise Linear | Intensity | Multi-segment transform | Custom curves |
| 13 | Contrast Stretching | Narrow range | Full range [0,255] | Low-contrast images |
| 14 | Gray Level Slicing | Intensity range | Binary/highlighted | ROI extraction |
| 15 | Bit Plane Slicing | Bit position | Binary plane | Compression/analysis |
| 16 | Frequency Domain | Spatial image | Frequency spectrum | FFT analysis |
| 17 | Low Pass Filter | Frequency spectrum | Smooth image | Noise reduction |
| 18 | High Pass Filter | Frequency spectrum | Sharp image | Edge enhancement |
| 19 | Ideal Filter | Spectrum | Filtered spectrum | Theoretical |
| 20 | Butterworth | Spectrum | Smooth filtered spectrum | Practical smoothing |
| 21 | Gaussian | Spectrum | Smoothest filtered spectrum | Optimal smoothing |
| 22 | Image Segmentation | Intensity/frequency | Labeled regions | Object extraction |

---

## CONCLUSION

These 22 image processing techniques form the foundation of modern digital image enhancement, analysis, and manipulation. Understanding spatial domain operations (topics 1-15) provides intuitive grasp of image modification. Frequency domain methods (topics 16-21) enable efficient filtering and analysis. Segmentation (topic 22) bridges visual understanding and computational image processing.

Mastery of these techniques enables development of sophisticated image processing pipelines for forensic analysis, medical imaging, surveillance, quality control, and countless applications in digital forensics and biometric systems.