# Setup and reproducibility notes

## Current repository status

This repository snapshot contains documentation, a license, and a Git ignore file. The original ESP32 firmware, NodeMCU firmware, Streamlit application, trained model, and complete dependency list are not present. As a result, the end-to-end prototype cannot currently be launched from this repository alone.

This page deliberately does not invent a working installation command or claim that the software has been tested.

## Hardware described in the project report

- AD8232 ECG module and electrode patches
- ESP32 development board
- MAX30102 sensor
- NodeMCU ESP8266
- Laptop running the Python/Streamlit dashboard

## Software and services described

- Python and Streamlit
- TensorFlow model saved in Keras format
- JupyterLab and WFDB for model development
- Firebase Realtime Database
- PySerial and Requests
- VOSK, PyAudio or sounddevice, gTTS, pygame, and schedule for voice features
- Telegram Bot API

Exact versions and a complete dependency manifest were not supplied in the report.

## Steps needed to make this project reproducible

1. Add the original ESP32 firmware and NodeMCU firmware source.
2. Add the Streamlit application and signal-preprocessing modules.
3. Provide a model artifact or a documented training notebook and instructions for obtaining the dataset.
4. Add a tested requirements.txt with exact package versions.
5. Document Firebase setup, database rules, expected data schema, and authentication.
6. Document serial-port selection and the expected format of NodeMCU vital readings.
7. Add tests for preprocessing and inference, plus a small synthetic sample that contains no personal health data.
8. Verify the complete flow on the actual hardware before describing it as runnable.

## Secrets and configuration

Never commit Firebase service-account files, database secrets, Wi-Fi credentials, Telegram bot tokens, patient information, or real sensor logs. Use environment variables or a local, ignored configuration file. The .env.example file contains placeholder names only; update it to match the original code when that code is restored.

## Safety

This is a research/educational prototype and is not a substitute for medical-grade equipment or professional medical advice.
