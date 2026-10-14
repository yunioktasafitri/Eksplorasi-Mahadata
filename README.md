# Eksplorasi Mandiri Mahadata: REPLIKASI PARSIAL PERBANDINGAN KINERJA MONGODB DAN COUCHDB MENGGUNAKAN YCSB

Tugas individu mata kuliah Mahadata (IF25-40402), Institut Teknologi Sumatera.

- Nama: Yuni Okta Safitri
- NIM: 123140213
- Dosen: Meida Cahyo Untoro

## Tujuan

Mereplikasi sebagian eksperimen pada artikel berikut dalam skala kecil di Google Colab:

> Carvalho, I., Sá, F., & Bernardino, J. (2023). Performance evaluation of NoSQL document databases: Couchbase, CouchDB, and MongoDB. *Algorithms, 16*(2), Article 78. https://doi.org/10.3390/a16020078

Yang diuji adalah **MongoDB** dan **CouchDB** dengan 8 workload YCSB (A sampai H). Ukuran yang dicatat adalah runtime fase run. Couchbase tidak diuji.

| Parameter | Nilai |
|---|---|
| Jumlah rekaman | 10.000 (20 field x 500 byte) |
| Jumlah operasi | 10.000 per run |
| Jumlah thread | 1, 2, 4 |
| Ulangan | 3 per kombinasi |
| Total run | 72 per basis data |

Perbedaan dari artikel (skala data, jumlah thread, klien CouchDB, mesin) dijelaskan di laporan, Bagian B.4.

## Struktur folder

```
.
├── 123140213_YuniOktaSafitri_Eksplorasi_Mahadata.ipynb   # notebook Colab: pemasangan, eksekusi, analisis
├── hasil_mongodb.csv                                     # runtime mentah 72 run MongoDB
├── hasil_couchdb.csv                                     # runtime mentah 72 run CouchDB
├── tabel_rata_rata.csv                                   # rata-rata tiga ulangan per kombinasi
├── grafik_total.png                                      # total runtime per jumlah thread
├── grafik_per_workload.png                               # runtime per workload (skala log)
├── requirements.txt                                      # pustaka Python
└── README.md
```

## Lingkungan

Eksperimen dijalankan di Google Colab (versi gratis):

| Komponen | Versi |
|---|---|
| Prosesor | Intel Xeon 2,20 GHz, 2 core |
| Memori | 12 GiB |
| Sistem operasi | Ubuntu 24.04.5 LTS |
| Python | 3.13.16 |
| Java | OpenJDK 21.0.12.1 |
| YCSB | 0.17.0 |
| MongoDB | 6.0.16 |
| CouchDB | 3.5.3 |

Pustaka Python dicantumkan di `requirements.txt`. MongoDB, CouchDB, dan YCSB bukan paket Python, sehingga dipasang oleh sel-sel di notebook (lihat bagian berikut).

## Cara menjalankan

1. Buka notebook `123140213_YuniOktaSafitri_Eksplorasi_Mahadata.ipynb` di Google Colab (*File → Upload notebook*, atau buka langsung dari GitHub).
2. Pilih runtime Python 3 biasa (CPU).
3. Jalankan seluruh sel berurutan dengan *Runtime → Run all*. Sel-sel tersebut akan:
   - mencatat spesifikasi mesin;
   - mengunduh YCSB 0.17.0 dan memasang MongoDB 6.0.16;
   - membuat berkas workload G dan H;
   - menjalankan 72 run MongoDB dan menyimpan `hasil_mongodb.csv`;
   - memasang CouchDB 3.5.3 dan menjalankannya secara manual;
   - menjalankan 72 run CouchDB dengan skrip Python peniru YCSB dan menyimpan `hasil_couchdb.csv`;
   - menggabungkan hasil, lalu menghasilkan `tabel_rata_rata.csv`, `grafik_total.png`, dan `grafik_per_workload.png`.
4. Hasil tersimpan di folder `/content` pada Colab. Unduh sebelum sesi berakhir, karena berkas di folder tersebut bersifat sementara.

Perkiraan waktu: sekitar 11 menit untuk MongoDB dan sekitar 2 jam lebih untuk CouchDB. Bila sesi terputus, jalankan ulang sel yang sama. Kombinasi yang sudah tercatat di CSV akan dilewati.

Untuk membuat ulang tabel dan grafik tanpa menjalankan ulang eksperimen, unggah kedua berkas CSV hasil ke Colab, lalu jalankan hanya sel analisis (penggabungan dan pembuatan grafik).

## Data

Tidak ada dataset eksternal. Data dibangkitkan secara sintetis: YCSB membuat rekaman untuk MongoDB, dan skrip Python membuat dokumen dengan struktur yang sama (20 field x 500 karakter) untuk CouchDB. Seed acak dibuat tetap pada skrip CouchDB (sama dengan nomor ulangan).

## Sumber

- Artikel acuan: Carvalho et al. (2023), DOI di atas.
- YCSB: https://github.com/brianfrankcooper/YCSB
- Dokumentasi MongoDB: https://www.mongodb.com/docs/manual/
- Dokumentasi CouchDB: https://docs.couchdb.org
