# Virtual Lab Jaringan Saraf Tiruan (JST) — Supervised Learning

> **Aplikasi Simulasi Web Interaktif Pembelajaran Terawasi (*Supervised Learning*) Menggunakan Dataset Nyata Mahasiswa**  
> **Pengembang:** Muhammad Nailul Ghufron Majid  
> **Institusi:** Jurusan Teknik Informatika, Fakultas Sains dan Teknologi, Universitas Islam Negeri Maulana Malik Ibrahim Malang  
> **Mata Kuliah:** Kecerdasan Buatan (AI)  
> **Live Demo:** [https://nailulgh.github.io/virtual-lab-jst-mahasiswa/](https://nailulgh.github.io/virtual-lab-jst-mahasiswa/)

---

## 📌 Ringkasan Proyek

Proyek ini merupakan **Virtual Lab Interaktif JST** berbasis web (*single-page application*) yang dikembangkan untuk memenuhi tugas Artificial Intelligence. Aplikasi ini mengalihkan paradigma simulasi klasik (yang umumnya hanya mendemokan gerbang logika biner 2-input `AND`/`OR`) menjadi **laboratorium pelatihan dan evaluasi JST pada data tabular nyata** menggunakan dataset kelulusan mahasiswa ([`dataset_mahasiswa.csv`](./dataset_mahasiswa.csv)) serta mendukung pengunggahan file CSV bebas dari Kaggle/UCI.

Antarmuka dirancang dengan standar desain **Minimalist Swiss & Academic Workbench**, mengutamakan kenyamanan visual, hierarki fungsional yang tenang, responsivitas penuh (Mobile, Tablet, Laptop), serta dukungan tema **Light Mode (*Warm Paper*)** dan **Dark Mode (*Carbon Slate*)**.

---

## 🎯 Pemenuhan 6 Rincian Tugas

| No | Rincian Tugas Praktikum | Implementasi pada Aplikasi |
| :-: | :--- | :--- |
| **1** | **Menyiapkan dataset & menentukan kolom input serta target** | Menyediakan dataset bawaan `dataset_mahasiswa.csv` (221 baris) sekaligus tombol **Upload File CSV (`.csv`)**. Dilengkapi mesin **Smart Auto-Cleaner** untuk memfilter nilai kosong/strip (`-`) dan **Auto-Label Encoder** untuk mengubah target teks (`tepat`/`tidak tepat`, `sangat memuaskan`/`memuaskan`) menjadi label biner numerik `1` dan `0`. |
| **2** | **Menampilkan & menggunakan dataset di Virtual Lab** | Tabel dataset interaktif dengan pemisah **Data Latih (80%)** dan **Data Uji (20%)** melalui *systematic stratified split*, pemilih kolom fitur ($X_1 \dots X_n$) dan target ($t$), serta sakelar *toggle* **Nilai Asli vs Normalisasi Min-Max `[0, 1]`**. |
| **3** | **Pengaturan & proses pelatihan model JST** | Menyediakan 4 algoritma *Supervised Learning* (**Perceptron Rule**, **Delta Rule / LMS Widrow-Hoff**, **Backpropagation Multi-Layer Perceptron**, dan **Hebb Rule**), kontrol *Learning Rate* ($\alpha$), *Threshold* ($\theta$), *Max Epoch*, serta tombol **+1 Sampel**, **+1 Epoch**, **Auto-Run**, dan **Latih Selesai**. |
| **4** | **Menampilkan proses pembelajaran (bobot, epoch, error)** | Kanvas topologi JST dinamis (`#nnCanvas`) beresolusi tinggi, kartu bobot sinaptik $w_1 \dots w_n$ dan bias $b$ *real-time*, kurva konvergensi *Mean Squared Error* (MSE) per epoch (Chart.js), serta **Inspektor Perhitungan Matematis** per sampel. |
| **5** | **Pengujian langsung (input pengguna $\rightarrow$ prediksi)** | Formulir **Simulasi Prediksi Langsung** dengan input numerik dinamis sesuai fitur terpilih, tombol cepat **Contoh Kelas 1 (Lulus)** dan **Contoh Kelas 0 (Tidak)**, serta kalkulasi nilai net ($y_{in}$) dan skor aktivasi secara instan. |
| **6** | **Membandingkan hasil prediksi dengan target pada data uji** | Tabel **Daftar Hasil Prediksi vs Target Asli** pada data uji yang menyandingkan nilai fitur, $y_{in}$, target aktual ($t$), dan tebakan JST ($\hat{y}$) dengan indikator status `✓ Tepat` / `✗ Meleset`, dilengkapi **Akurasi (%)** dan **Confusion Matrix** (*TP, TN, FP, FN*). |

---

## 🧠 4 Algoritma JST yang Didukung

### 1. Perceptron Learning Rule (Rosenblatt)
Menggunakan fungsi aktivasi tangga biner (*step function*) terhadap nilai ambang (*threshold* $\theta$):
$$y_{in} = b + \sum_{i=1}^{n} x_i w_i$$
$$\hat{y} = \begin{cases} 1, & \text{jika } y_{in} \ge \theta \\ 0, & \text{jika } y_{in} < \theta \end{cases}$$
Pembaruan bobot hanya dilakukan saat terjadi kesalahan prediksi ($e = t - \hat{y} \neq 0$):
$$w_i^{(\text{baru})} = w_i^{(\text{lama})} + \alpha \cdot (t - \hat{y}) \cdot x_i$$
$$b^{(\text{baru})} = b^{(\text{lama})} + \alpha \cdot (t - \hat{y})$$

### 2. Delta Rule / Widrow-Hoff (Least Mean Square)
Meminimalkan kuadrat kesalahan secara kontinu dengan aktivasi linier:
$$e = t - y_{in}$$
$$w_i^{(\text{baru})} = w_i^{(\text{lama})} + \alpha \cdot e \cdot x_i$$
$$b^{(\text{baru})} = b^{(\text{lama})} + \alpha \cdot e$$

### 3. Backpropagation (Multi-Layer Perceptron / MLP)
Arsitektur multilapis ($N$ Input $\rightarrow$ 3 Hidden Neurons $\rightarrow$ 1 Output Neuron) dengan aktivasi *Sigmoid* kontinu:
$$f(z) = \frac{1}{1 + e^{-z}}$$
Gradien kesalahan lapisan keluaran diteruskan kembali (*backpropagated*) ke lapisan tersembunyi:
$$\delta_{\text{output}} = (t - \hat{y}) \cdot \hat{y} \cdot (1 - \hat{y})$$
$$\delta_{\text{hidden}, h} = \delta_{\text{output}} \cdot w_{2, h} \cdot z_h \cdot (1 - z_h)$$

### 4. Hebb Rule (Bipolar Correlation)
Mentransformasikan input dan target ke representasi bipolar $\{-1, +1\}$ untuk memperkuat bobot sinapsis yang memiliki korelasi positif:
$$w_i^{(\text{baru})} = w_i^{(\text{lama})} + \alpha \cdot x_{\text{bipolar}, i} \cdot t_{\text{bipolar}}$$

---

## 📊 Hasil Evaluasi Model pada `dataset_mahasiswa.csv`

Pengujian dilakukan atas **200 data valid** pada skenario **Prediksi Ketepatan Waktu Kelulusan** (`keterangan`: *tepat* vs *tidak tepat*) dengan pembagian **80% Data Latih (160 sampel)** dan **20% Data Uji (40 sampel)**:

| Algoritma JST | Akurasi Data Latih | Akurasi Data Uji | MSE Akhir | Status Konvergensi |
| :--- | :---: | :---: | :---: | :---: |
| **Perceptron Rule** | **100.0%** | **100.0%** | `0.0000` | Konvergen sempurna |
| **Backpropagation (MLP)** | **93.8%** | **94.9%** | `0.0124` | Sangat stabil & akurat |
| **Delta Rule (LMS)** | **90.7%** | **89.7%** | `0.0213` | Penurunan MSE konsisten |
| **Hebb Rule (Bipolar)** | **88.8%** | **89.7%** | `0.1118` | Cepat satu epoch |

---

## 💻 Fitur Antarmuka & UX Pro Max

1. **Dark Mode & Light Mode (*Token-Driven*):**
   - Transisi halus antara tema **Warm Paper** (latar `#F8FAFC`, kartu putih `#FFFFFF`) dan **Carbon Slate** (latar `#0B0F17`, kartu `#111827`).
   - Warna garis sinapsis pada kanvas dan kisi-kisi grafik Chart.js otomatis menyesuaikan tema aktif.
   - Pilihan tema tersimpan secara persisten di `localStorage`.
2. **Two-Tier Adaptive Header:**
   - Navigasi 3-tahap responsif yang otomatis berubah menjadi *Compact 3-Column Grid* di layar ponsel (`<640px`) tanpa ada geseran horizontal yang mengganggu.
   - Kapsul status telemetri *live* (Sampel Valid, Epoch aktif, Akurasi Uji) tersedia untuk desktop, tablet, maupun layar mobile.
3. **High-DPI Responsive Canvas (`#nnCanvas`):**
   - Penyesuaian skala dinamis mengikuti lebar layar tablet dan laptop untuk menjaga ketajaman garis dan teks node.
4. **Zero-Dependency Server:**
   - Seluruh pustaka (Tailwind CSS, Chart.js, Google Fonts) dimuat melalui CDN resmi, dan dataset bawaan telah ditanamkan langsung (*embedded*). Cukup buka file `index.html` dengan *double-click* di browser mana pun tanpa perlu menjalankan web server lokal.

---

## 🚀 Cara Menjalankan

### Cara 1: Buka Langsung di Browser (Offline / Lokal)
1. Buka folder `virtual_lab_jst_mahasiswa/`.
2. Klik ganda pada berkas [`index.html`](./index.html) atau [`virtual_lab_jst_mahasiswa.html`](./virtual_lab_jst_mahasiswa.html).
3. Halaman Virtual Lab akan langsung terbuka dan siap digunakan.

### Cara 2: Live Demo Online via GitHub Pages
Aplikasi ini dapat diakses secara langsung di browser tanpa instalasi melalui:  
👉 **[https://nailulgh.github.io/virtual-lab-jst-mahasiswa/](https://nailulgh.github.io/virtual-lab-jst-mahasiswa/)**

---

## 📂 Struktur Berkas

```
virtual_lab_jst_mahasiswa/
├── index.html                     # Entry point web untuk GitHub Pages & hosting publik
├── virtual_lab_jst_mahasiswa.html # Aplikasi Virtual Lab JST mandiri
├── dataset_mahasiswa.csv          # Dataset tabular kelulusan mahasiswa (221 baris)
└── README.md                      # Dokumentasi teknis & panduan penggunaan proyek
```

---

## 📜 Lisensi & Atribusi
Dikembangkan oleh **Muhammad Nailul Ghufron Majid** untuk keperluan akademik dan edukasi pembelajaran Jaringan Saraf Tiruan. Bebas digunakan dan dimodifikasi untuk tujuan pembelajaran.
#   v i r t u a l _ l a b _ j s t _ m a h a s i s w a 
 
 
