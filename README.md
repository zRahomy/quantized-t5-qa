#  Quantized T5 Question Answering System

### Abdulalrahman Husham A. Razzaq Alabbas  
**Student ID:** 1905983  
**Course:** ARI5501 – Natural Language Processing  

---

##  Project Overview

This project studies the effect of **post-training quantization** on a neural **question answering system** based on **T5-small**.

Three inference configurations are compared:

- **FP16 baseline**
- **INT8 quantized**
- **INT4 quantized**

The evaluation focuses on five key metrics:

- **Exact Match (EM)**
- **F1 Score**
- **Inference Time**
- **Peak GPU VRAM Usage**
- **Model Disk Storage Size**

**Goal:** Understand the practical trade-offs between **accuracy**, **speed**, and **memory efficiency**.

---

##  System Pipeline

### 1. Data Loading
The **SQuAD v1.1** dataset is automatically downloaded using **HuggingFace Datasets**.

### 2. Preprocessing
The dataset is shuffled and subsampled into:

- **10,000 training samples**
- **2,000 validation samples**

The samples are converted into **T5 prompt format** and tokenized.

### 3. Model Training
**T5-small** is fine-tuned using **HuggingFace Trainer** with **FP16** enabled.

### 4. Quantization & Export
The trained model is saved as an **FP16 baseline**, then quantized into **INT8** and **INT4** versions using **BitsAndBytes**.

### 5. Evaluation & Benchmarking
All models are evaluated on the validation set while measuring accuracy, runtime, GPU memory usage, and disk size.

---

##  Experimental Results

| Model | EM (%) | F1 (%) | Time (s) | VRAM (MB) | Disk Size (MB) |
|------|------|------|------|------|------|
| **FP16** | 63.85 | 78.11 | **217.19** | 774.87 | 233.92 |
| **INT8** | 63.65 | 78.02 | 651.54 | 682.21 | 112.77 |
| **INT4** | 63.50 | 77.85 | 371.02 | **636.25** | **98.14** |

---

##  Key Findings

- Quantization preserves accuracy with minimal EM/F1 degradation.
- Disk storage is reduced by over **57%** with **INT4**.
- Runtime GPU memory decreases but remains dominated by activation and generation buffers.
- **FP16** is the fastest due to GPU tensor-core optimization.
- **INT4** provides the best memory compression but slower inference.

---

##  Repository Structure

```text
notebooks/   → all experiment pipelines
data/        → auto-generated at runtime
model/       → auto-generated at runtime
```

> **Note:**  
> The `data/` and `model/` folders are intentionally empty in this repository.  
> All datasets and trained models are automatically created when the notebooks are executed.

---

##  How to Run

### 1. Clone the repository
```bash
git clone https://github.com/zRahomy/quantized-t5-qa.git
cd quantized-t5-qa
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebooks in order
```text
01_data_loading.ipynb  
02_preprocessing.ipynb  
03_training.ipynb  
04_Evaluation.ipynb  
05_QuantizationAndResults.ipynb
```

All datasets and models will be downloaded and generated automatically.

---

##  Dataset Reference

**SQuAD v1.1**  
https://rajpurkar.github.io/SQuAD-explorer/

---

##  Course Context

This project was developed as the **final course project** for  
**ARI5501 – Natural Language Processing**.
