# 🔬 Stiff Neural ODE Modeling of Hydrogen Autoignition

This repository presents a deep learning-based framework that models stiff hydrogen-air ignition dynamics using **Autoencoder-Neural ODE (AE-NODE)** architectures. The model reduces stiffness, compresses data using latent embeddings, and accurately simulates combustion reactions with reduced computational cost.

> 🧪 Built using Cantera simulations, multiscale KDE sampling, and PyTorch-based Neural ODE solvers.

---

📁 Project Structure
.
├── data_sampling_sb.ipynb         # KDE + random sampling of Cantera output
├── h2_node_training_sp.ipynb      # AE-NODE training and validation
├── solution_data/                 # Raw ignition simulation data (CSV)
├── sampled_multiscale_50/         # KDE-sampled reduced dataset
├── models/                        # Trained model weights (.pt)
├── plots/                         # Result visualizations and training loss
└── README.md                      # Project overview and usage guide


## 🚀 Getting Started

### 🛠️ Requirements

- Python 3.8+
- PyTorch
- NumPy
- SciPy
- scikit-learn
- matplotlib
- Cantera (for data generation, optional)

```bash
pip install -r requirements.txt
⚙️ Run Instructions
1. 🧪 Sampling
Generate reduced training data using KDE and random techniques:

python
Copy
Edit
# Run inside data_sampling_sb.ipynb
# INPUT: solution_data/*.csv
# OUTPUT: sampled_multiscale_50/*.csv
2. 🧠 Train AE-NODE Model
python
Copy
Edit
# Run inside h2_node_training_sp.ipynb
# Defines encoder, decoder, ODE function, and trains the model
