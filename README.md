# Image as Data: Pixel & Metadata Inspector

Notebook Python untuk mempelajari bagaimana gambar digital direpresentasikan sebagai kumpulan angka (piksel). Notebook juga memuat bagian analisis informasi file, warna, metadata EXIF/GPS, indikator metadata tambahan, serta ekspor laporan JSON dan CSV.

> **Status sumber:** file notebook yang disertakan masih membutuhkan beberapa definisi helper sebelum seluruh alur analisis dapat dijalankan dari kernel yang bersih. Daftar fungsi/variabel yang belum didefinisikan dijelaskan pada bagian **Catatan kompatibilitas notebook** di bawah.

## Fitur yang dituju

- Menampilkan gambar dan ukuran file.
- Membaca dimensi array NumPy serta menampilkan contoh nilai piksel.
- Mengubah sebagian nilai piksel pada salinan array untuk menunjukkan bahwa perubahan angka mengubah tampilan gambar. File gambar asli tidak ditimpa oleh demonstrasi ini.
- Menampilkan informasi file seperti format, resolusi, ukuran, waktu sistem berkas, hash MD5/SHA-256, dan magic bytes.
- Menganalisis statistik channel RGB, histogram, dan perkiraan warna dominan.
- Mengekstrak metadata EXIF, termasuk informasi kamera, waktu pengambilan, pengaturan kamera, dan GPS jika tersedia.
- Membuat tautan Google Maps dari koordinat GPS jika koordinat ditemukan.
- Memeriksa indikator metadata tambahan seperti ICC, XMP, software, dan data setelah penanda akhir file.
- Menyimpan laporan satu gambar ke JSON dan merangkum analisis satu folder ke CSV.
- Menyediakan rancangan reverse geocoding opsional. Koordinat lokasi bersifat sensitif; jangan aktifkan pengiriman koordinat ke layanan pihak ketiga tanpa mempertimbangkan privasi.

## Struktur proyek

```text
image-metadata-github/
├── analisis_gambar_metadata.ipynb
├── README.md
└── .gitignore
```

## Kebutuhan

Gunakan Python 3.9 atau lebih baru. Dependensi yang digunakan atau diperlukan oleh bagian-bagian notebook meliputi:

- JupyterLab / Jupyter Notebook
- NumPy
- Pillow
- Matplotlib
- pandas
- IPython
- geopy (untuk reverse geocoding jika helper tersebut diterapkan dan diaktifkan)

Pasang dependensi dengan perintah:

```bash
python -m pip install jupyterlab numpy Pillow matplotlib pandas ipython geopy
```

## Cara menjalankan

1. Buka terminal pada folder proyek.
2. Jalankan JupyterLab:

   ```bash
   jupyter lab
   ```

3. Buka `analisis_gambar_metadata.ipynb`.
4. Pada sel konfigurasi awal, sesuaikan lokasi gambar:

   ```python
   IMAGE_PATH = 'Gambar.jpeg'
   ```

5. Letakkan gambar tersebut di folder proyek atau gunakan path lengkap/menuju lokasi file yang sesuai.
6. Jalankan sel dari atas ke bawah. Untuk analisis folder, notebook menggunakan folder `gambar` sebagai nilai awal `FOLDER_PATH`; sesuaikan ke folder berisi gambar yang ingin dianalisis.
7. Bagian penyimpanan laporan menggunakan folder `output` sebagai lokasi keluaran.

## Catatan kompatibilitas notebook

Dalam notebook yang disertakan, bagian analisis lanjutan memanggil beberapa nama yang belum memiliki definisi pada source cell yang tersedia, antara lain:

- Fungsi helper: `get_file_info`, `extract_exif`, `detect_extra_metadata`, `load_rgb_array`, `channel_statistics`, `dominant_colors`, `reverse_geocode_coordinates`, dan `plot_rgb_histograms`.
- Konfigurasi/alias: `ENABLE_REVERSE_GEOCODING`, `ANALYZE_SUBFOLDERS`, `SUPPORTED_EXTENSIONS`, serta alias pandas `pd`.

Akibatnya, demonstrasi awal pembacaan gambar dan perubahan nilai piksel dapat digunakan setelah `IMAGE_PATH` diarahkan ke gambar yang ada, tetapi alur metadata/EXIF/GPS, histogram, JSON, dan CSV secara penuh belum dapat dijalankan dari kernel bersih sampai definisi helper dan konfigurasi yang hilang ditambahkan atau dipulihkan. README ini mendokumentasikan isi notebook yang diberikan dan tidak menganggap fungsi yang belum ada telah berjalan.

## Privasi dan interpretasi hasil

- Metadata EXIF tidak selalu tersedia. Banyak aplikasi menghapus metadata ketika gambar diedit atau diunggah.
- Koordinat GPS dapat mengungkap lokasi pribadi. Periksa laporan JSON/CSV sebelum membagikannya.
- Reverse geocoding, bila diimplementasikan dan diaktifkan, dapat mengirim koordinat ke layanan pihak ketiga.
- Hash MD5 dan SHA-256 dihitung dari byte file. MD5 disertakan untuk identifikasi/checksum lama, bukan untuk keamanan kriptografis; gunakan SHA-256 untuk checksum modern.
- Magic bytes dan indikator data tambahan bukan pemeriksaan keamanan menyeluruh. Data tambahan di akhir file tidak otomatis berarti file berbahaya.
- Warna dominan adalah perkiraan warna, bukan pengenalan objek atau makna gambar.

## GitHub

Sebelum melakukan commit, pastikan gambar pribadi, keluaran analisis, dan laporan metadata tidak ikut diunggah. Aturan `.gitignore` di proyek ini mengabaikan folder input/output yang umum dipakai serta file laporan hasil analisis.
