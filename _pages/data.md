---
layout: single
title: "Data"
permalink: /data/
author_profile: true
---

## Templat Data Fasilitas Ketenagalistrikan 2015 sampai 2025

*Data request template: electricity generation and grid facilities in Indonesia, 2015 to 2025.*

Templat ini membantu pengisian data fasilitas pembangkit dan jaringan ketenagalistrikan untuk penelitian akademik yang menghasilkan rekomendasi kebijakan. Templat hanya alat bantu. Apabila data sudah tersimpan dalam format lain, mohon dikirim apa adanya dan peneliti yang akan menyesuaikannya.

**[Unduh templat Excel (.xlsx)]({{ '/files/Templat-Data-Ketenagalistrikan-2015-2025.xlsx' | relative_url }})**

### Cara pengisian

1. Unduh templat, lalu isi secara *offline* di Excel.
2. Isi sel berwarna hijau muda mulai baris ke-5. Baris abu-abu (baris ke-4) hanyalah contoh fiktif dan mohon dihapus atau ditimpa.
3. Kirim file yang sudah diisi ke [ariyo.irhamna@indef.or.id](mailto:ariyo.irhamna@indef.or.id).

### Isi templat

| No | Lembar | Isi | Prioritas |
|---|---|---|---|
| 1 | `Petunjuk` dan `Kamus_Variabel` | Petunjuk pengisian dan penjelasan setiap kolom | Bacaan |
| 2 | `Pembangkit` | Satu baris per lokasi pembangkit | Utama |
| 3 | `Unit_Pembangkit` | Satu baris per unit, termasuk tanggal konstruksi, tersambung ke jaringan, *commissioning*, dan operasi komersial | Utama |
| 4 | `Produksi_Bulanan` | Satu baris per unit per bulan, Januari 2015 sampai Desember 2025 | Utama |
| 5 | `Gardu_Induk` | Satu baris per gardu induk | Kedua |
| 6 | `Riwayat_Kapasitas_Gardu` | Satu baris per perubahan kapasitas gardu setelah beroperasi | Kedua |
| 7 | `Jaringan_Transmisi` | Satu baris per ruas transmisi | Kedua |

### Catatan penting

- **Tingkat lokasi.** Mohon koordinat (*latitude* dan *longitude*, desimal WGS84). Untuk pembangkit, desa/kelurahan dan kecamatan juga wajib diisi. Untuk gardu induk dan transmisi, jika koordinat tidak ada, isi desa/kelurahan atau minimal kecamatan. Nama kabupaten/kota dan provinsi selalu diisi.
- **Tanggal.** Format YYYY-MM-DD. Untuk riwayat kapasitas gardu, jika tanggal pasti tidak ada, mohon minimal minggu, bulan, dan tahunnya (isi hari Senin pada minggu itu).
- **COD** adalah *commercial operation date*, yaitu tanggal unit resmi beroperasi secara komersial.
- **Data tidak tersedia.** Kosongkan sel. Jangan isi 0, karena 0 berarti nilai nol sungguhan.
