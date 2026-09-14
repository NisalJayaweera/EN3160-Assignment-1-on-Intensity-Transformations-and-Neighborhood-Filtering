# EN3160 — Assignment 1: Intensity Transformations and Neighborhood Filtering

Coursework repository for Assignment 1 of **EN3160 (Image Processing and Machine Vision)**,
Department of Electronic and Telecommunication Engineering, University of Moratuwa.

**Index Number:** 230300C
**Report:** [`230300c_a01.pdf`](./230300c_a01.pdf)

## Overview

This assignment implements and evaluates ten classical intensity-transformation and
neighborhood-filtering techniques in Python/OpenCV, each verified against the equivalent
OpenCV routine where one exists.

| # | Task | Key idea |
|---|------|----------|
| 1 | Piecewise-linear intensity transform | Breakpoint-defined LUT via `cv2.LUT` |
| 2 | White/gray matter accentuation | Grey-level slicing on a brain PD MRI slice |
| 3 | Gamma correction | Applied to the L plane in L\*a\*b\* space |
| 4 | Vibrance enhancement | Gaussian-modulated boost on the saturation plane |
| 5 | Histogram equalization | From-scratch implementation, verified pixel-identical to `cv2.equalizeHist` |
| 6 | Foreground-only histogram equalization | Saturation-plane masking + equalization restricted to the subject |
| 7 | Sobel filtering | Three equivalent routes: `filter2D`, manual correlation, separable `[1,2,1]ᵀ*[1,0,-1]` |
| 8 | Image zooming | Nearest-neighbor and bilinear interpolation, scored by normalized SSD |
| 9 | GrabCut segmentation + background blur | Includes the masking-order artifact behind the dark edge halo |
| 10 | Bilateral filtering | From-scratch implementation benchmarked against `cv2.bilateralFilter` (PSNR) |

## Repository structure

```
.
├── en3160_a01.ipynb             
├── 230300c_a01.pdf          
├── images                 
└── README.md
```

## Running it

```bash
pip install opencv-python numpy matplotlib scikit-image jupyter nbconvert

# regenerate and execute the notebook
python build_notebook.py
jupyter nbconvert --to notebook --execute --inplace en3160_a01.ipynb

# export the report
jupyter nbconvert --to pdf en3160_a01.ipynb --output 230300c_a01
```

## Notes

- Q8's zoom validation uses a self-contained down/up-sample round trip on one of the supplied
  images, since the course-provided small/large image test set wasn't distributed with the
  assignment brief. Swap in the actual dataset files under `images/` before relying on the
  reported SSD numbers.
- All from-scratch implementations (histogram equalization, Sobel filtering, bilateral filter)
  are cross-checked against the corresponding OpenCV routine directly in the notebook.
