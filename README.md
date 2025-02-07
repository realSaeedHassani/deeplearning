# Deep Learning for Bearing Fault Detection
> **Project**: Bearing Fault Detection and Classification Using Temporal Convolutions and LSTM Networks in Induction Machine Systems.

This project applies deep learning to detect and classify faults in bearings of induction machines. The model leverages Temporal Convolutional and LSTM layers to effectively identify various fault types.

---

## 📄 Publication Reference

For a comprehensive exploration of our methodology and findings, consult our published paper:

**Title**: *Classification of Fault Severity in Induction Machine Systems Using Temporal Convolutions and Recurrent Networks*  
**Authors**: V. Mashayekhi, S. Hasani Borzadaran, M. Hoseintabar Marzebali  
**Published**: February 16, 2022  
**Access**: [DOI](https://doi.org/10.1155/2022/4224356)

This paper outlines the advanced deep learning techniques developed to detect and classify fault severity in induction machine systems.

---

## Requirements
To reproduce the results, install the dependencies in a Python 3.7 environment.

- **Python**: 3.7
- **Required Packages**: Listed in `requirements.txt`

## Dataset Summary
The dataset consists of bearing fault signals, pre-processed for experiments with optional downsampling. The table below summarizes the data structure:

| Downsampling | Sequence Length | Training Samples | Test Samples | Classes |
| :---: | :---: | :---: | :---: | :---: |
| Yes | 899 | 3095 | 890 | 16 |
| No | 1000 | - | - | 16 |

---

## Model Evaluation
The following table shows the performance of GRU-based models across various configurations, using different downsampling and architecture options to optimize classification accuracy.

| Run | Epochs | Batch Size | Architecture | Weights | Downsampling | Accuracy |
| --- | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | 600 | 128 | [#1](#1-architecture) | 1 | Yes | 71.46% |
| 2 | 1200 | 128 | [#1](#1-architecture) | 2 | Yes | 84.26% |
| 3 | 1200 | 128 | [#2](#2-architecture) | 3 | Yes | 84.94% |
| **4** | 1200 | 128 | [#3](#3-architecture) | 4 | Yes | **87.52%** |
| 5 | 900 | 64 | [#1](#1-architecture) | 5 | Yes | 83.37% |
| _ | _ | _ | _ | _ | _ | _ |
| 6 | 200 | 128 | [#4](#4-architecture) | - | No | 71.35% |
| 7 | 500 | 128 | [#4](#4-architecture) | - | No | 94.65% |
| 8 | 650 | 128 | [#4](#4-architecture) | - | No | 95.37% |
| 9 | 700 | 128 | [#4](#4-architecture) | - | No | 95.48% |
| 10 | 900 | 128 | [#4](#4-architecture) | - | No | 95.62% |
| **11** | 1050 | 128 | [#4](#4-architecture) | - | No | **95.77%** |
| _ | _ | _ | _ | _ | _ | _ |
| 12 | 600 | - | [#5](#5-architecture) | - | No | 91.91% |
| **13** | 850 | - | [#5](#5-architecture) | - | No | **93.70%** |
| 14 | 1000 | - | [#5](#5-architecture) | - | No | 92.43% |
| 15 | 1050 | - | [#5](#5-architecture) | - | No | 92.43% |

---
## Model Architectures

This section details the model architectures used for bearing fault detection, optimized with different downsampling strategies to enhance efficiency and accuracy. Each architecture utilizes 1D convolutional layers with varying configurations.

---

### Architectures with Downsampling (Yes)

These architectures employ downsampling to reduce sequence length, facilitating faster training while retaining essential temporal features.

- **#1 Architecture**: A four-layer convolutional model that maintains consistent dimensionality across the first three layers, with a reduction in the final layer.
    ```python
    Conv1D(128) => Conv1D(128) => Conv1D(128) => Conv1D(64)
    ```

- **#2 Architecture**: An enhanced version of #1 with increased dimensionality in the middle layers for improved feature extraction.
    ```python
    Conv1D(128) => Conv1D(256) => Conv1D(256) => Conv1D(64)
    ```

- **#3 Architecture**: This configuration introduces a more gradual increase in filter sizes, potentially capturing finer-grained features before reduction.
    ```python
    Conv1D(64) => Conv1D(128) => Conv1D(256) => Conv1D(64)
    ```

---

### Architectures without Downsampling (No)

These architectures retain the full sequence length, designed for more detailed temporal feature extraction without losing data granularity.

- **#4 Architecture**: A stable model with identical filter sizes in the first three layers, enabling consistent feature maps, followed by a final reduction layer.
    ```python
    Conv1D(128) => Conv1D(128) => Conv1D(128) => Conv1D(64)
    ```


<div align="center">
    <img src="images/run-01.png" alt="Run 01 Results">
    <span>Figure 1: Results for Architecture #4</span>
</div>
    
---

- **#5 Architecture**: A deeper configuration with an initial smaller filter size, followed by an increase, allowing the model to learn a hierarchical representation of features.
    ```python
    Conv1D(64) => Conv1D(64) => Conv1D(64) => Conv1D(128) => Conv1D(64)
    ```

  
<div align="left">
    <img src="images/run-02.png" alt="Run 02 Results">
    <span>Figure 2: Results for Architecture #5</span>
</div>


---

Each architecture has been tested with specific training conditions to measure its accuracy and performance, providing insights into the effectiveness of downsampling for fault detection in induction machine systems.

