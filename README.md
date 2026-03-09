
# Privacy-Preserving Cascaded Federated Deep Learning for Nomophobia Risk Prediction

## Overview
This repository contains the implementation and experimental resources for the research paper:

**“Privacy-Preserving Cascaded Federated Deep Learning for Nomophobia Risk Prediction with Encrypted Masked Updates.”**

The project proposes a privacy-preserving federated deep learning (FL) framework designed to detect **nomophobia (smartphone dependency anxiety)** using smartphone behavioral data.

Unlike centralized machine learning systems, this framework keeps **raw user data on local devices** and shares only **protected model updates** with a coordinating server.

The approach integrates:
- Federated learning using **FedAvg aggregation**
- Differential privacy using **DP-SGD**
- **Encrypted transport of masked updates**
- Multiple **deep tabular models** for behavioral prediction

The system predicts three levels of nomophobia risk:
- Normal
- Mild
- Severe

---

# Research Motivation

Nomophobia is an emerging behavioral condition associated with excessive smartphone dependency. Many current screening approaches rely on **self-reported questionnaires**, which can be subjective and difficult to scale.

This research explores whether **smartphone usage telemetry** can provide an **objective and privacy-preserving method** for identifying nomophobia risk levels.

The proposed framework addresses three key challenges:

1. Detecting multi-level nomophobia risk from behavioral smartphone data  
2. Preserving user privacy during distributed model training  
3. Achieving high predictive accuracy under decentralized data settings  

---

# System Architecture

The system follows a **cross-silo federated learning architecture**.

### Client Side
Each client device:
1. Collects smartphone behavioral features
2. Preprocesses and encodes tabular data
3. Trains a local deep learning model
4. Generates protected model updates

Instead of sharing raw data, clients transmit **encrypted masked updates** to the server.

### Server Side
The central coordinator:
1. Receives encrypted updates
2. Decrypts the masked payload
3. Aggregates model parameters using **FedAvg**
4. Broadcasts the updated global model to all clients

This process repeats for multiple communication rounds until convergence.

---

# Dataset

The study uses the **Smartphone Usage and Behavioral Dataset** from Kaggle.

Original dataset size:
1,000 user records

To support deep learning experiments, the dataset is expanded using **constraint-aware tabular synthesis** to:

100,000 user records

Example features include:

| Feature | Description |
|------|------|
| Age | User age |
| Gender | Self-reported gender |
| Total_App_Usage_Hours | Daily total app usage |
| Daily_Screen_Time_Hours | Total daily screen time |
| Social_Media_Usage_Hours | Time spent on social media |
| Gaming_App_Usage_Hours | Time spent on gaming apps |
| Productivity_App_Usage_Hours | Time spent on productivity apps |
| Number_of_Apps_Used | Number of distinct applications used |
| Location | U.S. state-level geographic label |

A continuous **nomophobia risk score** is computed and converted into three categories:

Normal | Mild | Severe

---

# Machine Learning Models

The federated framework supports several deep tabular models:

- MLP (Multi-Layer Perceptron)
- CNN for tabular representation
- ResMLP
- Wide & Deep Network
- TabNet-style gated architecture

All models share the same **input–output interface** and produce logits corresponding to the three nomophobia classes.

---

# Privacy Mechanisms

The framework integrates multiple privacy protection strategies.

### Federated Learning
Raw smartphone usage data **never leaves the device**.

### Differential Privacy
Training uses **DP-SGD** with privacy parameters:
epsilon (ε) and delta (δ).

### Encrypted Masked Updates
Before transmission:
1. Gaussian masking is applied to the model update
2. The masked update is encrypted
3. The encrypted payload is sent to the server

This protects update confidentiality during communication.

---

# Training Configuration

Example experimental setup:

Federated Algorithm: FedAvg  
Number of Clients: 5  
Communication Rounds: 25  
Local Epochs: 3  
Batch Size: 32  
Learning Rate: 0.001  

---

# Evaluation Metrics

The models are evaluated using standard classification metrics:

- Accuracy
- Precision
- Recall
- F1 Score
- Matthews Correlation Coefficient (MCC)
- Area Under ROC Curve (AUC)

---

# Example Results

Best performing model:

MLP  
Accuracy: 99.12%  
F1 Score: 99.12%  
MCC: 0.9868  
AUC: 0.9997  

Wide & Deep model:

Accuracy: 98.95%

---

## Repository Structure

```
📦 Nomophobia-FL
 ┣ 📂 data
 ┃ ┣ raw_dataset.csv
 ┃ ┣ train_dataset.csv
 ┃ ┗ test_dataset.csv
 ┣ 📂 models
 ┃ ┣ mlp_model.py
 ┃ ┣ cnn_tabular_model.py
 ┃ ┣ resmlp_model.py
 ┃ ┗ tabnet_model.py
 ┣ 📂 federated
 ┃ ┣ client.py
 ┃ ┣ server.py
 ┃ ┗ aggregation.py
 ┣ 📂 privacy
 ┃ ┣ dp_sgd.py
 ┃ ┗ masked_update_encryption.py
 ┣ 📂 notebooks
 ┃ ┗ Nomophobia_FL_BestPerformance.ipynb
 ┗ README.md
```
---

# Installation

Clone the repository:

git clone https://github.com/yourusername/Nomophobia-FL.git
cd Nomophobia-FL

Install dependencies:

pip install -r requirements.txt

---

# Running the Experiment

Start the server:

python server.py

Run client nodes:

python client.py

---

# Citation

If you use this work in your research, please cite: Once published I will give the citations

---

# License
MIT License

---

# Acknowledgments
This research was conducted with collaboration among:

- Texas A&M University–Kingsville
- Khwaja Yunus Ali University
- West Virginia University Institute of Technology
- The University of Aizu
