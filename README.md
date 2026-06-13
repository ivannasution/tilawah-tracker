# 🌙 Tilawah Tracker

> **تِلَاوَة** — Aplikasi pelacak tilawah Al-Qur'an harian, dari cover ke cover.

Dibuat untuk rutinitas Fajr, 2–4 halaman per hari.

🔗 **Live app:** [ivannasution.github.io/tilawah-tracker](https://ivannasution.github.io/tilawah-tracker/)

---

## Fitur

### 📖 Log Sesi
- Pilih waktu shalat (Fajr / Dzuhur / Asr / Maghrib / Isya / Other)
- Tanggal bisa diubah untuk log retrospektif
- Input surah awal + ayah awal, surah akhir + ayah akhir
- Mendukung **cross-surah** (baca lebih dari satu surah dalam satu sesi)
- Kalkulasi halaman otomatis berdasarkan tabel batas halaman Mushaf Utsmani
- Override halaman manual jika diperlukan
- Kolom catatan opsional

### 👥 Multi-Profil
- Buat beberapa profil (misalnya untuk diri sendiri dan pasangan)
- Switch antar profil kapan saja
- Setiap profil menyimpan riwayat, statistik, dan progress khatam masing-masing
- **Starting position** — saat membuat profil, bisa langsung set posisi baca saat ini sehingga Juz 1–N langsung tertandai selesai dengan benar

### 📊 Statistik
- Rata-rata halaman per hari
- Jumlah sesi dan hari yang dicatat
- Streak harian 🔥
- Grafik batang 14 hari terakhir
- 4 skenario prediksi khatam (pace saat ini, 2 pg/hari, 3 pg/hari, 4 pg/hari)

### 🗓️ Grid Juz
- 30 kotak Juz dengan batas halaman nyata (bukan pembagian /20)
- Hijau = selesai, Pink = sedang dibaca, Kosong = belum

### 🏆 Khatam Tracking
- Otomatis terdeteksi saat halaman 604 tercapai
- Modal perayaan dengan hitungan khatam dan tanggal
- Riwayat semua khatam tersimpan

### 📋 Riwayat & Edit
- Semua sesi tersimpan dengan detail lengkap
- Edit sesi yang sudah dilog (surah, ayah, halaman, tanggal, catatan)
- Hapus sesi individual
- Clear log dengan konfirmasi ganda

### 🔗 Google Sheets Sync
- Sync otomatis setiap kali simpan, edit, atau hapus sesi
- Full sync on connect
- Dua sheet: **Log** (detail sesi) dan **Stats** (ringkasan per profil)
- Tombol "Open Sheet" untuk buka spreadsheet langsung

---

## Cara Pakai

**Langsung pakai** — buka link di atas dari HP, lalu "Add to Home Screen" untuk install sebagai app.

Tidak perlu daftar akun. Semua data tersimpan di perangkat (localStorage).

---

## Setup Google Sheets Sync (Opsional)

Untuk sync data ke Google Sheets agar bisa diakses dari mana saja:

### 1. Buat Google Sheet baru
Buka [Google Sheets](https://sheets.google.com) → buat spreadsheet baru → beri nama misalnya "Quran Tilawah Tracker".

### 2. Buat Apps Script
Di Google Sheet → **Extensions → Apps Script** → hapus semua kode yang ada → paste kode dari file [`tilawah-apps-script.js`](tilawah-apps-script.js) → Save.

### 3. Deploy sebagai Web App
Di Apps Script → **Deploy → New deployment** → pilih tipe **Web app** → atur:
- Execute as: **Me**
- Who has access: **Anyone**

Klik Deploy → copy URL yang muncul (bentuknya `https://script.google.com/macros/s/.../exec`).

### 4. Hubungkan di app
Buka app → tab **Stats** → tempel URL Apps Script di kolom "Apps Script Web App URL" → klik **Connect**.

Tempel juga URL Google Sheet di kolom "Google Sheet URL" → klik **Save** (untuk tombol Open Sheet).

### Kolom Log Sheet (A–N)
`id · date · prayer · profile · startSurahN · startSurahName · fromAyah · endSurahN · endSurahName · toAyah · startPage · endPage · pages · notes`

### Kolom Stats Sheet (A–I)
`profile · totalPages · pagesLeft · percent · avgPagesPerDay · sessions · daysLogged · prayerBreakdown · lastSync`

---

## Catatan Teknis

- **Single-file PWA** — seluruh app dalam satu file `index.html`, tidak ada dependency eksternal selain Google Fonts
- **Data storage** — localStorage browser; setiap perangkat menyimpan datanya sendiri
- **Multi-device** — Google Sheets berfungsi sebagai sumber kebenaran bersama; fitur "pull from GSheet" direncanakan untuk versi berikutnya
- **Timezone** — menggunakan local timezone (bukan UTC) sehingga tanggal selalu benar di zona waktu pengguna
- **Halaman Mushaf** — menggunakan tabel batas halaman Mushaf Utsmani standar 604 halaman (Madinah)

---

## Changelog

| Versi | Tanggal | Perubahan |
|-------|---------|-----------|
| v1.4.3 | 2026-06-13 | Fix stats GSheet: totalPages dan pagesLeft kini pakai posisi nyata dari app (termasuk starting position), bukan hanya jumlah halaman dari sesi log |
| v1.4.2 | 2026-06-13 | Fix Juz grid: totalPg kini dihitung dari end page aktual sesi, bukan akumulasi — profil tanpa starting position kini menampilkan Juz yang benar |
| v1.4.1 | 2026-06-13 | Fix openGs() tidak lagi pakai browser prompt; fix confirmClear() reset ke starting position awal profil; version string dari konstanta |
| v1.4.0 | 2026-06-13 | GSheet sync untuk save/edit/delete; fallback text matching untuk surah search di setup |
| v1.3.x | — | Edit log modal; delete per entry; prayer time chips |
| v1.2.x | — | Khatam detection & celebration modal; khatam count |
| v1.1.x | — | Multi-profile; starting position; cross-surah logging |
| v1.0.0 | — | Rilis pertama |

---

## Rencana Berikutnya

- [ ] PWA manifest + service worker (offline install yang sesungguhnya)
- [ ] Pull from GSheet (sync dua arah untuk multi-device)
- [ ] Notifikasi pengingat harian

---

*Semoga Allah menerima tilawah kita. آمين*
