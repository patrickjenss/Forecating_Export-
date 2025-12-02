# Forecating_Export-
Forecast for potential export indonesia in 2026

## Forecasting Ekspor Indonesia dengan SARIMA

Proyek ini bertujuan untuk memodelkan dan mem-forecast nilai **ekspor bulanan Indonesia** menggunakan pendekatan **time series SARIMA (Seasonal ARIMA)**. Data historis berasal dari publikasi Badan Pusat Statistik (BPS) untuk periode **Januari 2018 – September 2025** (frekuensi bulanan).

### Tujuan Proyek

- Membangun model time series yang mampu memproyeksikan **12 bulan ke depan**.
- Mengevaluasi akurasi model menggunakan **MAPE** dan **RMSE**.
- Menyediakan visualisasi tren historis, backtest, dan forecast berikut **confidence interval**.
- Memberikan insight sederhana terkait pola ekspor Indonesia dan implikasi bisnisnya.

### Metodologi Singkat

1. **Data Ingestion & Cleaning**  
   - Mengambil data dari database PostgreSQL (kredensial disembunyikan di repo publik).  
   - Konversi kolom tanggal ke `datetime`, set sebagai index, dan set frekuensi bulanan.

2. **Eksplorasi & Stasioneritas**  
   - Visualisasi deret waktu dan dekomposisi tren–musiman.  
   - Uji **ADF** dan **KPSS** untuk menentukan kebutuhan differencing.  
   - Analisis **ACF** dan **PACF** sebagai dasar pemilihan orde model.

3. **Pemodelan SARIMA/SARIMAX**  
   - Pencarian awal orde dengan `auto_arima`.  
   - Eksperimen model dengan dan tanpa variabel eksogen (dummy COVID).  
   - Pemilihan model final **SARIMA(0,1,1)(0,1,1,12)** berdasarkan **AIC** dan diagnostik residual.

4. **Evaluasi Model**  
   - Split data menjadi **train (~88%)** dan **test (12 bulan terakhir)**.  
   - Perhitungan **MAPE ≈ 5%** dan **RMSE** pada test set.  
   - Plot historis, backtest, dan forecast 12 bulan ke depan + interval kepercayaan.

5. **Output**  
   - Tabel `forecast_final` yang berisi nilai **forecast**, **lower_ci**, dan **upper_ci** untuk 12 bulan ke depan.  
   - DataFrame gabungan historis + forecast untuk analisis lanjutan.

### Cara Menjalankan

1. Clone repository ini.
2. Buat dan aktifkan environment Python (opsional namun direkomendasikan).
3. Install dependensi utama (contoh):
   ```bash
   pip install -r requirements.txt
   ```
4. Pastikan koneksi ke database atau ganti blok pengambilan data dengan file CSV lokal.
5. Buka notebook utama (`forecast_export2.ipynb`) dan jalankan sel secara berurutan.

> **Catatan:**  
> - Kredensial database **tidak** disertakan di repo publik. Gunakan file konfigurasi lokal atau variabel environment.  
> - Proyek ini berfokus pada demonstrasi proses end-to-end forecasting time series untuk keperluan pembelajaran dan portofolio.

### Pengembangan Lanjutan

Beberapa ide yang dapat dikembangkan ke depan:

- Menguji model lain seperti **Prophet**, **ETS**, atau model berbasis machine learning (XGBoost/LightGBM) dengan fitur kalender.  
- Menambahkan **rolling backtest** untuk mengevaluasi stabilitas performa model dari waktu ke waktu.  
- Membangun dashboard interaktif (misalnya dengan Streamlit) untuk menampilkan hasil forecast ke user non-teknis.
