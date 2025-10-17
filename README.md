# Predicting Sleep Using Consumer Wearable Sensing Devices

###  Team 32 — PES University

**Members: Nikitha P (PES2UG23CS389), Vaishnavi Narepalepu (PES2UG23CS367)

---

##  Problem Statement

Consumer wearable devices (like smartwatches) are widely used for sleep tracking, but their accuracy compared to clinical methods like **Polysomnography (PSG)** remains uncertain.
This project bridges that gap by using **machine learning** to analyze EEG-based, accelerometer-like data and classify whether a person is **asleep (1)** or **awake (0)**.

---

##  Objective

Develop a machine learning model that:

* Accurately distinguishes between **sleep** and **wakefulness**
* Uses **statistical and signal-based EEG features** (mean, variance, RMS, energy, etc.)
* Achieves high accuracy with **lightweight, interpretable models**
* Demonstrates how wearable devices can estimate sleep patterns reliably

---

##  Dataset Details

* **Source:** [Sleep-EDF Expanded Dataset – PhysioNet](https://physionet.org/content/sleep-edfx/1.0.0/)
* **Data Type:** EEG polysomnography (PSG) with hypnogram annotations
* **Samples:** ~2,650 epochs (each 30 seconds)
* **Features Extracted (9):**

  * Mean, Median, Std, Variance, RMS, Max, Min, Energy, ZCR (Zero Crossing Rate)
* **Target Variable:**

  * `0` → Wake
  * `1` → Sleep

---

##  Methodology

### Step 1. **Data Acquisition**

* Downloaded EEG and Hypnogram `.edf` files from PhysioNet
* Loaded using **MNE (Magnetoencephalography and Electroencephalography)** library

### Step 2. **Preprocessing**

* Selected single EEG channel (`Fpz–Cz`)
* Resampled to a uniform frequency (100 Hz)
* Segmented continuous signal into **30-second epochs**
* Aligned each epoch with its corresponding sleep-stage label

### Step 3. **Feature Extraction**

Calculated 9 key time-domain features per epoch:

> Mean, Median, Std, Var, RMS, Max, Min, Energy, ZCR

### Step 4. **Label Encoding**

Mapped multi-class hypnogram labels into **binary** form:

> Wake = 0, Sleep = 1

### Step 5. **Model Development**

Trained and compared three models:

| Model               | Type      | Purpose                         |
| ------------------- | --------- | ------------------------------- |
| Logistic Regression | Linear    | Fast, interpretable baseline    |
| SVM (RBF Kernel)    | Nonlinear | Captures complex patterns       |
| Random Forest       | Ensemble  | Best accuracy, feature insights |

### Step 6. **Model Evaluation**

Used metrics: Accuracy, Precision, Recall, F1-Score, Confusion Matrix

| Model               | Accuracy | Precision | Recall |   F1 |
| ------------------- | -------: | --------: | -----: | ---: |
| Logistic Regression |     0.86 |      0.85 |   0.84 | 0.84 |
| Random Forest       |     0.92 |      0.91 |   0.93 | 0.92 |
| SVM (RBF)           |     0.89 |      0.88 |   0.88 | 0.88 |

**Best Model:** Random Forest — stable, high performance, interpretable feature importance.

**Top 4 Features:** RMS, Energy, Variance, Std — represent signal intensity and variability.

---

## 💻 Streamlit Web App

After completing the notebook, the project was extended into a **Streamlit UI** for easy, real-time use.

###  App Features

* Upload EEG data or use sample epochs
* Visualize waveform and extracted features
* Predict **Sleep / Wake** instantly using the trained Random Forest model
* Show accuracy, confusion matrix, and feature importance in a simple dashboard

###  Run the App

```bash
streamlit run streamlit_app.py
```

This turns the trained model into an interactive web tool — demonstrating how wearable devices could process and predict sleep states live.

---

##  Results Summary

* **Best Model:** Random Forest
* **Accuracy:** ~86%
* **Key Features:** RMS, Energy, Variance, Std
* **Conclusion:** EEG signals can simulate wearable sensor data effectively for binary sleep detection.

---

##  Conclusion

This project demonstrates that:

* EEG-based accelerometer-like data can classify **Sleep vs Wake** with over **90% accuracy**
* **Random Forest** provides robust performance and clear feature interpretability
* A simple **Streamlit interface** can make ML sleep prediction models accessible to everyone

By combining affordable wearable sensors with intelligent ML models, we move one step closer to **personalized, low-cost, and clinically reliable sleep tracking**.

---

