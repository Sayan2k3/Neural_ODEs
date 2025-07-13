# 🔥 AE-NODE for Hydrogen Autoignition Modeling

This repository implements an **Autoencoder-Neural ODE (AE-NODE)** framework to efficiently model the stiff chemical dynamics of constant-pressure hydrogen-air autoignition systems. Leveraging **Cantera** for data generation and **PyTorch** for training, the model captures complex temporal evolution with significantly reduced computational overhead.

---
## 📁 Project Structure

.
├── data_sampling_sb.ipynb         # KDE + random sampling of Cantera output
├── h2_node_training_sp.ipynb      # AE-NODE training and validation
├── solution_data/                 # Raw ignition simulation data (CSV)
├── sampled_multiscale_50/         # KDE-sampled reduced dataset
├── models/                        # Trained model weights (.pt)
├── plots/                         # Result visualizations and training loss
└── README.md                      # This file

## 🚀 Project Overview

Stiff ODE systems from combustion chemistry are notoriously difficult and expensive to simulate. This project applies **non-linear autoencoders** to embed high-dimensional simulation data into a low-dimensional latent space and uses **Neural ODEs** to evolve the dynamics continuously in time.

### 🔍 Highlights

- ✅ Simulated **36 hydrogen ignition scenarios** using Cantera
- ✅ Employed **KDE-based multi-scale sampling** for temporal resolution
- ✅ Trained a **latent-space Neural ODE** model using `torchdiffeq`
- ✅ Validated on **24 unseen cases** with strong generalization
- ✅ Achieved accuracy comparable to direct solvers with much lower cost

---


---

## 🛠️ Technologies Used

- **Python**, **NumPy**, **Matplotlib**
- **PyTorch** – model definition and training
- **Torchdiffeq** – continuous-time Neural ODE solver
- **Cantera** – hydrogen-air autoignition simulations
- **Kernel Density Estimation (KDE)** – for multi-scale temporal sampling

---

## 📊 Dataset

- 🔬 **36 hydrogen ignition cases** generated via Cantera
- ⏱️ **10 ms simulation time**, with **1e-6 s timestep** → 10,000 time points per case
- 📦 **10 state variables**: 9 species mass fractions + 1 temperature
- 🎯 **KDE-based sampling** reduced data to **50 key points per case**

---

## 🧠 Model Architecture

- **Encoder**: `10 → 128 → 64 → 5` (ELU activations)
- **Latent ODE Function**: `5 → 64 → 64 → 5` (latent dynamics)
- **Decoder**: `5 → 64 → 128 → 10` (reconstruction)
- **ODE Solver**: `dopri5`, `atol=1e-8`, `rtol=1e-7`
- **Loss Function**: L1 (Mean Absolute Error)
- **Training Setup**:
  - Epochs: `1000`
  - Learning Rate: `1e-4` with scheduler
  - Batch Size: `1`, Batch Time: `9998`
  - Gradient Clipping: Max Norm = `1.0`

---

## 📈 Results

- ✅ AE-NODE accurately captures ignition delay and post-ignition behavior
- 📉 KDE sampling enhances learning convergence and model robustness
- ⚡ Reduced system stiffness enables stable training with explicit solvers
- 🔬 Latent representation preserves temporal evolution with fewer dimensions

---

## ✅ How to Run

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/h2-autoignition-node.git
   cd h2-autoignition-node


