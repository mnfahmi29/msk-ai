# 🦴 MSK-AI
**Interpretable Morphology-Driven AI for Musculoskeletal Tumor Histopathology**
> A dictionary-based, feature-driven AI pipeline for musculoskeletal (MSK) tumor classification from H&E whole-slide images (WSIs), emphasizing interpretability, modularity, and clinical reasoning.

---

## 📌 Project Overview
This repository documents an **end-to-end AI pipeline** for analyzing **soft tissue tumor histopathology** using **explicit morphological features** rather than end-to-end black-box deep learning.
The central philosophy is:

> **Extract what pathologists see → encode it → reason over it.**

Instead of predicting directly from pixels, this pipeline:
1. Segments nuclei,
2. Extracts interpretable nucleus & cell features,
3. Builds a **morphological dictionary**,
4. Encodes slides as distributions of visual words,
5. Trains transparent classifiers,
6. Reports **what morphological patterns drive decisions**.

---

## 🎯 Scientific Motivation
Musculoskeletal tumor diagnosis often relies on:
* Nuclear pleomorphism
* Cell density & arrangement
* Nucleus–cytoplasm ratio
* Chromatin intensity & heterogeneity

Many centers lack access to advanced molecular testing, making **H&E morphology the most accessible signal**.
This project aims to:
* Preserve **clinical interpretability**
* Enable **auditable AI**
* Support **low-resource pathology settings**
* Bridge classical pathology with modern ML

---

## 🧠 Pipeline Summary  

![MSK-AI Research Workflow](figure/research_workflow.png)


### **Step 1 — Data Acquisition & Preprocessing**
* ~100 H&E WSIs of soft tissue tumors
* Quality control (resolution, staining, artifacts)
* Metadata linkage
* Dataset split (train/val/test or CV)
**Output:** curated WSIs + structured metadata

---

### **Step 2 — Nuclei Segmentation**
* Color deconvolution (hematoxylin channel)
* Multi-level Otsu thresholding
* Morphological cleanup
* Watershed separation of clustered nuclei
**Output:** validated nucleus masks

---

### **Step 3 — Feature Extraction**
Extract **explicit, pathologist-aligned features**:
  
#### Nucleus features
* Area, perimeter, circularity
* Eccentricity, calipers, aspect ratio
* Hematoxylin optical density (mean, max, std, range)
* Nuclear density per patch

#### Cell & context features
* Nucleus-to-cell ratio
* Estimated cell size & shape
* Cytoplasmic (eosin) intensity
* Cell density & spatial clustering

**Output:** nucleus + cell feature matrix

---

### **Step 4 — Dictionary Construction**

Cluster feature vectors into **morphological “visual words”**.
* **K-means** → hard nucleus categories
* **GMM** → soft cell phenotypes
* Typical dictionary size: **64–256 words**

#### Example nucleus descriptors
* Small / medium / large
* Round / elongated / spindle / pleomorphic
* Pale / hyperchromatic / heterogeneous chromatin

#### Example cell descriptors
* Low vs high nucleus–cell ratio
* Sparse vs crowded arrangement
* Light vs eosinophilic cytoplasm

**Output:** interpretable morphological dictionary

---

### **Step 5 — Patch & Slide Encoding**
* Encode patches as histograms of dictionary words
* Aggregate to slide-level representation
* Normalized distributions (L1)

**Output:** slide-level encoded feature vectors

---

### **Step 6 — Classification Modelling**
* Logistic Regression
* SVM
* Random Forest
* Gradient Boosting

Includes:
* Calibration (Platt / Isotonic)
* AUROC, PR, confusion matrix
* External validation (10–15 WSIs)

**Output:** benign vs malignant classifier + metrics

---

### **Step 7 — Interpretability & Uncertainty**
* Feature importance (coefficients / SHAP)
* Top dictionary words driving predictions
* Explicit uncertainty zone (e.g. 0.45–0.55)

**Output:** dictionary-level explanation report with visual prototypes

---

## 🧩 Design Principles
This repository follows these principles:
* **Interpretability first**
* **Modular pipeline** (each step can be audited)
* **Clinically grounded features**
* **Model transparency over raw accuracy**
* **Reproducible scientific reporting**

---

## 🗂 Repository Status
* ✅ Conceptual pipeline defined
* ✅ Parameters & outputs specified
* ✅ Literature-anchored methodology
* ⏳ Code implementation (future work)
* ⏳ Public dataset instantiation (future work)

This README serves as a **scientific and architectural reference** for:
* Grant proposals
* Collaboration discussions
* Future implementation repositories

---

## 📚 Key References
* Allan C et al. *OMERO: flexible, model-driven data management*. Nat Methods, 2012
* Heckenbach I et al. *Nuclear morphology as a biomarker*. Nat Aging, 2022
* Abdolhoseini M et al. *Segmentation of clustered nuclei*. Sci Rep, 2019
* Zhao R et al. *Dictionary learning in medical imaging*. Arch Comput Methods Eng, 2021

---

## 👤 Author

**Muhammad Nur Fahmi, MD**

Physician–Researcher

---
