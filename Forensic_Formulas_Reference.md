# FORENSIC SCIENCE - QUICK REFERENCE FORMULAS & KEY CONCEPTS
## College-Level Examination Support Material

---

## UNIT 1: SOUND FORENSICS - KEY FORMULAS & CONSTANTS

### Wave Physics Fundamental Relationships
\(v = f \times \lambda\)
- v = wave velocity (m/s)
- f = frequency (Hz)
- λ = wavelength (meters)

**Temperature Dependency of Sound Speed:**
\(v_w = (331 \text{ m/s}) \times \sqrt{\frac{T}{273 \text{ K}}}\)
- At 20°C: v ≈ 343 m/s
- At 0°C: v ≈ 331 m/s
- At 37°C (body temperature): v ≈ 354 m/s

### Human Speech Frequencies
• **Fundamental Frequency (F0):**
  - Adult males: 80-120 Hz (average 100 Hz)
  - Adult females: 150-250 Hz (average 200 Hz)
  - Children: 200-300 Hz (average 250 Hz)

• **Formant Frequencies:**
  - F1 (vowel height): 200-900 Hz
  - F2 (vowel position): 500-2,500 Hz
  - F3 (articulation detail): 2,000-4,000 Hz
  - F4 (higher harmonics): 3,500-4,500 Hz

• **Speech Rate:** 3-5 syllables per second (normal conversation)
• **Articulation Rate:** 5-7 syllables per second (excluding pauses)
• **Phonation-Time Ratio:** Typically 0.60-0.80 (60-80% speaking vs. silence)

### Mel-Frequency Cepstral Coefficients (MFCC)
MFCC computation steps:
1. Apply pre-emphasis filter
2. Frame-wise FFT computation
3. Mel-scale frequency warping: \(f_{mel} = 2595 \log_{10}(1 + \frac{f}{700})\)
4. Triangular filter bank application (typically 40 filters)
5. DCT (Discrete Cosine Transform) of log power spectrum
6. Extract MFCC coefficients (typically 12-13 coefficients)

### Spectrographic Analysis Time-Frequency Relationship
**Short-Time Fourier Transform (STFT):**
\(X[n, k] = \sum_{m=0}^{N-1} x[m] \times w[n-m] \times e^{-j2\pi km/N}\)
- Window length: typically 20-50 ms
- Hop size: typically 10 ms
- Frequency resolution: ~20 Hz for 20 ms window at 8 kHz sampling

### Likelihood Ratio Calculation (Speaker Identification)
\(LR = \frac{P(\text{Evidence} | \text{Suspect is speaker})}{P(\text{Evidence} | \text{Random person is speaker})}\)

**Interpretation Scale (ENFSI Guidelines):**
- LR < 1: Evidence supports non-match
- LR 1-10: Limited support for match
- LR 10-100: Moderate support for match
- LR 100-1,000: Strong support for match
- LR > 1,000: Very strong support for match

---

## UNIT 2: BRAIN FINGERPRINTING - KEY PARAMETERS & STANDARDS

### P300 Component Specifications
• **Latency:** 300-400 milliseconds post-stimulus (hence "P300")
• **Peak Amplitude:** 5-10 microvolts (μV) for recognized stimuli
• **Scalp Distribution:** Maximum at central and parietal regions (Cz, Pz)
• **Polarity:** Positive (hence "P" in P300)
• **Duration:** ~100-200 ms from peak onset to return to baseline

### Brain Fingerprinting Accuracy Parameters
• **Sensitivity (True Positive Rate):** 88-95%
• **Specificity (True Negative Rate):** 90-98%
• **Accuracy in controlled conditions:** 93-99%
• **Accuracy with field-grade recordings:** 85-92%

### Electrode Specifications (10-20 System)
**Total electrodes typically used:** 19-32 electrodes
**Standard reference positions:**
- Reference electrodes: A1, A2 (mastoid processes)
- Ground electrode: Fpz or AFz
- Common layout:
  - Frontal (4): Fp1, Fp2, F3, F4
  - Fronto-central (1): Fz
  - Central (4): C3, C4, T3, T4
  - Centro-parietal (2): Cz, Pz
  - Parietal (4): P3, P4, T5, T6
  - Occipital (2): O1, O2

