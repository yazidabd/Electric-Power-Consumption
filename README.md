# ⚡ Power Consumption Forecasting (Time Series Machine Learning)

## 🧭 Ringkasan Proyek
Proyek ini bertujuan untuk **memprediksi konsumsi listrik (PowerConsumption_Zone1)** menggunakan pendekatan **Machine Learning berbasis Time Series**.  
Eksperimen dilakukan dengan beberapa algoritma seperti **Linear Regression** dan **XGBoost**, serta dilakukan **Hyperparameter Tuning** untuk meningkatkan performa model.

---

## 📂 Dataset
Link: https://www.kaggle.com/datasets/fedesoriano/electric-power-consumption/   
Berisi data konsumsi listrik per 10 menit dengan fitur tambahan seperti cuaca dan arus cahaya difus.  

### 🔹 Kolom Utama:
| Kategori | Fitur |
|-----------|--------|
| Target | `PowerConsumption_Zone1` |
| Cuaca | `Temperature`, `Humidity`, `WindSpeed`, `GeneralDiffuseFlows`, `DiffuseFlows` |
| Waktu | `Datetime` (interval 10 menit) |

---

## 🧹 1. Data Preparation
### Langkah-langkah:
1. **Konversi dan Atur Index**
   - Mengubah kolom `Datetime` ke format `datetime` dan menjadikannya sebagai index waktu.
   - Urutkan index agar berurutan dan konsisten.
2. **Cek kelengkapan data**
   - Pastikan tidak ada timestamp duplikat atau hilang.
3. **Eksplorasi awal (EDA)**
   - Visualisasi konsumsi listrik harian, hubungan dengan suhu, dan heatmap korelasi antar fitur.

---

## 🧠 2. Feature Engineering
Tujuan dari tahap ini adalah agar model bisa mengenali **pola waktu, musiman, dan perilaku historis konsumsi**.

| Jenis | Fitur | Penjelasan |
|-------|--------|------------|
| Waktu | `hour`, `day`, `month`, `day_of_week`, `is_weekend` | Menangkap pola harian dan mingguan |
| Lag | `lag_10min`, `lag_30min`, `lag_1h`, `lag_1d` | Representasi konsumsi pada waktu sebelumnya |
| Rolling | `rolling_1h`, `rolling_6h`, `rolling_24h` | Rata-rata bergerak untuk tren jangka pendek |

> Setelah proses shift dan rolling, baris dengan nilai NaN dihapus agar data bersih dan siap dilatih.

---

## 🔍 3. Model Training & Evaluation
Dataset dibagi menjadi:
- **Train:** 80%
- **Test:** 20%

### Model yang diuji:
1. **Linear Regression (Baseline)**
2. **XGBoost Regressor**
3. **XGBoost (Hyperparameter Tuning dengan RandomizedSearchCV)**

---

## 📊 4. Hasil Evaluasi

| Model | MAE | RMSE |
|-------|------|------|
| Linear Regression | **216.86** | **319.84** |
| XGBoost (default) | 321.19 | 524.63 |
| XGBoost (tuning) | 250.69 | 370.49 |

📈 **Kesimpulan:**
- Model **Linear Regression** memberikan hasil terbaik pada dataset ini.  
- Hal ini mengindikasikan bahwa **hubungan antar variabel bersifat cukup linear**, sehingga model kompleks seperti XGBoost tidak memberikan peningkatan signifikan.  
- Meskipun XGBoost dioptimasi melalui tuning, performanya masih di bawah baseline linear model.

---

## 📈 5. Visualisasi Prediksi vs Aktual
Contoh 200 titik terakhir dari data uji:

![comparison baseline](https://github.com/yazidabd/Electric-Power-Consumption/blob/main/assets/baselin%20model.png)

Terlihat bahwa **Linear Regression** mengikuti pola aktual dengan cukup baik, sedangkan XGBoost cenderung sedikit overfitting terhadap data pelatihan.

---

## 🧩 6. Insight Penting
- Konsumsi listrik memiliki **pola musiman dan harian** yang jelas.
- **Suhu dan kelembapan** mempengaruhi tingkat konsumsi (misal: penggunaan AC meningkat pada suhu tinggi).
- **Lag dan rolling features** membantu menangkap dinamika jangka pendek dalam konsumsi.

---

## 🧰 7. Tools & Library
- **Python** (pandas, numpy, matplotlib, seaborn)
- **Scikit-learn**
- **XGBoost**
- **Jupyter Notebook**

---

## 👤 Author
**Yazid Abdullah Subhi**  
_Data Enthusiast | data analyst & data science_  
📧 [yazidabdhi@gmail.com](mailto:yazidabdhi@gmail.com)

---

