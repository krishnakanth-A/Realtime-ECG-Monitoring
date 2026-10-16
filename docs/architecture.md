# System architecture

This document summarizes the architecture described in the April 2025 project report.

## Data flow

1. ECG electrodes feed the AD8232 analog front-end.
2. The ESP32 samples the conditioned analog signal, buffers samples, performs lead-off checks, and uploads batches over Wi-Fi to Firebase Realtime Database.
3. A laptop application built with Python and Streamlit polls Firebase and preprocesses the newest ECG batch.
4. The saved TensorFlow model performs classification on the laptop. Inference is not performed on the ESP32.
5. The Streamlit interface visualizes the waveform and displays the predicted class and vital readings.
6. A separate NodeMCU ESP8266 reads the MAX30102 sensor over I²C and forwards pulse/SpO₂ data to the laptop interface.
7. The Telegram bot provides status responses and connection-error notifications. The voice assistant can trigger an SOS Telegram message.

## Architecture diagram

~~~mermaid
flowchart TD
    subgraph ECG["ECG acquisition"]
        E[Electrodes] --> A[AD8232 analog front end]
        A --> M[ESP32 ADC / sample buffer]
        M -->|Wi-Fi JSON batches| F[(Firebase Realtime Database)]
    end
    subgraph PPG["Optical vital acquisition"]
        S[MAX30102] -->|I²C| N[NodeMCU ESP8266]
        N -->|Serial data| U[Streamlit laptop application]
    end
    F --> U
    U --> P[Normalization / padding]
    P --> T[TensorFlow CNN–Transformer / encoder model]
    T --> D[Classification and dashboard]
    U --> B[Telegram status and error notifications]
    V[VOSK voice keyword detection] --> B
~~~

## Data handling described in the report

- ECG readings are uploaded as JSON arrays under a user-specific Firebase path documented as /UsersData/<UID>/ecgReadings.
- Batches are timestamped using the device's millisecond counter.
- The firmware is described as removing older readings when a configured sample-count threshold is exceeded.
- The Streamlit application repeatedly fetches recent data and applies the saved model.

## Implementation boundary

This diagram reflects the report and is not a source-code audit. The current public repository snapshot does not include the firmware, Python application, model file, Firebase rules, or deployment configuration. Therefore, exact API contracts, threading behavior, error handling, and timing have not been independently verified.
