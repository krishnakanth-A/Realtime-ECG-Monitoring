# Hardware and signal processing

Based on the project report submitted in April 2025.

## Hardware

| Component | Role documented in the report |
|---|---|
| ECG electrodes / patches | Pick up the electrical signal |
| AD8232 | ECG analog front-end with conditioning and lead-off signals |
| ESP32 | Digitizes ECG using its ADC, buffers samples, and uploads them over Wi-Fi |
| MAX30102 | Optical red/IR sensing for pulse rate and SpO₂ |
| NodeMCU ESP8266 | Reads MAX30102 over I²C and forwards readings over serial |
| Laptop | Runs Streamlit and model inference |

The report specifies approximately 360 Hz ECG sampling and gives an example batch size of 360 samples. It describes the MAX30102 SDA/SCL connections to NodeMCU GPIO4 (D2) and GPIO5 (D1).

## Signal-processing flow

1. **Analog conditioning:** The report describes high-pass and low-pass filtering through the AD8232 circuitry to reduce baseline drift and interference.
2. **Lead-off checks:** Electrode disconnection is detected to help prevent invalid readings.
3. **Digitization and buffering:** The ESP32 samples the ECG waveform and uploads batches.
4. **Beat segmentation:** R-peak detection is used to isolate beats.
5. **Morphology features:** The report discusses P-wave amplitude/duration, QRS width and R-peak height, ST slope, T-wave polarity/duration, and RR interval.
6. **Normalization:** Z-score and Min–Max normalization are described.
7. **Fixed-length input:** Sequences are padded or truncated to 100 time steps.
8. **Classification:** A TensorFlow CNN–Transformer / Transformer encoder model predicts one of five classes: Normal, APC, PVC, LBBB, or RBBB.

## Training approach documented

The report describes JupyterLab, WFDB waveform data, an 80:20 training/validation split, categorical cross-entropy, Adam with learning rate 0.001, noise injection and random shifting, checkpoints, and early stopping.

The report does not include a numeric final accuracy value, the exact record-level split, a full class-wise metrics table, or the model artifact in the current repository. Do not infer or publish performance figures until those artifacts are available.

## Safety note

This is an educational prototype. Sensor readings can be affected by placement, motion, noise, calibration, and implementation limitations. The report does not establish clinical validation. Do not use its predictions or estimated blood-pressure values to diagnose or treat a medical condition.
