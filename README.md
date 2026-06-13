# README

# Computer Vision and Video-Based Vibration Analysis

## Objective

The objective of this project is to explore fundamental image processing and motion analysis techniques through three tasks:

1. Edge Detection
2. Optical Flow Estimation
3. Vibration Mode Analysis using Temporal FFT of Optical Flow

The project demonstrates how motion information can be extracted from images and videos and how frequency-domain analysis can be used to identify the dynamic characteristics of vibrating objects.

The modal analysis portion of this work is inspired by:

**Image-Space Modal Bases for Plausible Manipulation of Objects in Video**
Abe Davis, Justin G. Chen, Frédo Durand
SIGGRAPH Asia 2015

---

# Task 1: Edge Detection

## Objective

The objective of this task is to detect prominent edges within an image.

Edges correspond to locations where image intensity changes rapidly and often represent object boundaries, corners, and important structural features.

## Methodology

The following steps were performed:

1. Convert the image to grayscale.
2. Apply Gaussian smoothing to reduce noise.
3. Compute image gradients using Sobel operators.
4. Calculate gradient magnitude and gradient direction.
5. Apply thresholding to obtain the final edge map.

## Output

The output of this task is an edge image highlighting significant boundaries and structural details present in the original image.

## Significance

Edge detection serves as a fundamental image processing operation and provides insight into image gradients, which are also used in motion estimation techniques such as optical flow.

---

# Task 2: Optical Flow Estimation

## Objective

The objective of this task is to estimate the apparent motion between two video frames using optical flow.

Two frames approximately five frames apart are selected from a video sequence, and the motion field between them is computed.

## Methodology

### Frame Selection

Two frames separated by approximately five frames are extracted from the video.

### Grayscale Conversion

The selected frames are converted to grayscale for processing.

### Optical Flow Computation

The Horn-Schunck Optical Flow Method is used to estimate motion between the two frames.

The method computes:

* Horizontal motion component (u)
* Vertical motion component (v)

for every pixel in the image.

### Flow Visualization

The resulting motion vectors are visualized using a quiver plot, where:

* Arrow direction indicates motion direction.
* Arrow length indicates motion magnitude.

## Outputs

1. Frame 1
2. Frame 2
3. Optical Flow Quiver Plot

## Significance

Optical flow provides a dense motion field describing pixel movement between frames and forms the foundation for subsequent vibration analysis.

---

# Task 3: Modal Analysis Using Temporal FFT

## Objective

The objective of this task is to identify dominant vibration frequencies and corresponding mode shapes directly from video data.

Instead of using physical sensors, vibration information is extracted from optical flow computed between consecutive video frames.

## Methodology

### Video Acquisition

A video containing an object oscillating about its mean position is used.

Examples include:

* Vibrating ruler
* Cantilever beam
* Pendulum
* Tuning fork
* Oscillating wire

The camera should remain stationary while the object vibrates.

### Frame Extraction

The video is decomposed into grayscale frames.

### Optical Flow Computation

Dense optical flow is computed between every pair of consecutive frames using the Farneback Optical Flow algorithm.

For each pixel:

* u(x,y,t) → Horizontal motion
* v(x,y,t) → Vertical motion

These values collectively form the optical flow field.

### Motion Signal Generation

The magnitude of optical flow is calculated as:

Motion Magnitude = √(u² + v²)

The average motion magnitude over all pixels is computed for every frame pair to generate a one-dimensional motion signal.

### Frequency Analysis

Fast Fourier Transform (FFT) is applied to the motion signal.

FFT converts the motion signal from the time domain to the frequency domain and reveals the dominant frequencies present in the vibration.

### Power Spectral Density (PSD)

The Power Spectral Density is computed as:

PSD = |FFT|²

The PSD plot highlights frequencies with significant vibrational energy.

The two largest peaks are selected as the dominant vibration frequencies.

### Temporal FFT of Optical Flow

Following the concepts presented by Davis et al., FFT is applied along the temporal axis of the optical flow fields.

Input dimensions:

Time × Height × Width

After FFT:

Frequency × Height × Width

Each frequency slice corresponds to a vibration mode.

### Mode Shape Extraction

For each dominant frequency:

* X-direction mode shape is extracted from the horizontal flow field.
* Y-direction mode shape is extracted from the vertical flow field.

The magnitude of these frequency-domain flow fields is visualized as mode shapes.

---

# Workflow

Edge Detection

↓

Video Acquisition

↓

Frame Extraction

↓

Grayscale Conversion

↓

Optical Flow Computation

↓

Motion Signal Generation

↓

Fast Fourier Transform (FFT)

↓

Power Spectral Density (PSD)

↓

Dominant Frequency Identification

↓

Temporal FFT of Optical Flow

↓

Mode Shape Extraction

↓

Visualization

---

# Software Requirements

* Python 3.x
* OpenCV
* NumPy
* Matplotlib
* SciPy

---

# Outputs

## Task 1: Edge Detection

* Edge Map

## Task 2: Optical Flow Estimation

* Frame 1
* Frame 2
* Optical Flow Quiver Plot

## Task 3: Modal Analysis

* PSD vs Frequency Plot
* X Mode Shape at Dominant Frequency 1
* Y Mode Shape at Dominant Frequency 1
* X Mode Shape at Dominant Frequency 2
* Y Mode Shape at Dominant Frequency 2

---

# Conclusion

This project demonstrates the progression from basic image processing to advanced video-based motion analysis. Edge detection is used to identify important image structures, optical flow is used to estimate motion between frames, and temporal frequency analysis is used to recover vibration characteristics directly from video data.

The results show that dominant vibration frequencies and corresponding mode shapes can be extracted without physical contact, illustrating the effectiveness of computer vision techniques for structural and dynamic analysis.
