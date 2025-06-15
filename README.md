# Nilrean_ROI_based_MVPA
This repository contains code to perform ROI-based multivariate pattern analysis (MVPA) on fMRI beta images using nilearn, focusing on emotional valence decoding (positive vs negative) within depressed individuals exposed to musical and nonmusical auditory stimuli. 

## ROI-Based Valence Decoding in Depression (Music vs Non-Music fMRI)

This repository contains Python code for performing region-of-interest (ROI) based multivariate pattern analysis (MVPA) on fMRI beta images using the nilearn library. The analysis focuses on decoding emotional valence (positive vs. negative) from beta patterns in predefined ROIs, using data from individuals diagnosed with Major Depressive Disorder (MDD).

The script implements decoding with a linear support vector machine (SVM) and compares the results to a baseline classifier using scikit-learn’s DummyClassifier. Evaluation is performed using the Area Under the Receiver Operating Characteristic Curve (AUC), with significance tested via paired t-tests.

## Dataset

This analysis uses beta images derived from the openly available dataset:

Lepping, R. J., et al. (2016). Neural Processing of Emotional Musical and Nonmusical Stimuli in Depression.
PLoS ONE, 11(6), e0156859. https://doi.org/10.1371/journal.pone.0156859

The dataset is hosted on OpenNeuro and can be accessed here:
https://openneuro.org/datasets/ds000171

## Reference Implementation

This analysis builds upon and extends the decoding structure provided by the official Nilearn tutorial:

Nilearn Haxby Decoding Example:
https://nilearn.github.io/stable/auto_examples/02_decoding/plot_haxby_full_analysis.html

The current script adapts the following components:

ROI-based signal extraction using NiftiMasker
Classification using LinearSVC
AUC scoring (roc_auc) instead of accuracy
Subject-level cross-validation (LeaveOneGroupOut)
Comparison to DummyClassifier as a chance-level benchmark
Design Summary

## Experimental Design:
A 2 (Valence: Positive vs. Negative) × 2 (Stimulus Type: Music vs. Non-Music) within-subject design.

## ## Group Selection:### 
Only participants in the depression group were selected for this analysis.

## Data Structure:

3 runs contain music stimuli
2 runs contain non-music stimuli
Each run includes blocks of emotionally evocative stimuli (positive or negative)
Important Methodological Note:
Because the number of runs per condition is unequal (3 music vs. 2 non-music), we avoid using run-based chunks for cross-validation. Instead, subject_ids are used as the grouping variable, enabling leave-one-subject-out (LOSO) cross-validation. This ensures generalization to new subjects and avoids information leakage due to modality imbalance.
 
## Analysis Goals

## This analysis aims to:

Determine whether specific ROIs (e.g., ACC, Right Amygdala, Occipital Cortex) contain valence-discriminative information in individuals with depression.
Statistically evaluate whether decoding performance is significantly better than chance using paired t-tests between the SVM and Dummy classifier AUCs.
Visualize classification performance and statistical outcomes across ROIs.
Output Files

## depression_roi_results.csv: Summary of decoding performance per ROI, including:
SVM AUC and standard deviation
Dummy AUC and standard deviation
Performance difference
t-statistic and p-value

## depression_roi_analysis.png: Visualization containing:
Bar plot comparing SVM and Dummy AUCs
AUC difference across ROIs
-log10(p-value) plot for statistical significance
Table summarizing results per ROI
Interpretation Guidelines

AUC ≈ 0.5: Indicates chance-level decoding (no information)
AUC > 0.6: Suggests reliable valence decoding

Statistical threshold: p < 0.05 (two-tailed paired t-test)
## Requirements

Python 3.7+
nilearn
scikit-learn
numpy, pandas
matplotlib, seaborn
Nifti beta images and ROI masks in .nii format
