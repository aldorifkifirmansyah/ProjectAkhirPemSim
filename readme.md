# Komputasi Sistem Antrean Bank Sumut KCP USU (Model M/M/s)

Repositori ini berisi implementasi program berbasis Python untuk mereplikasi, memvalidasi, dan mengoptimalkan kalkulasi analitis sistem antrean Customer Service (CS) pada Bank Sumut KCP USU berdasarkan penelitian empiris Januari 2026. Proyek ini dibuat untuk memenuhi tugas akhir matakuliah Pemodelan dan Simulasi, Program Studi Informatika, Universitas Jember.

## Anggota Kelompok

- **Aldo Rifki Firmansyah** (232410103025)
- **Devitri Buaton** (232410103026)
- **Moh Akbar Hidayatullah** (232410103034)
- **Eggy Tio Wandana** (232410103052)

---

## Ringkasan Proyek

Proyek ini melakukan komputasi parameter performa antrean menggunakan model **Multi Channel Single Phase (M/M/s)**. Data input dibagi menjadi 6 blok jam operasional (Jam A sampai F) untuk menangani sifat antrean perbankan yang dinamis.

### Alur Kerja Komputasi:

1. **Replikasi:** Menghitung ulang parameter performa menggunakan data laju kedatangan dan laju pelayanan dari dataset industri.
2. **Validasi Otomatis:** Membaca file data validasi untuk menghitung selisih (_error rate_) secara absolut antara hasil komputasi Python dengan hasil kalkulasi pada jurnal acuan.
3. **Optimasi Skenario:** Memprediksi penurunan performa antrean dengan mensimulasikan penambahan jumlah server dari 1 CS menjadi 2 CS aktif pada jam sibuk (09.00 - 11.00 WIB).

### Parameter Performa yang Dihitung:

- **Tingkat Utilisasi Kesibukan Server ($\rho$):**
  $$\rho = \frac{\lambda}{s \cdot \mu}$$
- **Probabilitas Sistem Kosong ($P_0$):**
  $$P_0 = \left[ \sum_{n=0}^{s-1} \frac{(\lambda/\mu)^n}{n!} + \frac{(\lambda/\mu)^s}{s! \left(1 - \frac{\lambda}{s\cdot\mu}\right)} \right]^{-1}$$
- **Rata-rata Jumlah Nasabah dalam Antrean ($L_q$):**
  $$L_q = \frac{P_0 \cdot (\lambda/\mu)^s \cdot \rho}{s! \cdot (1 - \rho)^2}$$
- **Rata-rata Waktu Tunggu dalam Antrean ($W_q$):**
  $$W_q = \frac{L_q}{\lambda}$$
- **Rata-rata Waktu Total dalam Sistem ($W_s$):**
  $$W_s = W_q + \frac{1}{\mu}$$

---

## Struktur Direktori

```text
├── TugasAkhirPemSim/ #ini virtual environment
├── data_antrean.csv
├── data_validasi.csv
├── cumi hitam pak kris.ipynb
├── requirements.txt
└── README.md
```

---

## Panduan Instalasi & Penggunaan

### 1. Kloning Repositori

```bash
git clone https://github.com/aldorifkifirmansyah/TugasAkhirPemSim.git
cd TugasAkhirPemSim
```

### 2. Membuat & Mengaktifkan Virtual Environment

- **Windows:**

```bash
  python -m venv TugasAkhirPemSim
  TugasAkhirPemSim\Scripts\activate
```

- **Linux/macOS:**

```bash
  python -m venv TugasAkhirPemSim
  source TugasAkhirPemSim/bin/activate
```

### 3. Install Dependensi

```bash
pip install -r requirements.txt
```

### 4. Menjalankan Notebook

```bash
jupyter notebook
```

Buka file `cumi hitam pak kris.ipynb` dan jalankan seluruh cell secara berurutan.

---

## Spesifikasi Berkas Data (CSV)

### 1. Data Input (`data_antrean.csv`)

Memuat variabel dasar struktural antrean per blok jam:

```csv
blok_jam,interval,lambda_arrival,mu_service,cs_count
A,08.00-09.00,3,7,1
B,09.00-10.00,5,8,1
C,10.00-11.00,5,8,1
```

### 2. Data Target Validasi (`data_validasi.csv`)

Memuat hasil kalkulasi asli dari jurnal acuan untuk menghitung nilai simpangan (_error_):

```csv
blok_jam,rho_jurnal,wq_jurnal,ws_jurnal
A,0.429,15.0,6.43
B,0.625,20.0,12.50
C,0.625,20.0,12.50
```

---

## Lisensi

Proyek ini dibuat murni untuk keperluan akademis di Lingkungan Fakultas Ilmu Komputer Universitas Jember.
