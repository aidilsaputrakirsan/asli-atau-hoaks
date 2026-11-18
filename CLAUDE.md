# Asli atau Rekayasa? — Slide materi verifikasi foto/video untuk kepolisian (Slidev)

Presentasi Aidil Saputra Kirsan. Audiens: kepolisian. Fokus: cara membedakan foto/video asli vs
hoaks/rekayasa (termasuk deepfake) dan **perbandingan cara memeriksa**.
Jawab dalam Bahasa Indonesia, santai tapi jelas.

**Status: DRAF untuk diskusi dengan panitia.** Acara, tanggal, durasi, profil peserta, dan format belum
ada. Placeholder `[Nama acara] · [Satuan/Polda] · [Tanggal]` di sampul. Pertanyaan untuk panitia
dan usulan alur ada di `BAHAN-DISKUSI.md`.

## Benang merah
> Membuat konten palsu sudah murah. Yang mahal adalah kebiasaan memeriksa sebelum percaya.
> Pertanyaannya bukan "AI atau bukan?", tapi "apakah konten ini benar menunjukkan apa yang diklaim?"

Alur: kuis asli/AI → data (manusia ±48%) → kasus deepfake Presiden (Bareskrim 2025) → 4 tingkat rekayasa
→ pertanyaan inti → **tabel perbandingan 4 cara** (mata, asal-usul file, alat deteksi, konteks/OSINT)
→ satu slide per cara → alur 5 langkah → 5 tingkat keyakinan → liar's dividend → hukum & pembuktian
→ praktik (opsional) → rekomendasi → penutup.

## Jalankan
```bash
npm install            # node_modules disalin dari simfoni-itk-2026, biasanya tidak perlu
npm run dev            # http://localhost:3030 · presenter: /presenter
npm run build
npm run export         # PDF
```
Node 22 lewat mise (`.nvmrc`). Slidev v53. Deploy GitHub Pages lewat `.github/workflows/deploy.yml`
(base otomatis dari nama repo). Repo publik/privat BELUM diputuskan. User commit & push sendiri.

## Tema: TERANG (beda dari SIMFONI yang gelap)
Token di `:root` `styles/index.css`: latar `#f6f7f9` (+ kisi titik samar dari `global-bottom.vue`),
teks `#10131a`, redup `#4a5160`, garis `#e1e4ea`, biru `#1f62d6` (bagian kunci judul),
aksen teal `#0b7a6e` (asli/terverifikasi/nomor), merah `#c0392b` (rekayasa), kuning `#a86b00` (ragu).
Label `.status.asli|palsu|ragu` selalu berisi TEKS (aman untuk buta warna).
Plus Jakarta Sans + JetBrains Mono. Aturan gaya sama dengan SIMFONI: judul = kalimat pernyataan dua warna,
tanpa emoji/gradien/bayangan tebal/label kapital di atas judul, `v-mark` maks 1 per slide (warna `#0b7a6e`),
hindari grid 3 kartu bernomor, setiap angka luar wajib `.sumber`. Slide `class: malam` = latar sedikit lebih tegas.

## Komponen
| File | Isi |
|---|---|
| `components/Kuis.vue` | 4 gambar A–D, jawaban muncul `:buka="$clicks >= 1"`; gambar kosong → bingkai petunjuk |
| `components/Tangkapan.vue`, `Foto.vue`, `AngkaNaik.vue` | dari SIMFONI, warna disesuaikan ke tema terang |
| `global-top.vue` | header "Asli atau rekayasa?" + `bagian`, nomor halaman |
| `global-bottom.vue` | latar terang + kisi titik (statis) |

## Data & sumber (jangan mengarang angka baru)
| Angka | Sumber | Catatan |
|---|---|---|
| Akurasi manusia 48% (wajah asli vs AI), 59% setelah latihan, wajah AI dinilai lebih dipercaya | Nightingale & Farid, PNAS 119(8), 2022 | 315 peserta |
| 0,1% bisa membedakan semua; >60% yakin | iProov, Feb 2025, 2.000 responden UK/AS | studi vendor |
| Deepfake Presiden: penangkapan Jan–Feb 2025, satu pelaku ±100 korban ±Rp65 jt, forensik: palsu | Bisnis.com 7 Feb 2025; detik.com | liputan media, cek ke rilis Polri |
| Kerugian penipuan berbasis AI Rp700 miliar | Komdigi via Bisnis.com 23 Okt 2025 | cek ulang |
| Liar's dividend | Chesney & Citron, California Law Review 107 (2019) | |
| UU ITE Ps. 5, 28(3), 35; KUHP UU 1/2023 berlaku 2 Jan 2026 | teks UU | verifikasi di JDIH |

## Belum selesai (TODO)
- Semua info acara (lihat `BAHAN-DISKUSI.md`).
- `public/kuis/a–d.jpg` (2 asli bebas lisensi + 2 buatan AI sendiri), `public/praktik/kasus-1..3.jpg`.
- Rekaman demo (Google Lens, InVID-WeVerify, EXIF, WA biasa vs dokumen).
- Lembar verifikasi + Google Form.

## Privasi
Jangan pakai wajah tokoh nyata/anggota Polri untuk contoh buatan AI, jangan memuat data korban/kasus
yang belum dirilis resmi. Kalau repo publik: anggap semua isi bisa dibaca siapa saja.
