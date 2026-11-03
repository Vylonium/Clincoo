# Clincoo

Aplikasi obrolan AI satu-file (`index.html`) yang berjalan langsung di browser. Tidak ada server, tidak ada build step. Cocok di-hosting di GitHub Pages.

- Live: https://vylonium.github.io/Clincoo/
- Repo: https://github.com/Vylonium/Clincoo

## Fitur

- Obrolan AI streaming lewat OpenRouter (rantai model gratis + fallback otomatis).
- **Lampiran multi-file** (gambar + dokumen) sekaligus, hingga 20 file per pesan, total puluhan MB, tanpa error kuota.
- Gambar di-downscale otomatis (maks 1400px, JPEG 82%) sebelum dikirim ke model.
- Isi file disimpan di **IndexedDB**, bukan localStorage, jadi riwayat obrolan tetap ringan.
- Blok kode interaktif: jalankan kode (E2B, fallback Piston), preview HTML (iframe sandbox), salin, unduh.
- Markdown aman: semua HTML dari model disanitasi dengan DOMPurify.
- Panel Workspace untuk melihat proyek yang dibuat lewat obrolan.

## Pengaturan API (wajib sekali)

Kunci API **tidak lagi ditanam di kode**. Buka ikon gear di kanan atas (atau menu Pengaturan) lalu isi:

| Key | Wajib | Fungsi |
| --- | --- | --- |
| OpenRouter | Ya | Menjalankan obrolan. Buat di https://openrouter.ai/keys |
| E2B | Tidak | Eksekusi kode di sandbox. Tanpa ini dipakai Piston. |
| Jina AI | Tidak | Baca URL dan pencarian web real-time. |

Key hanya disimpan di `localStorage` perangkat pengguna dan hanya dikirim ke penyedia terkait.

## Struktur

- `index.html` - seluruh aplikasi (UI, state, API, penyimpanan).
- `TASKS.md` - pembagian tugas dan status pekerjaan.

## Riwayat keamanan (penting)

Versi lama repo ini memuat tiga API key dalam kode sumber publik (OpenRouter, E2B, Jina). Key tersebut sudah **dihapus dari kode**, tetapi masih ada di riwayat git. Pemilik repo wajib merotasi/menghapus ketiga key itu di dashboard masing-masing penyedia. Lihat `TASKS.md` bagian P0.

## Menjalankan lokal

```bash
python3 -m http.server 8899
# buka http://localhost:8899/index.html
```
