# AI-Enabled Intrusion Detection and Adaptive Heterogeneous D2D Communication Framework

**Authors:** Siddharth Anand & Tathagat Parashar  
**Institution:** Vellore Institute of Technology (VIT), School of Electronics Engineering  

## Project Overview
This repository contains the simulation models, cryptographic scripts, and deep learning architectures for a multi-layered security framework designed for 5G and Beyond 5G (B5G) Vehicular Ad-hoc Networks (VANETs). By leveraging decentralized Device-to-Device (D2D) communication, this system addresses the latency constraints of traditional cellular infrastructure while mitigating the unique security vulnerabilities of open vehicular networks. 

To overcome the inherent "Security-Latency Trade-off," this project integrates an adaptive physical-layer link selection protocol, a lightweight 256-bit Elliptic Curve Diffie-Hellman (ECDH) cryptographic foundation, and an AI-driven CNN-LSTM behavioral intrusion detection system.

![Multi-Layer Workflow](docs/multi_layer_workflow.png)

---

## Multi-Layered Defense Architecture

### 1. Adaptive Link Selection (Physical Layer)
The framework utilizes a multi-interface On-Board Unit (OBU) to dynamically switch between three spectrum layers based on real-time Signal-to-Noise Ratio (SNR) and inter-vehicular distance:

![Heterogeneous Architecture](docs/heterogeneous_architecture.png)

*   **Mode 1 (Visible Light Communication - VLC):** Optimal for strict Line-of-Sight (LoS) distances under 5 meters, ensuring high throughput and physical security.
*   **Mode 2 (mmWave):** Utilizes the 28 GHz frequency for medium-range connectivity between 5 and 30 meters.
*   **Mode 3 (Sub-6 GHz):** Serves as a reliable fallback for Non-Line-of-Sight (NLOS) and long-range excursions exceeding 30 meters.

![SNR Decay Analysis](docs/snr_decay_analysis.png)
*Comparative SNR decay analysis mapping the sharp degradation of VLC against the sustained viability of mmWave over distance.*

### 2. Lightweight Cryptography (Session Layer)
*   Implements an optimized 256-bit ECDH key exchange on the NIST p256 curve (secp256r1).
*   Provides security parity with legacy 3072-bit RSA frameworks while drastically reducing the computational burden on resource-constrained OBUs.
*   Achieves a Key Agreement Success Rate (KASR) of **0.9880**, outperforming traditional Diffie-Hellman (0.9580) and RSA (0.9790) protocols in highly dynamic vehicular environments.

### 3. AI-Driven Intrusion Detection (Behavioral Layer)
The system features a hybrid CNN-LSTM deep learning engine that analyzes encrypted traffic metadata, completely bypassing the massive processing overhead of Deep Packet Inspection (DPI).

![CNN-LSTM Architecture](docs/cnn_lstm_architecture.png)

*   The **1D-CNN layer** extracts spatial micro-patterns in packet bursts.
*   The **Bi-LSTM layer** maps long-term temporal dependencies.
*   Monitors Inter-Arrival Time (IAT), transmission frequency, packet size distribution, and timestamp jitter to detect advanced anomalies.

---

## Threat Mitigation Performance
The system addresses multiple threat vectors without requiring payload decryption:

*   **Flooding & DoS Attacks:** Detected via LSTM temporal tracking of packet bursts, achieving a **98.6% overall accuracy**.
*   **Fuzzy Injection:** Identified with a remarkably low False Negative Rate (FNR) of **1.9%**, far surpassing baseline Random Forest (11.6%) and standard LSTM (7.9%) models.

![Confusion Matrix](docs/confusion_matrix.png)
*Confusion matrix confirming precise threat classification with a 1.9% False Negative Rate against obfuscated fuzzy attacks.*

![ROC Curves](docs/roc_curves.png)
*Receiver Operating Characteristic (ROC) curves proving the classification superiority of the CNN-LSTM framework across diverse threat vectors.*

---

## Repository Structure
*   `/ai_ids_model`: Contains the TensorFlow/Keras implementation of the hybrid CNN-LSTM architecture and data preprocessing scripts for Min-Max scaling.
*   `/crypto_module`: Python scripts executing the ECDH session initialization, parameter consensus, and HKDF-SHA256 key extraction.
*   `/ns3_simulations`: Network simulation configurations mapping vehicular mobility and link-state dynamics across 5.9 GHz, 28 GHz, and 400-800 THz spectrums.
*   `/docs`: System architecture flowcharts, mathematical performance graphs, and evaluation logs.
