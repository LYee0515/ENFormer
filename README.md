# ENFormer: Enhanced Spatiotemporal Transformer for Robust 3D Human Pose Estimation

This repository provides the official implementation of **ENFormer**, a robust and efficient framework for 3D human pose estimation.  
ENFormer integrates **frequency-domain filtering**, **local joint interaction modeling**, and **temporal kinematic constraints** to enhance accuracy and robustness, especially under occlusions and noisy 2D detections.

This code is directly related to the manuscript submitted to **The Visual Computer (2025)**.
---

## 🔗 Project Links

- **GitHub:** https://github.com/LYee0515/ENFormer

---

## 🔧 Environment Setup

```bash
conda create -n enformer python=3.9
conda activate enformer
pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117
pip install -r requirements.txt
```

## 📘 Introduction

Transformer-based 3D human pose estimation has demonstrated strong performance, but existing models suffer from:

- **Sensitivity to 2D noise**  
- **Weak local joint modeling**  
- **Limited temporal consistency**  

To solve these issues, **ENFormer** introduces:

### 🔹 Frequency Filtering Module (FFM)
Filters high-frequency noise and enhances domain-relevant joint trajectory signals.

### 🔹 Local Interaction Enhancement (LIE)
Captures fine-grained spatial relations between local joint groups.

### 🔹 Temporal Interaction Module (TIM)
Imposes temporal kinematic consistency for smooth and stable pose predictions.

Experiments on **Human3.6M** and **MPI-INF-3DHP** demonstrate that ENFormer achieves competitive state-of-the-art accuracy with strong robustness.

---

## 🧩 Repository Structure
ENFormer/
├── README.md
├── requirements.txt
├── run_enformer.py                   # Main training/testing script (placeholder)
├── run_3dhp.py              
├── model/
│   ├── ENFormer.py         # Main architecture (to be released)
│   └── graph.py
├── dataset/
│   ├── data_2d_h36m_cpn_ft_h36m_dbb.npz
│   ├── data_2d_h36m_gt.npz
│   ├── data_3d_h36m.npz
│   ├── data_test_3dhp.npz
│   ├── data_train_3dhp.npz
│   └── README.md
├── common/
├── images/
├── checkpoint/
└── demo/
Note: Some core files (e.g., ENFormer.py) will be released after paper acceptance.

🧪 Training and Evaluation
### Human 3.6M
For the training stage, please run:
```bash
python run_enformer.py -g 0 -k cpn_ft_h36m_dbb -frame 27 -frame-kept 3 -coeff-kept 3 -c checkpoint/NAMED_PATH
```

For the testing stage, please run:
```bash
python run_enformer.py -g 0 -k cpn_ft_h36m_dbb -frame 27 -frame-kept 3 -coeff-kept 3 -c checkpoint/ --evaluate NAME_ckpt.bin
```
Different models use different configurations as follows.
F: number of input frames; N: number of sampled frames; D: number of retained Discrete Cosine Transform coefficients

| F   | N  | D  | Alias |  
|-----|----|----|-------|
| 9   | 1  | 1  | H1    |
| 9   | 1  | 3  | H2    |
| 27  | 1  | 3  | H3    |
| 27  | 3  | 3  | H4    |
| 243 | 27 | 27 | H5    |
The results are as follows.

| Alias | P1 (mm) | P2 (mm) | 
|-------|---------|---------|
| H1    | 50.0    | 39.2    |
| H2    | 49.2    | 38.0    |
| H3    | 47.2    | 36.5    |
| H4    | 47.4    | 36.6    |
| H5    | 44.5    | 34.9    |
### MPI-INF-3DHP
We followed P-STMO to prepare the data and train our model.


🎥 Visualization
Qualitative visualizations are conducted using publicly available online videos for demonstration purposes.
All identifiable information has been removed.

The full source code, pre-trained weights, and experiment logs
will be made public upon paper acceptance to ensure transparency and reproducibility.




