# project# 
🗣️ Voice Disorder Classification Model

Welcome! This is a lightweight neural network designed to classify human voice samples as either **Healthy** or **Pathological**.

It’s built as a research prototype to demonstrate how voice-derived acoustic features can be paired with machine learning for screening purposes.

## 🚀 How It Works

The entire inference pipeline is straightforward and fast:

1. **Audio Input**: Feed the system a WAV voice recording.
2. **Feature Extraction**: It extracts 60 Mel-frequency cepstral coefficients (MFCCs) using Librosa (30 means + 30 standard deviations).
3. **Scaling**: Features are standardized using the training data's mean and scale.
4. **Neural Network**: Data passes through a tiny two-layer network.
5. **Output**: It outputs a probability. If `P(Pathological) >= 0.5`, it flags the sample as Pathological.

## 🧠 Model Architecture

Because the model is lightweight, it's perfect for embedded systems or edge devices.

* **Input**: 60-dimensional feature vector.
* **Hidden Layer**: Dense layer with 256 neurons (ReLU activation).
* **Output Layer**: Dense layer with 1 neuron (Sigmoid activation).
* **Size**: Only 15,873 trainable parameters.

## 📊 Dataset & Performance

The model was trained on a balanced dataset of **2,094 WAV samples** (1,047 Healthy / 1,047 Pathological) using a 90/10 train-test split and 5-fold cross-validation.

**Test Set Results (210 unseen samples):**

* **Accuracy**: 69.05%
* **Sensitivity**: 64.76%
* **Specificity**: 73.33%
* **ROC-AUC**: 75.29%

**Confusion Matrix:**

|  | Predicted Healthy | Predicted Patho |
| --- | --- | --- |
| **Actual Healthy** | 77 | 28 |
| **Actual Patho** | 37 | 68 |

## 📦 What's Included?

If you run the training pipeline, you'll get three main outputs:

* `voice_disorder_model.keras`: The ready-to-use TensorFlow/Keras model.
* `voice_disorder_scaler.pkl`: The exact scaler used during training (required for preprocessing new audio).
* `network_weights_256/`: The raw weight matrices (`W1`, `b1`, `W2`, `b2`). We export these so you can easily rebuild the model outside of TensorFlow—like in MATLAB, C++, or directly on an FPGA.

## 🖥️ Tech Stack

* Python
* TensorFlow 2.20.0
* Librosa 0.11.0

---

### ⚠️ Important Medical Disclaimer

*This project is a research prototype. With a test accuracy of ~69%, **this model must not be used as a standalone medical diagnostic tool**. It is intended strictly for educational, research, and screening-demonstration purposes. Further clinical validation is required before any real-world healthcare application.*