### EEG Recording Parameters
• **Sampling rate:** 500-1000 Hz minimum
• **Filter settings:** 0.1 Hz high-pass, 100 Hz low-pass
• **Impedance:** <5,000 Ohms per electrode
• **Recording duration per stimulus category:** 2-4 minutes
• **Number of stimuli per category:** 20-40 presentations
• **Inter-stimulus interval:** 3-5 seconds

### Brain Fingerprinting Test Validity Factors
\(\text{Stimulation Information} = \frac{P300_{\text{Crime-Relevant}} - P300_{\text{Irrelevant}}}{P300_{\text{Crime-Relevant}} + P300_{\text{Irrelevant}}}\)

**Interpretation:**
- > +3.0: Information Present (guilty knowledge)
- -3.0 to +3.0: Inconclusive
- < -3.0: Information Absent (no guilty knowledge)

---

## UNIT 3: FORENSIC FACIAL RECONSTRUCTION - MEASUREMENTS & PROPORTIONS

### Soft Tissue Thickness Database Values (in millimeters)

**Male Measurements:**
| Anatomical Point | Thickness (mm) | Reference |
|---|---|---|
| Glabella (forehead) | 6-8 | FARO, IDENTITAS |
| Nasion (bridge of nose) | 5-7 | Standard |
| Nasal tip | 7-9 | Rhinion +1mm |
| Subnasale (below nose) | 9-11 | Critical point |
| Upper lip | 10-12 | Labial height |
| Lower lip | 8-10 | Lip thickness |
| Pogonion (chin) | 10-12 | Mandibular |
| Mentale (mental eminence) | 8-10 | Chin point |
| Angle of mandible | 14-16 | Bilateral |
| Zygoma (cheekbone) | 12-14 | Zygomatic arch |
| Frontal bone | 5-7 | Forehead area |

**Female Measurements (typically 10-15% thinner):**
| Anatomical Point | Thickness (mm) |
|---|---|
| Glabella | 5-7 |
| Nasion | 4-6 |
| Nasal tip | 6-8 |
| Subnasale | 8-10 |
| Upper lip | 9-11 |
| Lower lip | 7-9 |
| Pogonion | 8-10 |

### Age Correction Factors
**Juvenile (5-12 years):**
- Apply 80-90% of adult values
- Facial features more proportional

**Adolescent (13-17 years):**
- Apply 90-95% of adult values
- Growth plates still visible

**Adult (18-50 years):**
- Use standard database values
- Maximum facial development

**Elderly (50+ years):**
- Apply 95-110% of adult values
- Account for tissue sagging and loss of elasticity

### Ancestry-Specific Characteristics
**African Ancestry:**
- Larger orbital aperture
- Wider nasal aperture
- Thicker nasal tissues
- More prominent zygoma

**European Ancestry:**
- Narrower nasal aperture
- Higher nasal bridge
- Smaller orbital aperture

**East Asian Ancestry:**
- Moderate orbital aperture
- Narrower nasal aperture
- Shovel-shaped incisors

**South Asian Ancestry:**
- Moderate to large orbital aperture
- Medium nasal aperture
- Variable soft tissue thickness

### Key Facial Ratios
**Neoclassical Canons (used for validation):**
- Facial height : Width ratio: 1.3 : 1 (ideal)
- Inter-ocular distance : Orbital width ratio: 0.5
- Bizygomatic width : Facial height ratio: 0.7-0.8
- Mandibular width : Bizygomatic width ratio: 0.6-0.8

### Craniofacial Superimposition Accuracy Thresholds
- **Positive identification:** ±1% linear mismatch in facial height
- **Consistent with identity:** ±3-5% mismatch with minor discrepancies
- **Inconclusive:** ±5-8% mismatch with multiple discrepancies
- **Exclusion:** >8% mismatch or multiple characteristic differences

---

## UNIT 4: BLOODSTAIN PATTERN ANALYSIS - CALCULATIONS & CONVERSIONS

