# Pembagian Tugas - Clincoo

Diperbarui: 3 November 2026. Legenda status: `[x]` selesai, `[ ]` belum.

## P0 - Keamanan (aksi pemilik, tidak bisa dikerjakan dari kode)

- [ ] **Rotasi OpenRouter key** di https://openrouter.ai/keys (key lama `sk-or-v1-6b48...c54` pernah publik).
- [ ] **Rotasi E2B API key** di https://e2b.dev/dashboard (key lama `e2b_bb64...411` pernah publik).
- [ ] **Rotasi Jina AI key** di https://jina.ai (key lama `jina_63e2...4T` pernah publik).
- [ ] Opsional: bersihkan riwayat git (filter-repo / BFG + force push) supaya key lama benar-benar hilang dari history publik.

## P1 - Fungsional inti

- [x] Chat error 402 diperbaiki: model berbayar diganti rantai model gratis dengan fallback otomatis.
- [x] API key tidak lagi ditanam di kode; dipindah ke menu Pengaturan (localStorage).
- [x] Pesan error API yang jelas (401/402/429/404/jaringan) + tombol menuju Pengaturan.
- [x] Parser streaming tahan chunk terpotong + deteksi error di tengah stream.
- [x] Retry otomatis tanpa gambar bila model tidak mendukung vision.
- [x] Upload multi-file (hingga 20 file/pesan) + drag & drop + thumbnail + hapus per file.
- [x] Isi file disimpan di IndexedDB, jadi tidak lagi "hilang" karena kuota localStorage.
- [x] Judul sesi otomatis memakai rantai model yang sama (fallback ke potongan pesan).

## P2 - Keamanan aplikasi

- [x] Sanitasi HTML (DOMPurify) untuk semua output markdown dan pesan pengguna.
- [x] Escape judul sesi, nama lampiran, dan nama domain sumber.
- [x] Iframe preview HTML dipaksa `sandbox` dan tidak boleh membawa `src`/`srcdoc` dari markdown.
- [x] Konfirmasi sebelum menghapus percakapan.

## P3 - Navigasi & UI

- [x] 5 tautan mati (workspace/gambar/canvas/perpustakaan/aplikasi.html) dihapus dari sidebar.
- [x] Panel Workspace baru: menampilkan proyek yang dibuat lewat obrolan.
- [x] Panel Pengaturan baru (OpenRouter / E2B / Jina) + toast notifikasi.
- [x] Modal Pengaturan terbuka otomatis bila key belum diisi.
- [x] Popup opsi sesi tidak lagi keluar layar.

## P4 - Performa & ketahanan

- [x] Logo 3D: favicon diperbarui tiap 800ms (dari 150ms) dan berhenti saat tab tidak aktif.
- [x] Inisialisasi WebGL dibungkus try/catch: aplikasi tetap hidup walau CDN/WebGL gagal.
- [x] Semua `JSON.parse` localStorage dibungkus try/catch + toast saat penyimpanan penuh.
- [x] Render markdown saat mengetik di-throttle (~70ms) agar tidak membebani CPU.
- [x] Batas ukuran file (gambar 12 MB, dokumen 20 MB) dan teks dokumen dipotong 60k karakter.

## P5 - Belum dikerjakan (roadmap berikutnya)

- [ ] Halaman `gambar.html` (galeri hasil generate) bila fitur Gambar mau dihidupkan kembali.
- [ ] Halaman `canvas.html` sebagai editor/preview penuh.
- [ ] Halaman `perpustakaan.html` (arsip dokumen yang diunggah).
- [ ] Halaman `aplikasi.html` (daftar tool/integrasi).
- [ ] Proxy server (Cloudflare Worker) agar key pengguna tidak perlu disimpan di browser sama sekali.
- [ ] Tes otomatis (Playwright) di GitHub Actions untuk regresi UI.
- [ ] Dukungan `.docx` (ekstraksi teks) selain PDF/TXT/MD/CSV/JSON.

## Catatan teknis

- Semua pekerjaan P1-P4 sudah diterapkan di `index.html` pada commit terbaru dan diuji dengan Chrome headless: upload 12 file (20.5 MB) berhasil semua, tidak ada error konsol, gambar tetap tampil setelah reload (IndexedDB), XSS diblokir, dan obrolan mengembalikan jawaban normal.
