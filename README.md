# ACF: Axial Contrastive Field for TAD boundary prediction on Hi-C Data

## Overview
This repository contains the implementation of **ACF (Axial Contrastive Field)**, 
a deep learning–based feature extraction approach designed for identifying structural patterns in Hi-C contact matrices.

Hi-C data is represented as a 2D matrix, where topologically associating domains (TADs) appear as square-shaped regions.  
ACF is implemented using Tensorflow and focuses on learning **axis-wise intensity changes** rather than internal interactions, which allows more efficient and purpose-aligned pattern learning.

## Data Assumptions
- Input Hi-C contact matrices are expected to be:
  - **Binned at 25 kb resolution**
  - **Distance-normalized and scaled**
  - Provided in **plain text (.txt) matrix format**
- Each input file should represent a square Hi-C contact matrix
  with bin indices already aligned to the chosen resolution.

## Environment
This code was tested with the following environment:
- Python 3.11.0
- NumPy 2.1.3
- pandas 2.3.1
- TensorFlow 2.19.0
- SciPy (for numerical utilities)

## Background & Motivation
Conventional TAD callers rely on handcrafted statistics or heuristic boundary detection, often producing inconsistent results across methods.

While recent deep learning–based approaches exist, some architectures (e.g., Transformer-based) introduce unnecessary complexity by modeling global interactions that do not directly align with the definition of TAD boundaries.

This project explores an alternative design:
- Emphasizing **local axis-wise changes**
- Reducing model complexity
- Improving interpretability and efficiency

## Core Idea
The core idea of ACF is:
- Treating Hi-C contact matrices as image-like 2D data
- Learning **directional changes (up/down/left/right)** across matrix axes
- Reinforcing boundary and edge patterns instead of internal region similarity
![Figure 2-1](https://github.com/user-attachments/assets/4d5df5c1-7567-4cca-8618-c12a023a49d1)


This design enables:
- Better alignment between model structure and research objective
- Lower memory usage compared to attention-based models
- More stable boundary-focused predictions

## Repository Structure
ACF.ipynb
- Core implementation of the ACF model
- TensorFlow-based implementation of the ACF model
- Model architecture and training pipeline

ACF_sample_generation.ipynb
- Sample generation and preprocessing for Hi-C matrices
- Patch extraction and data preparation utilities

## How to Use
1. Prepare Hi-C contact matrix data in matrix format.
2. Use `ACF_sample_generation.ipynb` to generate input samples.
3. Run `ACF.ipynb` to train and evaluate the ACF model.
4. Modify paths and parameters as indicated in the notebooks.

## Implementation Notes & Acknowledgements
- The data preprocessing pipeline and false positive filtering logic were adapted and modified based on the implementation of **deepTAD**.
- These components were selectively restructured to better align with the ACF design and the axis-change–focused learning objective.
- Hierarchical TAD merging and downstream hierarchy construction were intentionally excluded from this repository.
  For full hierarchical reconstruction, refer to the original **deepTAD** implementation.
- This repository focuses on feature extraction and boundary-aware pattern learning, rather than providing a complete end-to-end TAD calling framework.
- Ground truth preparation is not included in this repository and may vary depending on the experimental setup.
![Figure 2-2](https://github.com/user-attachments/assets/e75b45fe-26e6-4028-9f7f-2d95a49700f5)


## Notes
- This code is intended for **research and experimental use**.
- The implementation focuses on structural pattern learning rather than end-to-end TAD calling pipelines.
- Some hyperparameters and preprocessing steps may require tuning depending on data resolution.
- This implementation does **not** perform:
  - End-to-end TAD calling
  - Domain hierarchy construction
  - Post-hoc biological interpretation


## Disclaimer
This repository is provided for academic and research purposes.
Not intended for clinical or production use.
