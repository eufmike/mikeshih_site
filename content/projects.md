---
title: "Projects"
date: 2020-04-19T05:13:10-05:00
draft: false
toc: true
---

## DL Segmentation on FIB-SEM Datasets
GitHub: [DL Segmentation on FIB-SEM Datasets](https://github.com/eufmike/fibsem_seg_dl)\
Features: Python, Keras, TensorFlow


---

## STORM Imaging Analysis
GitHub: [STORM Imaging Analysis](https://github.com/eufmike/storm_image_processing)\
Features: Python, R, MATLAB, Numpy, Scipy, ImageJ/Fiji

This project was a collaboration aiming to analyze the nanoclusters of membrane proteins and the interaction between membrane proteins and lipid rafts. The function combined multiple platforms and packages including Python, R (spatstat), MATLAB, and ImageJ/Fiji(Thunderstorm) to employ Ripley's K function, Local-K, density map, and Coordinate-based colocalization. 
{{< figure src="/posts/projects/storm_image_analysis.png">}}
Detail of point pattern analysis (Ripley's K family) was described in the following posts.
* [Point Pattern Analysis](/content/posts/point_pattern_analysis.md)
* [Ripley's K Demo: 01 Point Process Simulation](/content/posts/Ktest_demo_01_simulator.md)
* [Ripley's K Demo: 02 K test](/content/posts/Ktest_demo_02_Ktest.md)

---

## Lung Vasculature Analysis

GitHub: [Lung Vasculature Analysis](https://github.com/eufmike/woo_lung_analysis)\
Features: Python, Pandas, Numpy, Matplotlib

This project was to analyze mice lung vasculature labeled with gold nanoparticles. 3D tomography was acquired from Zeiss Xradia. I used Amira to segment targeted regions by combining a series of background subtraction, edge detection, and manual labeling. Filament analysis was then applied by using built-in auto-skeletonization to extract the backbone of lung vasculature and its diameter. 
{{< figure src="/posts/projects/lung_vasculature.png" width="250">}}

---

## Embryonic Brain Reconstruction

GitHub: [Embryonic Brain Reconstruction](https://github.com/eufmike-archive-wucci/matlab_batch_testing)\
Features: MATLAB, Image Processing Toolbox

This project was to contour the brain region on embryonic slide scans acquired from Zeiss Axio Scan.Z1. The sample was stained with four different nucleus and epithelial markers, which can be used for segmentation. The images were then exported to MBF Brain Maker for image registration. I used Imaris for 3D reconstruction.  

{{< figure src="/posts/projects/embryonic_brain.jpg">}}