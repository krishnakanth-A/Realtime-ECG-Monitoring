# Realtime ECG Monitoring System

An academic IoT and deep-learning prototype for acquiring ECG signals, monitoring pulse rate and SpO₂, classifying ECG waveforms, and presenting readings through a Streamlit dashboard with Firebase synchronization and Telegram notifications.

> **Project status:** Academic prototype completed in April 2025. This documentation is based on the project report, IP REPORT.pdf. The report describes the system design and final prototype, but this repository currently contains only a README, license, and Git ignore file. The original application source, trained model, and firmware are not currently included here.

## Overview

The system combines sensor-based acquisition, cloud communication, laptop-based inference, and user notifications. The ESP32 acquires ECG samples from an AD8232 module and sends buffered readings to Firebase Realtime Database. A separate NodeMCU ESP8266 reads the MAX30102 optical sensor for pulse rate and SpO₂. A Python/Streamlit application running on a laptop retrieves the ECG data, runs the saved TensorFlow model, and displays the results.

## Key features documented in the project report

- **ECG acquisition:** AD8232 analog front end connected to an ESP32; approximately 360 Hz sampling is described in the report.
- **Pulse and oxygen monitoring:** MAX30102 connected to a NodeMCU ESP8266 using I²C.
- **Cloud data transfer:** Firebase Realtime Database used for temporary ECG batch storage and synchronization.
- **ECG classification:** TensorFlow model described as a CNN–Transformer / Transformer encoder approach with five output classes.
- **Dashboard:** Streamlit interface for waveform visualization, classification, and vital readings.
- **Telegram bot:** On-demand status messages and warnings for hardware, serial, or Firebase connectivity problems.
- **Voice assistant:** VOSK-based keyword recognition for “help”/“SOS” alerts, plus scheduled medication and hydration reminders using gTTS and pygame.
- **Data management:** The report describes clearing older Firebase samples when a configured storage threshold is exceeded.

## System architecture

~~~mermaid
flowchart LR
    A[ECG electrodes] --> B[AD8232]
    B --> C[ESP32 ADC and buffer]
    C --> D[Firebase Realtime Database]
    D --> E[Python / Streamlit on laptop]
    E --> F[Signal preprocessing]
    F --> G[Saved TensorFlow model]
    G --> H[ECG class and live dashboard]
    I[MAX30102 PPG sensor] --> J[NodeMCU ESP8266]
    J --> E
    E --> K[Telegram bot]
    L[VOSK voice assistant] --> K
~~~

The inference model runs on the laptop, **not on the ESP32**. The report describes the ESP32 as the acquisition and upload device.

## Hardware and software

| Area | Components / tools described in the report |
|---|---|
| ECG acquisition | ECG electrodes, AD8232, ESP32 |
| Pulse / SpO₂ | MAX30102, NodeMCU ESP8266 |
| Cloud | Firebase Realtime Database |
| Model development | Python, JupyterLab, TensorFlow, WFDB |
| Dashboard | Streamlit |
| Serial / API communication | PySerial, Requests |
| Voice features | VOSK, PyAudio or sounddevice, gTTS, pygame, schedule |
| Notifications | Telegram Bot API |

## ECG classes

The model is described as classifying five categories:

- **Normal**
- **APC** — Atrial Premature Contraction
- **PVC** — Premature Ventricular Contraction
- **LBBB** — Left Bundle Branch Block
- **RBBB** — Right Bundle Branch Block

## Signal processing and model approach

The report describes analog filtering through the AD8232 circuitry, lead-off detection, R-peak detection and beat segmentation, P/Q/R/S/T morphology feature extraction, and normalization. Sequences are described as being padded or truncated to 100 time steps. Training is documented in JupyterLab with an 80:20 training/validation split, categorical cross-entropy, Adam optimizer (learning rate 0.001), noise injection and random-shift augmentation, checkpointing, and early stopping.

The report mentions WFDB waveform data and refers to the MIT-BIH Arrhythmia Database in its background and bibliography. The exact dataset records, final numeric evaluation results, and reproducible evaluation files are not included in this repository at present.

## Repository contents

~~~text
Realtime-ECG-Monitoring/
├── README.md
├── LICENSE
├── .gitignore
├── .env.example
└── docs/
    ├── architecture.md
    ├── hardware-and-signal-processing.md
    └── setup-guide.md
~~~

The documentation files are being added from the April 2025 project report. The source code, firmware, trained model, and runnable dependency lockfile are not available in this repository snapshot, so this repository is **not yet a reproducible, runnable release**.

## Documentation

- [System architecture](docs/architecture.md)
- [Hardware and signal processing](docs/hardware-and-signal-processing.md)
- [Setup and reproduction notes](docs/setup-guide.md)

## Results and limitations

The report documents an integrated prototype and includes photographs of the sensor setup, Telegram output, and Streamlit dashboard. It describes the model results qualitatively, but does not provide a numeric final accuracy value or a machine-readable classification report in the submitted report. No accuracy figure is claimed here.

This is an **academic proof of concept**, not a medical device. ECG classifications and vital readings must not be used as a diagnosis or to make treatment decisions. Blood-pressure values are described as calculated/estimated by the prototype and should not be treated as clinically validated measurements. The system has not been established as clinically validated in the report.

## Future work listed in the report

- Extend Firebase data retention.
- Add temperature, respiration rate, and stress-related metrics.
- Improve the front end using HTML, CSS, and JavaScript.
- Develop a doctor-facing application with history tracking and scheduled reports.

## Team and acknowledgement

This was a group project submitted to the Department of Electronics and Communication Engineering, PSG College of Technology, in April 2025. The report lists Aaditya Prakaash J, Krishnakanth A, Mithun Hari K, and Mugundan K as team members.

## License

Released under the MIT License. See [LICENSE](LICENSE).
