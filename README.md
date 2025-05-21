Tentu! Berikut dokumentasi penggunaan masing-masing fitur script Anda, siap untuk dimasukkan ke README GitHub:

---

# 📦 File Size Analyzer (Android Project & APK/AAB)

Script Python untuk menganalisis ukuran file di project Android (repo lokal) dan APK/AAB hasil build, lengkap dengan validasi, rekomendasi optimasi, dan berbagai mode audit.

---

## 🚀 Fitur Utama

- **Audit snapshot HEAD**: Analisis file di project yang berpotensi masuk ke APK/AAB.
- **Audit per-commit**: Analisis file yang berubah di setiap commit (dengan rentang tanggal).
- **Audit seluruh commit history**: Analisis semua file yang pernah ada/berubah di seluruh commit.
- **Audit APK/AAB**: Analisis isi APK/AAB hasil build, termasuk mapping ke file sumber project.
- **Validasi ukuran file**: Berdasarkan best practice Android (gambar, audio, font, native lib, dsb).
- **Rekomendasi optimasi**: Saran otomatis untuk file yang oversize.
- **Progress bar**: Untuk semua proses analisis.
- **Report Excel**: Multi-sheet, mudah dibaca dan didokumentasikan.

---

## 🛠️ Cara Install

1. **Clone repo ini**
2. **Buat virtual environment (opsional):**
   ```sh
   python3 -m venv venv
   source venv/bin/activate
   ```
3. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```

---

## 📋 Cara Penggunaan

### 1. **Audit Snapshot HEAD (Project Lokal)**
Analisis file di project yang relevan untuk APK/AAB (hanya folder dan ekstensi yang umum di-package).

```sh
python check_file_size_by_commit.py --analyze-local-snapshot --local-path /path/to/your/project --output-excel hasil_snapshot.xlsx
```

#### **Filter Tipe File (Opsional)**
Hanya proses file tertentu (misal hanya gambar):
```sh
python check_file_size_by_commit.py --analyze-local-snapshot --local-path /path/to/your/project --snapshot-file-types png,jpg,webp --output-excel hasil_snapshot_gambar.xlsx
```

---

### 2. **Audit Per-Commit (Rentang Tanggal)**
Analisis file yang berubah di setiap commit dalam rentang tanggal tertentu.

```sh
python check_file_size_by_commit.py --analyze-local-commits --local-path /path/to/your/project --start-date 2024-05-01 --end-date 2024-06-01 --output-excel hasil_commit_range.xlsx
```

---

### 3. **Audit Seluruh Commit History**
Analisis semua file yang pernah ada/berubah di seluruh commit (bukan hanya linear).

```sh
python check_file_size_by_commit.py --analyze-local-all-commits --local-path /path/to/your/project --output-excel hasil_all_commits.xlsx
```

---

### 4. **Audit APK/AAB Hasil Build**
Analisis isi APK/AAB, size file, saran optimasi, dan mapping ke file sumber project.

```sh
python check_file_size_by_commit.py --analyze-apk --apk-path /path/to/app-release.apk --local-path /path/to/your/project --output-excel hasil_apk_audit.xlsx
```

---

## 📑 Hasil Report Excel

- **Info**: Ringkasan analisis (mode, branch, tanggal, dsb)
- **Snapshot HEAD**: File di project yang relevan untuk APK/AAB
- **Optimization Candidates**: File oversize yang bisa dioptimasi (dengan saran)
- **File Report**: Detail file per commit (untuk mode commit)
- **Grouped Files**: Rekap file unik (untuk mode commit)
- **All Commits**: Semua file yang pernah ada/berubah di seluruh commit
- **APK_AAB_Content**: Isi file di APK/AAB hasil build
- **APK_to_Project_Mapping**: Mapping file di APK/AAB ke file sumber project (by basename)
- **Validation Rules**: Aturan validasi ukuran file

---

## 📝 Contoh Argumen Lain

- `--snapshot-file-types png,jpg,webp`  
  Filter file di snapshot HEAD hanya untuk tipe tertentu.
- `--start-date 2024-05-01 --end-date 2024-06-01`  
  Filter commit berdasarkan tanggal.

---

## ⚠️ Catatan

- Untuk audit APK/AAB, mapping ke file sumber project berbasis nama file (tidak selalu 100% akurat).
- Hanya folder dan file yang relevan untuk APK/AAB yang diproses di mode snapshot HEAD.
- Sheet “Optimization Candidates” hanya muncul jika ada file oversize yang bisa dioptimasi.

---

## 💡 Saran Penggunaan

- **Audit awal:** Gunakan snapshot HEAD untuk menemukan file besar di project.
- **Audit release:** Gunakan audit APK/AAB untuk tahu file yang benar-benar masuk ke APK/AAB.
- **Audit history:** Gunakan mode commit/all-commits untuk investigasi file besar sepanjang sejarah repo.

---
