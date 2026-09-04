# DiaCare: Diabetes Risk Prediction Using Deep Learning & Machine Learning

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Latest-green.svg)

Proyek ini berfokus pada klasifikasi risiko penyakit diabetes (*No Diabetes*, *Prediabetes*, dan *Diabetes*) berdasarkan indikator gaya hidup dan kondisi kesehatan umum. Model ini dibangun menggunakan arsitektur **Multi-Layer Perceptron (MLP)** dan **XGBoost** untuk menangani permasalahan *imbalanced data*.

---

## 📌 Deskripsi Proyek & Dataset
Prediksi risiko diabetes dilakukan menggunakan **CDC Behavioral Risk Factor Surveillance System (BRFSS)** dari Kaggle yang terdiri dari **21 fitur gaya hidup** (seperti BMI, tekanan darah, aktivitas fisik, usia, dll.) dan **1 variabel target** (`Diabetes_012`).

### Tantangan Utama
* **Class Imbalance:** Mayoritas data didominasi oleh kelas *No Diabetes*, sedangkan kelas *Prediabetes* merupakan minoritas ekstrem.
* **Penanganan Data:** Menggunakan *stratified split* (80:20), *StandardScaler* untuk variabel non-biner, dan penyesuaian *class weights* (inverse frequency) untuk mengurangi bias model.

---

## 🛠️ Arsitektur & Pelatihan Model

| Model | Arsitektur / Konfigurasi Utama | Detail Training |
| :--- | :--- | :--- |
| **Multi-Layer Perceptron (MLP)** | 3 Hidden Layers (128, 64, 32 neurons) + Activation ReLU + Dropout (0.3) + Softmax Output | 50 Epochs, Batch Size 512, Adam Optimizer |
| **XGBoost** | 2000 Estimators, Learning Rate 0.02, Max Depth 5, Subsample/Colsample 0.8, Custom Sample Weights | Histogram-based (`tree_method='hist'`) |

---

## 📊 Hasil Evaluasi & Performa

Mengingat pentingnya mendeteksi pasien berisiko tinggi di domain medis, metrik evaluasi berfokus pada **Recall (Sensitivitas)** pada kelas minoritas.

| Kelas Target | Recall (MLP) | Recall (XGBoost) |
| :--- | :---: | :---: |
| **0: No Diabetes** | **83.8%** | **89.8%** |
| **1: Prediabetes** | **30.4%** | **25.5%** |
| **2: Diabetes** | **61.2%** | **63.5%** |

### Temuan Utama:
* **XGBoost** menunjukkan performa keseluruhan yang lebih stabil dan *recall* lebih tinggi pada kelas **Diabetes** (63.5%).
* **MLP** sedikit lebih unggul dalam mendeteksi kelas **Prediabetes** (30.4%), meskipun *false negative* pada kedua model masih tergolong tinggi.
* **Kesimpulan Medis:** Model ini belum ideal dijadikan alat diagnosis klinis definitif, tetapi sangat berguna sebagai **alat penapisan mandiri (*preliminary screening*)**.

