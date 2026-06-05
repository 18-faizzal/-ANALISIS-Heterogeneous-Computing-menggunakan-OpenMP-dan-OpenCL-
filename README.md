# ANALISIS Heterogeneous Computing menggunakan OpenMP dan OpenCL

![Banner](docs/diagram/jaya.png.png)


## 📌 Deskripsi Proyek

Proyek ini mengimplementasikan dan membandingkan performa algoritma General Matrix Multiplication (GEMM) menggunakan tiga pendekatan komputasi yang berbeda, yaitu Sequential Computing, OpenMP, dan OpenCL. Tujuan utama proyek adalah menganalisis pengaruh paralelisme CPU dan GPU terhadap waktu eksekusi operasi perkalian matriks berukuran besar.

Implementasi pertama menggunakan pendekatan sequential sebagai baseline pengukuran performa. Seluruh proses perhitungan dilakukan secara berurutan menggunakan satu thread CPU melalui algoritma perkalian matriks standar dengan tiga tingkat perulangan (triple nested loop).

Implementasi kedua memanfaatkan OpenMP untuk melakukan paralelisasi pada CPU multicore. Proses perhitungan elemen-elemen matriks hasil didistribusikan ke beberapa thread menggunakan directive `#pragma omp parallel for collapse(2)`, sehingga beberapa bagian pekerjaan dapat dieksekusi secara bersamaan dan waktu komputasi dapat dikurangi.

Implementasi ketiga menggunakan OpenCL untuk menjalankan komputasi pada GPU. Pada pendekatan ini, data matriks dikirim dari memori utama (RAM) ke memori GPU (VRAM), kemudian kernel OpenCL dijalankan secara paralel menggunakan ribuan work-item untuk menghitung elemen-elemen matriks hasil. Setelah proses komputasi selesai, hasil perhitungan dikembalikan ke memori utama untuk diverifikasi.

Selain membandingkan waktu eksekusi, proyek ini juga melakukan analisis terhadap speedup yang diperoleh dari pendekatan paralel serta mengevaluasi berbagai faktor yang mempengaruhi performa sistem, seperti overhead manajemen thread pada OpenMP dan overhead transfer data antara CPU dan GPU pada OpenCL.

Melalui proyek ini diharapkan dapat diperoleh pemahaman yang lebih mendalam mengenai konsep Heterogeneous Computing, perbedaan model paralelisme CPU dan GPU, serta efektivitas masing-masing pendekatan dalam menyelesaikan komputasi numerik berskala besar.


# 🏗️ Arsitektur Sistem

## Gambaran Umum

Sistem ini dirancang untuk melakukan analisis kinerja komputasi heterogen pada operasi **General Matrix Multiplication (GEMM)** dengan membandingkan tiga pendekatan komputasi yang berbeda, yaitu **Sequential Computing**, **OpenMP**, dan **OpenCL**. Ketiga metode menerima input matriks yang sama dan menghasilkan output matriks yang identik sehingga perbandingan performa dapat dilakukan secara objektif.

Tujuan utama arsitektur ini adalah mengevaluasi efektivitas paralelisme CPU dan GPU dalam mempercepat proses komputasi matriks berukuran besar melalui pengukuran waktu eksekusi, speedup, dan efisiensi sistem.

### Alur Pemrosesan Sistem

```text
Input Matrix A & B
        │
        ▼
 Matrix Multiplication
        │
 ┌──────┼──────┐
 │      │      │
 ▼      ▼      ▼
Sequential  OpenMP  OpenCL
 (CPU)      (CPU)   (GPU)
 │           │       │
 └──────┬────┴───────┘
        ▼
 Performance Analysis
        │
        ▼
 Benchmark Results

