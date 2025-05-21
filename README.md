File Size Analyzer by Commit (Git & GitLab)
Script Python untuk menganalisis ukuran file per commit di repository Git (lokal) atau GitLab, dengan fitur validasi ukuran file sesuai best practice aplikasi Android.
Fitur Utama
Analisis file size per commit dari repository lokal (tanpa perlu akses API GitLab).
Dukungan filter tanggal: analisis commit dalam rentang tanggal tertentu.
Otomatis checkout branch sebelum analisis (--local-branch).
Validasi ukuran file berdasarkan kategori (ikon, gambar, audio, video, native libs, DEX, JSON, font, XML, dsb).
Report Excel lengkap:
Sheet 1: Info analisis (branch, tanggal mulai, tanggal akhir)
Sheet 2: Hasil analisis file (commit, file, size, validasi, dsb)
Sheet 3: Aturan validasi ukuran file
Highlight merah untuk file yang melebihi batas ukuran (OVERSIZE).
Progress bar saat proses analisis berjalan.
Aturan Validasi Ukuran File
| Kategori | Ekstensi/Format | Batas Maksimal (MB) | Catatan |
|---------------------------|-----------------|---------------------|--------------------------|
| Icon/Ilustrasi Sederhana | XML (Vector) | 0.02 | < 20 KB |
| Icon/Ilustrasi Sederhana | PNG/JPG | 0.05 | ≤ 50 KB |
| Gambar Konten | WebP | 0.2 | ≤ 200 KB |
| Gambar Fullscreen | WebP/JPG | 0.5 | ≤ 500 KB (1080x1920) |
| Audio Efek | OGG/AAC | 0.1 | < 100 KB (<5s) |
| Audio Musik Pendek | OGG/AAC | 0.3 | ≤ 300 KB |
| Video Pendek | MP4/MOV/M4V | 1 | < 1 MB (480p) |
| Lottie Animation | JSON | 0.2 | 50–200 KB |
| Native Library | .so | 5 | ≤ 5 MB per ABI |
| DEX/Kode | .dex | 10 | ≤ 10 MB per file |
| JSON/Data Bundling | .json | 0.1 | ≤ 100 KB |
| Font | .ttf/.otf | 0.5 | ≤ 500 KB |
| Resource XML | .xml | 0.02 | < 20 KB |
File yang melebihi batas di atas akan diberi label OVERSIZE dan cell-nya berwarna merah di report.
Cara Install
Clone repo ini
Buat virtual environment (opsional, tapi disarankan):
Apply to check_file_s...
activate
Install dependencies:
Apply to check_file_s...
txt
Cara Pakai (Analisis Lokal)
Apply to check_file_s...
xlsx
Penjelasan argumen:
--analyze-local-commits : Mode analisis commit lokal.
--local-path : Path ke repo git lokal (default: current directory).
--start-date / --end-date : Rentang tanggal commit (format YYYY-MM-DD).
--local-branch : (Opsional) Nama branch yang ingin di-checkout sebelum analisis.
--output-excel : Nama file hasil report Excel.
Contoh Output
Sheet 1: Info
Branch: nama branch yang dianalisis
Start Date: tanggal mulai analisis
End Date: tanggal akhir analisis
Sheet 2: File Report
Commit, Date, Commit Title, File, File Size (MB), NonStandard, Validation
Sheet 3: Validation Rules
Tabel aturan validasi ukuran file
Catatan
Pastikan repo lokal Anda tidak memiliki perubahan yang belum di-commit sebelum menjalankan analisis dengan --local-branch.
Script ini juga mendukung analisis via GitLab API (lihat argumen lain di script).
