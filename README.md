# Realtime-ECG-Monitoring
IoT + AI based real-time ECG classification system with voice assistant and Telegram alerts
# ⚡ Realtime ECG Monitoring System Using IoT + AI

A low-cost, real-time, AI-powered health monitoring system for arrhythmia detection, built using ECG and PPG sensors, cloud integration, and a Transformer-based deep learning model. Designed to assist remote and elderly patients with live classification, alerts, and voice-activated emergency support.

---

## 🚀 Features

- 🫀 **ECG Signal Acquisition** using AD8232 and ESP32
- 💓 **Heart Rate & SpO₂ Monitoring** using MAX30102 and NodeMCU
- 🤖 **Transformer-Based Arrhythmia Classification** (Trained on MIT-BIH Dataset)
- 📊 **Streamlit Web Dashboard** with Live ECG Plotting & Predictions
- 📦 **Firebase Realtime Database** Integration for Live Data Sync
- 📢 **Telegram Bot** for Alerts, Status, and Error Notifications
- 🗣️ **Voice Assistant** with SOS Trigger and Smart Reminders (Offline)
- 🧠 **Trained on WFDB Waveform Data** with Custom Preprocessing
- 🔐 Modular, Open-Source, and Designed for Edge Deployment

---

## 🧠 Tech Stack

| Layer          | Tools / Libraries                                    |
|----------------|------------------------------------------------------|
| Hardware       | ESP32, NodeMCU, AD8232, MAX30102                     |
| Cloud          | Firebase Realtime Database                          |
| AI Model       | TensorFlow, Transformer Encoder, JupyterLab         |
| Frontend       | Streamlit (Real-Time Dashboard)                     |
| Backend        | Python, PySerial, Requests                          |
| Voice Control  | VOSK (Offline Speech Recognition), gTTS, Pygame     |
| Bot Alerts     | Telegram Bot API                                    |

---

## 🖼️ Live Dashboard Preview

> 🔗 *Coming soon: Hosted demo link or screenshots*

---

## 📁 Project Structure

---Realtime-ECG-Monitoring/
├── hardware/
│   ├── ecg_esp32_firebase.ino          # ECG acquisition via ESP32
│   ├── max30102_nodemcu.ino            # BPM and SpO2 reading via NodeMCU
│   └── circuit_diagrams.png            # Schematics for hardware
│
├── model/
│   ├── ecg_transformer_model.keras     # Trained deep learning model
│   ├── training_notebook.ipynb         # JupyterLab training code
│   └── wfdb_preprocessing.py           # WFDB data loading & preprocessing
│
├── web_dashboard/
│   ├── app.py                          # Streamlit app (ECG + vitals)
│   ├── requirements.txt                # Python dependencies
│   └── screenshots/                    # Screenshots of the dashboard
│
├── voice_assistant/
│   └── voice_sos_assistant.py          # VOSK-based voice alert system
│
├── telegram_bot/
│   └── bot_integration.py              # Telegram bot code (alerts + status)
│
├── firebase_config/
│   └── firebase_credentials.json       # Firebase DB connection file
│
├── LICENSE                             # MIT License
├── README.md                           # This file
└── .gitignore                          # Files to ignore when pushing


## 🧪 Arrhythmia Classes Detected

- ✅ Normal
- ⚡ PVC (Premature Ventricular Contraction)
- 🔁 LBBB (Left Bundle Branch Block)
- 🔄 RBBB (Right Bundle Branch Block)
- ❗ APC (Atrial Premature Contraction)

---

## 🔒 Disclaimer

- This project is for **educational and research purposes** only.
- Not a substitute for medical-grade ECG equipment.
- Always consult a healthcare professional for diagnosis.

---

## ✨ Contributors

- 👨‍💻 [Krishnakanth](https://github.com/krishnakanth-A) — AI + Embedded Developer
- 💬 Feel free to open issues or contribute improvements!

---

## 📜 License

This project is licensed under the **MIT License** — feel free to use, modify, and share with credit.

---


