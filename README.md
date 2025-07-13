# 🔥 AE-NODE for Hydrogen Autoignition Modeling

This repository implements an **Autoencoder-Neural ODE (AE-NODE)** framework to efficiently model the **stiff chemical dynamics** of constant-pressure hydrogen-air autoignition systems. Leveraging Cantera for data generation and PyTorch for training, the model captures complex temporal evolution with reduced computational overhead.

---

## 🚀 Project Overview

Stiff ODE systems from combustion chemistry are notoriously difficult and expensive to simulate. This project applies **non-linear autoencoders** to embed high-dimensional simulation data into a low-dimensional latent space and uses **Neural ODEs** to evolve the dynamics continuously in time.

### Highlights:
- Simulated 36 ignition scenarios using Cantera.
- Used **multi-scale KDE sampling** for temporal resolution.
- Trained a **latent-space Neural ODE model** using `torchdiffeq`.
- Validated on 24 unseen cases with strong generalization.
- Achieved accuracy comparable to direct ODE solvers with a fraction of the cost.

---

## 📁 Project Structure

```bash
.
├── data_sampling_sb.ipynb         # KDE + random sampling of Cantera output
├── h2_node_training_sp.ipynb      # AE-NODE training and validation
├── solution_data/                 # Raw ignition simulation data (CSV)
├── sampled_multiscale_50/         # KDE-sampled reduced dataset
├── models/                        # Trained model weights (.pt)
├── plots/                         # Result visualizations and training loss
└── README.md                      # This file
## 🛠️ Technologies Used

- **Python**, **NumPy**, **Matplotlib**
- **PyTorch** – for model definition and training
- **Torchdiffeq** – for continuous-time Neural ODE integration
- **Cantera** – for hydrogen-air autoignition simulation and data generation
- **Kernel Density Estimation (KDE)** – for multi-scale temporal sampling

---

## 📊 Dataset

- **36 hydrogen ignition cases** simulated using Cantera
- **Simulation time**: 10 ms with **1e-6 s timestep** (10,000 points per case)
- **State variables**: 10 total (9 species mass fractions + 1 temperature)
- Dataset **reduced using KDE-based sampling** to 50 key points per case

---

## 🧠 Model Architecture

- **Encoder**: `10 → 128 → 64 → 5` with **ELU activations**
- **Latent ODE Function**: `5 → 64 → 64 → 5` (latent dynamics)
- **Decoder**: `5 → 64 → 128 → 10` for full-state reconstruction
- **ODE Solver**: `dopri5` with `atol=1e-8`, `rtol=1e-7`
- **Loss Function**: Mean Absolute Error (L1 Loss)
- **Training**: 
  - Epochs: `1000`
  - Learning Rate: `1e-4` with scheduler
  - Batch Size: `1`
  - Gradient Clipping applied

---

## 📈 Results

- The **AE-NODE model accurately reproduces ignition delays and species evolution**
- **KDE-based multi-scale sampling** improves model convergence and learning efficiency
- **Stiffness of the original system is mitigated**, enabling faster and stable inference using explicit solvers

---

## ✅ How to Run

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/h2-autoignition-node.git
   cd h2-autoignition-node