### Impact Angle Calculation
\(\sin(\theta) = \frac{\text{width of stain tail}}{\text{length of main stain body}}\)

**Angle Determination Examples:**
- sin(θ) = 0.26 → θ = 15° (very shallow angle)
- sin(θ) = 0.50 → θ = 30° (shallow angle)
- sin(θ) = 0.71 → θ = 45° (intermediate angle)
- sin(θ) = 0.87 → θ = 60° (steeper angle)
- sin(θ) = 0.98 → θ = 78° (very steep angle)
- sin(θ) = 1.00 → θ = 90° (perpendicular impact)

### Area of Convergence Calculation
**Two-dimensional (horizontal plane):**
1. For each stain, measure impact angle
2. Project backward trajectory along stain long axis on horizontal surface
3. Plot multiple trajectories from different stains
4. Find intersection point: Area of Convergence

**Mathematical calculation:**
\(\tan(\alpha) = \frac{\text{lateral distance from impact line}}{\text{stain distance from reference}}\)

### Area of Origin Calculation
**Three-dimensional (including height):**
\(h = d \times \tan(\theta)\)
- h = height of origin above surface (meters)
- d = distance from convergence point (meters)
- θ = impact angle (degrees)

**Example calculation:**
- Impact angle: 45°, Distance: 2 meters
- Height = 2 × tan(45°) = 2 × 1.0 = 2 meters above surface
- **Interpretation:** Origin point is 2 meters above the surface at distance 2 meters from convergence point

### Bloodstain Classification by Impact Velocity
| Stain Type | Velocity Range | Droplet Size | Pattern Features |
|---|---|---|---|
| Passive drip | Gravity only | 4-8 mm | Circular, smooth edges |
| Low-velocity | <5 m/s | 1-4 mm | Few satellites, some elongation |
| Medium-velocity | 5-25 m/s | 1-3 mm | Multiple satellites, asymmetric |
| High-velocity | >25 m/s | 0.1-1 mm | Fine mist, widely dispersed |

### Surface Tension and Droplet Formation
**Surface tension of blood:** σ ≈ 0.06 N/m
**Minimum droplet formation velocity:** ~1 m/s
**Droplet size calculation (Weber number):**
\(We = \frac{\rho v^2 d}{\sigma}\)
- ρ = fluid density (~1060 kg/m³ for blood)
- v = velocity (m/s)
- d = characteristic diameter (m)
- σ = surface tension (N/m)

**Critical Weber number for atomization:** We > 12 (causes breakup into smaller droplets)

### Void Pattern Dimensions
**Typical void analysis:**
- Void length × width measurements (cm)
- Object shape comparison with void geometry
- Void location and position relative to other patterns
- Presence of partial voids vs. complete voids

**Calculation of object dimensions from void:**
\(\text{Object dimension} = \sqrt{\text{void area}} \times \text{shape factor}\)
- Shape factor for circular objects: 1.13
- Shape factor for rectangular objects: varies with aspect ratio

---

## UNIT 5: ADVANCED FORENSIC TECHNOLOGIES - SPECIFICATIONS

### Laser Scanning (LiDAR) Specifications
• **Measurement range:** 300+ meters
• **Accuracy:** ±2-5 mm at 10 meters distance
• **Point cloud density:** 1,000-100,000+ points per second
• **Scan coverage:** 360° horizontal, 270° vertical
• **Data file size:** 100-500 MB per scan (varies with density)
• **Processing software:** Autodesk ReCap, CloudCompare, Leica LAS modules

### CBCT (Cone Beam Computed Tomography) Parameters
• **Voxel size:** 0.5-1.0 mm (isotropic)
• **Field of view:** 5-20 cm diameter
• **Scan time:** 10-30 seconds
• **Image quality:** Superior for bone detail
• **Radiation dose:** Lower than medical CT (25-210 μSv)
• **Reconstruction:** Sagittal, coronal, axial, 3D surface

