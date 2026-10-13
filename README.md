# Replikasi Parsial: Evaluasi Kinerja NoSQL Document Database (MongoDB dan CouchDB)

Tugas Eksplorasi Mandiri Mahadata (IF25-40402)

Nama: Yuni Okta Safitri  
NIM: 123140213

## Artikel acuan
Carvalho, I., Sá, F., & Bernardino, J. (2023). Performance evaluation of NoSQL document databases:
Couchbase, CouchDB, and MongoDB. *Algorithms, 16*(2), 78. https://doi.org/10.3390/a16020078

## Tujuan
Mengulang sebagian eksperimen artikel: mengukur runtime delapan workload (A sampai H) pada MongoDB
dan CouchDB dengan variasi jumlah thread, pada skala data yang diperkecil, lalu membandingkan
polanya dengan artikel.

## Cakupan replikasi (replikasi parsial)
| Aspek | Artikel | Eksperimen ini |
|---|---|---|
| Lingkungan | Laptop Windows 10 | Google Colab |
| Jumlah record | 100 ribu, 1 juta, 10 juta | 10.000 |
| Jumlah thread | 1, 3, 6 | 1, 2, 4 |
| Ulangan | 3, dirata-rata | 3, dirata-rata |
| Database | Couchbase, CouchDB, MongoDB | MongoDB, CouchDB |
| Alat ukur | YCSB | MongoDB: YCSB, CouchDB: skrip Python yang meniru YCSB |

Alasan perbedaan:
- **Jumlah record (10.000):** artikel memakai hingga 10 juta record (sekitar 95 GB data) dan
  total waktu eksekusinya sekitar 20 hari komputasi. Hal itu tidak mungkin ditiru dalam waktu
  pengerjaan tugas dan batas sumber daya Google Colab.
- **Jumlah thread (1, 2, 4):** disesuaikan dengan jumlah core CPU yang tersedia di Colab
  ([isi jumlah core Anda]), sedangkan artikel memakai laptop dengan 6 core.
- **CouchDB:** YCSB tidak menyediakan konektor CouchDB, sehingga CouchDB diukur dengan skrip
  Python yang meniru workload YCSB (proporsi operasi dan distribusi kunci dibaca dari file
  workload yang sama).
- **Lingkungan (Colab):** dipilih karena [alasan Anda, misalnya tidak perlu memasang Docker
  di laptop / laptop tidak cukup kuat].
- **Couchbase tidak diuji:** [alasan Anda, misalnya waktu terbatas dan konektor YCSB yang
  memakai SDK lama].

## Struktur repositori
- `[nama-notebook].ipynb` : notebook eksperimen
- `results/hasil_mongodb.csv`, `results/hasil_couchdb.csv` : hasil mentah tiap ulangan
- `results/tabel_rata_rata.csv` : rata-rata runtime per workload dan thread
- `results/grafik_total.png`, `results/grafik_per_workload.png` : grafik

## Lingkungan dan versi
[Python, MongoDB, CouchDB, YCSB, Java, OS Colab; isi sesuai yang benar-benar terpasang]

## Cara menjalankan
1. Buka notebook di Google Colab.
2. Jalankan sel secara berurutan: pasang database, definisikan fungsi pengukur, jalankan loop, lalu analisis.
3. Hasil mentah tersimpan di CSV; sel analisis menghasilkan tabel dan grafik.

## Catatan dan keterbatasan
- Skrip pengukur CouchDB bukan YCSB asli; klien Python dan klien MongoDB (Java) berbeda,
  jadi perbandingan nilai absolut tidak sepenuhnya adil.
- Update di CouchDB butuh dua permintaan (baca revisi, lalu tulis), di MongoDB satu.
- Database dan klien berjalan di mesin Colab yang sama.

## Sumber dan atribusi
- YCSB: https://github.com/brianfrankcooper/YCSB
- Data dan kode penulis artikel: https://github.com/isofiaC/Performance-Evaluation-of-NoSQL-Document-Databases
