# Image Pixel Manipulator

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manasir747/Image-Pixel-Manipulator/blob/main/Image_Pixel_Manipulator.ipynb)
![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![NumPy](https://img.shields.io/badge/NumPy-Array%20Manipulation-013243.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)

A hands-on, educational guide to fundamental digital image processing and pixel-level manipulation using pure **NumPy** array operations and **Matplotlib** visualization—without relying on heavy computer vision libraries.

---

## 📌 Overview

Images in digital computing are multidimensional arrays of pixel intensity values. This project demonstrates how digital images can be generated from scratch, manipulated, transformed, filtered, and analyzed at the pixel level using standard NumPy array slicing, vectorization, and data type management.

---

## 🚀 Workflow & Key Steps

The interactive notebook ([`Image_Pixel_Manipulator.ipynb`](Image_Pixel_Manipulator.ipynb)) covers five progressive steps:

### 1. Creating a Blank Image
- Initializes a blank $200 \times 200 \times 3$ RGB canvas using `np.zeros()` with data type `np.uint8`.
- Inspects core array properties:
  - **Shape:** `(200, 200, 3)`
  - **Data Type:** `uint8` (values from 0 to 255)
  - **Memory footprint:** Calculates memory usage using `img.nbytes` (120,000 bytes).
- Renders the baseline blank image via `matplotlib.pyplot.imshow()`.

### 2. Drawing Colored Shapes Using Array Slicing
- Uses direct indexing and array slicing (`img[y1:y2, x1:x2]`) to modify pixel values in-place without loops.
- Fills a $60 \times 60$ sub-region using `np.full()`.
- Generates a synthetic multi-colored grid with four quadrants:
  - **Top-Left:** Red `[255, 0, 0]`
  - **Top-Right:** Green `[0, 255, 0]`
  - **Bottom-Left:** Blue `[0, 0, 255]`
  - **Bottom-Right:** Yellow `[255, 255, 0]`
- Adds horizontal (`img[90:100, :]`) and vertical (`img[:, 90:100]`) white dividing borders.

### 3. Cropping, Flipping, and RGB Channel Extraction
- **Cropping:** Extracts a central $100 \times 100$ region (`img[50:150, 50:150, :]`).
- **Horizontal Flipping:** Inverts columns using step slicing (`img[:, ::-1, :]`).
- **Vertical Flipping:** Inverts rows using step slicing (`img[::-1, :, :]`).
- **Color Channel Decomposition:** Separates Red, Green, and Blue channels (`img[:, :, 0]`, `img[:, :, 1]`, and `img[:, :, 2]`) and visualizes individual channel intensities with grayscale color maps (`cmap="gray"`).

### 4. Brightness Adjustment & Boolean Masking
- **Type Conversion:** Promotes array to `np.float32` for safe arithmetic operations to avoid unsigned integer overflow/underflow.
- **Brightness Adjustment:**
  - Brightening by adding a scalar offset (`+ 50`).
  - Darkening by subtracting a scalar offset (`- 50`).
  - Uses `np.clip(..., 0, 255)` to clamp pixel values within the valid $[0, 255]$ range before converting back to `np.uint8`.
- **Boolean Masking:** Applies conditional thresholding across all 3 color channels using `np.all(img >= 200, axis=2)` to isolate bright regions (such as the white grid lines).

### 5. Memory Footprint Analysis (`uint8` vs `float64`)
- Explores memory consumption differences across numeric representations:
  - **`np.uint8`:** 1 byte per channel value $\rightarrow$ **120,000 bytes** (~117.2 KB).
  - **`np.float64`:** 8 bytes per channel value $\rightarrow$ **960,000 bytes** (~937.5 KB).
- Demonstrates an **$8\times$ memory reduction** when using appropriate data types and highlights normalization requirements when rendering floating-point imagery in Matplotlib.

---

## 🛠️ Requirements & Installation

### Prerequisites
- Python 3.8+
- Jupyter Notebook / JupyterLab or Google Colab

### Installation
Clone the repository and install the dependencies:

```bash
git clone https://github.com/manasir747/Image-Pixel-Manipulator.git
cd Image-Pixel-Manipulator
pip install numpy matplotlib notebook
```

---

## 💻 How to Run

### Option 1: Run Locally via Jupyter Notebook
Launch Jupyter:
```bash
jupyter notebook Image_Pixel_Manipulator.ipynb
```
Run the notebook cells sequentially to view each visualization and printed memory metrics.

### Option 2: Run in Google Colab
Click the badge below to run the notebook directly in your browser without any local setup:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manasir747/Image-Pixel-Manipulator/blob/main/Image_Pixel_Manipulator.ipynb)

---

## 📂 Project Structure

```text
Image-Pixel-Manipulator/
│
├── Image_Pixel_Manipulator.ipynb   # Main Jupyter notebook with all steps & visual outputs
└── README.md                       # Project documentation
```

---

## 📖 Key Takeaways

1. **Vectorized Operations:** Array slicing enables high-performance pixel manipulations without explicit Python `for` loops.
2. **Safe Pixel Arithmetic:** Arithmetic on pixel arrays should be conducted using floating-point representations combined with `np.clip()` to prevent byte overflow artifacts.
3. **Memory Optimization:** Choosing `uint8` over higher-precision floats significantly reduces memory requirements for image processing pipelines.