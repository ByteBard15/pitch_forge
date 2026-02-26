---

# Harmonic-Pulse: Native Audio Signal Analyzer

## 🎵 Project Overview

**Harmonic-Pulse** is a high-performance audio analysis engine written in C++ with a Node.js Addon interface. It processes raw audio signals to extract meaningful musical metadata and frequency-domain insights. By leveraging both **Discrete Fourier Transform (DFT)** and **Fast Fourier Transform (FFT)**, the project provides a playground for analyzing pitch, stability, and tonal shifts within a song.

---

## 🔬 Core Concepts: The Math of Sound

At its heart, this project converts audio from the **Time Domain** (amplitude over time) to the **Frequency Domain** (magnitude over frequency).

### 1. The Fourier Transform

We use the Fourier Transform to decompose complex audio waves into their constituent frequencies.

* **DFT (Discrete Fourier Transform):** The mathematical foundation. While computationally "expensive" at $O(N^2)$, it provides high precision for specific frequency bins.
* **FFT (Fast Fourier Transform):** An optimized algorithm that computes the same result in $O(N \log N)$ time, making real-time analysis possible.

The general formula for the DFT used in this project is:


$$X_k = \sum_{n=0}^{N-1} x_n \cdot e^{-\frac{i 2 \pi}{N} kn}$$

### 2. DSP Filtering

Before analysis, the signal is passed through various filters (Low-pass, High-pass) to isolate the "meat" of the audio and remove noise that could lead to inaccurate key detection.

---

## 📊 Extracted Metrics

The engine doesn't just "hear" the music; it calculates specific data points to define the "character" of a track:

| Metric | Description |
| --- | --- |
| **Average Key** | The most consistent dominant frequency throughout the track. |
| **Tonal Range** | The delta between the **Highest Key** and **Lowest Key** detected. |
| **Most Recurring Key** | The "Home Base" or Tonic frequency of the composition. |
| **Abrupt Changes** | A count of instances where the frequency shifts significantly within a narrow window (e.g., a key change or sudden bridge). |
| **The Greatest Change** | The single largest frequency jump recorded in the signal. |

---

## 🏗️ Architecture

### Native C++ Layer

* **Buffer Management:** Handles large arrays of audio samples efficiently.
* **Windowing Functions:** Applies Hanning or Hamming windows to the signal to prevent spectral leakage during FFT.
* **Peak Detection:** Algorithms to identify dominant spikes in the frequency spectrum.

### Node.js Addon (Future State)

* **Non-Blocking Analysis:** Offloads the heavy $O(N \log N)$ calculations to a separate thread so your JavaScript UI stays responsive.
* **Stream Processing:** Ability to pipe audio data directly from a Node.js stream into the C++ analyzer.

---

> [!NOTE]
> **Status:** This project is currently in the **Concept & Core Logic** phase. The C++ executable for CLI-based analysis is the primary focus, with the Node.js N-API wrapper currently in development.

---

## 🚀 Future Enhancements

* **BPM Detection:** Implementing autocorrelation to find the rhythmic pulse of the song.
* **Spectrogram Generation:** Exporting visual representations of the frequency analysis as image files.
* **Polyphonic Support:** Improving the algorithm to distinguish between multiple notes played simultaneously (chords).

---