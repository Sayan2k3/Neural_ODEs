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
🛠️ Technologies Used
Python, NumPy, Matplotlib

PyTorch for model definition and training

Torchdiffeq for Neural ODE integration

Cantera for data generation (autoignition modeling)

Kernel Density Estimation (KDE) for multi-scale sampling

📊 Dataset
36 hydrogen ignition cases

Simulated for 10 ms with timestep = 1e-6 s (10,000 steps per case)

10 state variables: 9 species mass fractions + temperature

Reduced using KDE-based multi-scale sampling (50 points per case)

🧠 Model Architecture
Encoder: 10 → 128 → 64 → 5 (ELU activations)

Neural ODE Function: 5 → 64 → 64 → 5 (latent dynamics)

Decoder: 5 → 64 → 128 → 10 (reconstruction)

ODE Solver: dopri5 with atol=1e-8, rtol=1e-7

Loss Function: L1 Loss

Learning Rate: 1e-4 with scheduler

Epochs: 1000

📈 Results
AE-NODE model accurately captures ignition delay and post-ignition dynamics

KDE sampling improves learning efficiency

Reduced stiffness allows use of explicit solvers

✅ How to Run
Clone the repository:

bash
Copy
Edit
git clone https://github.com/yourusername/h2-autoignition-node.git
cd h2-autoignition-node
Set up environment:

bash
Copy
Edit
pip install -r requirements.txt
Run sampling:

bash
Copy
Edit
jupyter notebook data_sampling_sb.ipynb
Train AE-NODE model:

bash
Copy
Edit
jupyter notebook h2_node_training_sp.ipynb
🔮 Future Work
Implement dual-phase sampling (pre- and post-ignition equally)

Integrate stiffness-aware loss functions or solvers

Extend to multi-dimensional and multi-fuel systems

Compare with other dimensionality reduction methods (PCA, VAEs)