### Carbon Dot Fluorescent Powder Properties
**Particle size:** 2-10 nanometers (nm) diameter
**Quantum Yield (QY):** 35-50% (traditional powders: 10-20%)
**Fluorescence emission:** Blue (450 nm), Green (520 nm), Red (650 nm)
**Excitation wavelength:** 365-405 nm (UV light)
**Fluorescence intensity improvement:** 200-500% vs. traditional powders
**Powder application:** Standard brush method
**Detection time:** Immediate under UV illumination
**Storage stability:** 1-2 years at room temperature (superior to traditional)

### AFIS Fingerprint Database Specifications
• **Database size (US):** >140 million fingerprint records
• **Database size (India):** >1 billion fingerprint records
• **Accuracy rate:** 99%+ for positive matches
• **Search time:** Seconds to minutes for database search
• **Minutiae features extracted:** 50-200 points per fingerprint
• **Comparison algorithms:** FFT-based, minutiae-based, ridge pattern-based
• **False positive rate:** <0.0001% (<1 in million)
• **False negative rate:** 2-5% (miss rate for actual matches)

### AI/ML Accuracy Benchmarks in Forensics
| Application | Accuracy | Technology |
|---|---|---|
| Fingerprint identification | 99.5%+ | AFIS with neural networks |
| Facial recognition | 95-99% | Deep learning CNN |
| Speaker identification | 95%+ | i-vector PLDA system |
| Handwriting analysis | 90-95% | Neural networks |
| Iris recognition | 99.9% | Texture analysis |
| Gait recognition | 85-95% | Deep learning CNN |
| Document authentication | 90%+ | Neural networks |

### Spectroscopy Wavelength Ranges
| Technique | Wavelength Range | Applications |
|---|---|---|
| Infrared (IR) | 0.7-300 μm | Paint, fiber, drug analysis |
| UV-Visible | 190-700 nm | Drug detection, ink analysis |
| Near-IR | 700-2500 nm | Fiber composition |
| Raman | Variable scattering | Chemical structure |
| X-ray Fluorescence (XRF) | 0.01-10 nm | Elemental composition |

### Statistical Analysis Methods in Forensics
**Univariate Analysis:**
- Mean, standard deviation, range
- t-tests for comparison of two samples
- ANOVA for comparison of multiple groups

**Multivariate Analysis:**
- Principal Component Analysis (PCA): Dimensionality reduction
- Linear Discriminant Analysis (LDA): Classification
- Logistic Regression: Probability modeling
- K-Nearest Neighbor (KNN): Pattern matching

**Likelihood Ratio:**
\(LR = \frac{P(E|H_p)}{P(E|H_d)}\)
- E = evidence
- Hp = prosecution hypothesis
- Hd = defense hypothesis

---

## IMPORTANT INDIAN LEGAL FRAMEWORK & GOVERNMENT STANDARDS

### Relevant Legal Provisions
**Indian Evidence Act 1872:**
- Section 45: Expert opinion on physical evidence
- Section 27: Admissibility of material discovered through interrogation
- Sections 47-51: Rules regarding expert evidence

**Criminal Procedure Code 1973:**
- Section 225: Application of forensic science
- Section 293: Procedures for collection of evidence

**Supreme Court Landmark Judgment:**
**Selvi v. State of Karnataka (2010)** Criminal Appeal No. 1267 of 2004
- Brain fingerprinting, polygraph, narcoanalysis cannot be forcefully administered
- Results of these tests NOT admissible as primary evidence
- Material discovered during tests IS admissible under Section 27 IEA
- Informed consent MANDATORY for voluntary administration

### Government Initiatives
**National Forensic Infrastructure Enhancement Scheme (2024):**
- Total allocation: ₹2,254.43 crore
- Duration: 2024-25 to 2028-29
- Components:
  - 9 off-campuses of National Forensic Sciences University
  - 7 Central Forensic Science Laboratories
  - Mobile Forensic Vans for all districts
  - National Forensic Data Centre (₹200.16 crore)
  - Training facilities and skilled manpower development

**National Forensic Sciences University (NFSU):**
- Established by Government of India as central agency
- Located in Delhi with regional campuses
- Provides accreditation and training for forensic laboratories
- Develops standardized protocols for forensic analysis

**Central Forensic Science Laboratories (CFSL):**
- Located at: Delhi, Kolkata, Chandigarh, Hyderabad, Mumbai, Pune, Bangalore, Bhopal, Guwahati
- Analyze evidence from state police agencies
- Employ certified forensic scientists

### ISO/IEC 17025 Accreditation
**Standard for forensic laboratory competence:**
- Technical competence of personnel
- Quality assurance procedures
- Equipment calibration and maintenance
- Uncertainty of measurements
- Documentation and record keeping
- Chain of custody requirements

---

## EXAMINATION PREPARATION CHECKLIST

### Unit 1: Sound Forensics
- [ ] Memorize wave equation: v = f × λ
- [ ] Know formant frequency ranges: F1-F4
- [ ] Understand spectrogram generation (FFT, window size, frequency resolution)
- [ ] Practice calculating impact angles from spectral data
- [ ] Know likelihood ratio interpretation scale
- [ ] Understand admissibility requirements in Indian courts

### Unit 2: Brain Fingerprinting
- [ ] Know P300 latency (300-400 ms) and amplitude (5-10 μV)
- [ ] Memorize electrode placement (10-20 system, 19+ electrodes)
- [ ] Understand information present/absent/inconclusive criteria
- [ ] Know Selvi judgment requirements (consent, admissibility)
- [ ] Distinguish brain fingerprinting from polygraph vs. narcoanalysis
- [ ] Know accuracy rates (88-95%)

### Unit 3: Facial Reconstruction
- [ ] Memorize soft tissue thickness values for key anatomical points
- [ ] Know age/sex/ancestry correction factors
- [ ] Understand difference between 2D and 3D reconstruction methods
- [ ] Know craniofacial superimposition accuracy thresholds (±1%)
- [ ] Understand CBCT specifications and advantages
- [ ] Know limitations and presumptive nature of reconstructions

### Unit 4: Bloodstain Pattern Analysis
- [ ] Master angle of impact calculation: sin(θ) = width/length
- [ ] Understand area of convergence vs. area of origin
- [ ] Know height calculation: h = d × tan(θ)
- [ ] Memorize bloodstain types and velocity ranges
- [ ] Understand void patterns and their interpretation
- [ ] Know 3D reconstruction tools (FARO, Hemospat)

### Unit 5: Advanced Technologies
- [ ] Know carbon dot fluorescent powder properties (QY 35-50%)
- [ ] Understand laser scanning specifications (accuracy ±2-5 mm)
- [ ] Know AFIS accuracy (99%+) and database sizes
- [ ] Understand AI/ML applications and accuracy rates (85-99%)
- [ ] Know spectroscopy methods and applications
- [ ] Know government initiatives and accreditation standards

---

## QUICK FACTS FOR RAPID REVIEW

**Sound Physics:**
- Speed of sound in air at 20°C: 343 m/s
- Human hearing range: 20 Hz to 20 kHz
- Forensic speech analysis range: 80-8000 Hz
- Male F0 average: 100 Hz | Female F0 average: 200 Hz

**Brain Fingerprinting:**
- P300 latency: 300-400 ms
- Accuracy: 88-95%
- Selvi ruling (2010): Tests NOT admissible directly
- Consent: MANDATORY
- Key ruling: Section 27 IEA allows discovered material

**Facial Reconstruction:**
- Soft tissue thickness: 5-16 mm at key points
- Accuracy: 85-95% match to photos
- Craniofacial superimposition tolerance: ±1%
- CBCT voxel size: 0.5-1.0 mm

**Bloodstain Analysis:**
- Passive drop size: 4-8 mm
- Low-velocity: 1-4 mm, medium: 1-3 mm
- High-velocity: 0.1-1 mm (mist)
- Impact angle formula: sin(θ) = width/length
- Area of origin height: h = d × tan(θ)

**Advanced Tech:**
- Carbon dot QY: 35-50%
- AFIS accuracy: 99%+
- Laser scan accuracy: ±2-5 mm
- AI accuracy (facial recognition): 95-99%
- National Forensic Infrastructure: ₹2,254.43 crore (2024-29)