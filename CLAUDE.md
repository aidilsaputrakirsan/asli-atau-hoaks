# Asli atau Rekayasa? — Slide materi verifikasi foto/video untuk kepolisian (Slidev)

Presentasi Aidil Saputra Kirsan. Audiens: kepolisian. Fokus: cara membedakan foto/video asli vs
hoaks/rekayasa (termasuk deepfake) dan **perbandingan cara memeriksa**.
Jawab dalam Bahasa Indonesia, santai tapi jelas.

**Status: DRAF untuk diskusi dengan panitia.** Peserta: perwakilan Polres se-Kaltim, maks. 150 orang
(latihan dimainkan per tim Polres). Acara, tanggal, durasi, dan format belum ada. Placeholder `[Nama acara] · [Satuan/Polda] · [Tanggal]` di sampul. Pertanyaan untuk panitia
dan usulan alur ada di `BAHAN-DISKUSI.md`.

## Benang merah
> Membuat konten palsu sudah murah. Yang mahal adalah kebiasaan memeriksa sebelum percaya.
> Pertanyaannya bukan "AI atau bukan?", tapi "apakah konten ini benar menunjukkan apa yang diklaim?"

Alur: kuis asli/AI → data (manusia ±48%) → kasus deepfake Presiden (Bareskrim 2025) → 4 tingkat rekayasa → video bodycam palsu (Sora)
→ pertanyaan inti → **tabel perbandingan 4 cara** (mata, asal-usul file, alat deteksi, konteks/OSINT)
→ satu slide per cara → alur 5 langkah → 5 tingkat keyakinan → **latihan antar-Polres 7 ronde** (kartu
hijau/kuning/merah; ronde 7 = suara asli vs klon ElevenLabs suara Aidil sendiri) → liar's dividend → hukum & pembuktian
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

## Desain: konsep SIMFONI, versi TERANG (penting)
User menolak tampilan "AI template". Ikuti konsep repo simfoni-itk-2026: setiap ide inti = diagram yang
bercerita per klik (jalur, gerbang, skala, alur), BUKAN tabel, badge/pil status, kotak-kotak, grid kartu,
atau daftar bullet panjang. Label = mono huruf kecil (`.label-kolom`), bukan kapital. Statement slide =
`layout: center` + `class: malam`. Latar = jaringan titik bergerak (global-bottom.vue, port SIMFONI).
Token `:root` styles/index.css: latar `#f6f7f9`, teks `#10131a`, redup `#4a5160`, garis `#e1e4ea`,
biru `#1f62d6` (bagian kunci judul), teal `#0b7a6e` (asli), merah `#c0392b` (rekayasa), kuning `#a86b00` (belum pasti).
Judul = kalimat pernyataan dua warna; `v-mark` maks 1/slide (warna `#0b7a6e`); setiap angka luar wajib `.sumber`.
Komponen klik memakai `useSlideContext().$clicks` + frontmatter `clicks: N`; elemen tambahan pakai `v-click="N"` absolut.
Mode ekspor (`isPrintMode`) selalu menampilkan keadaan akhir / daftar ringkas.

## Komponen
| File | Slide | Isi |
|---|---|---|
| `SampulAlur.vue` | 1 | partikel: konten beredar → diperiksa → asli / belum pasti / rekayasa (SMIL) |
| `Kuis.vue` | 3 | 4 gambar A–D, jawaban = garis warna + label mono |
| `SkalaTebak.vue` | 4 | skala 0–100% + "lempar koin"; 48% → 59% → iProov 0,1% (`clicks: 3`) |
| `ModusDeepfake.vue` | 5 | lima langkah modus deepfake Presiden (`clicks: 5`) |
| `SpektrumRekayasa.vue` | 6 | empat tingkat rekayasa + kurung detektor vs konteks (`clicks: 5`) |
| `Sorot.vue` | 7, 10 | gambar/video + penanda bernomor + catatan; slot untuk `<li v-click class="pancing">` |
| `EmpatLensa.vue` | 9 | peta 4 cara (cepat↔keahlian × lemah↔kuat) + panel fokus (`clicks: 5`) |
| `PerjalananFile.vue` | 11 | jejak file: kamera → WA → screenshot, chip dicoret (`clicks: 3`) |
| `SkorDetektor.vue` | 12 | satu gambar, tiga skor detektor (ilustrasi) (`clicks: 2`) |
| `JejakUnggahan.vue` | 13 | garis waktu cari balik → sumber pertama → geo/kronolokasi (ilustrasi) (`clicks: 4`) |
| `AlurVerifikasi.vue` | 14 | lima gerbang verifikasi + cabang ke ahli (`clicks: 6`) |
| `SkalaKeyakinan.vue` | 15 | skala 5 tingkat + jarum, kasus bodycam (`clicks: 3`) |
| `Ronde.vue` | 17–22 | ronde latihan: klaim + media (foto/video) + 3 jawaban (asli / asli-klaim salah / AI) + petunjuk bernomor + cara cek tercepat (`clicks: titik + 2`) |
| `RondeSuara.vue` | 23 | ronde suara: klip A–C + tombol putar + gelombang dari file audio; jawaban asli/kloning (`clicks: titik + 2`). Naskah: `NASKAH-SUARA.md` |
| `RantaiBukti.vue` | 26 | rantai pengamanan bukti + hash SHA-256 nyata (`clicks: 3`) |
| `TeksTerurai.vue` | 8 | teks acak → terurai jadi kalimat asli; adaptasi `DecryptedText` Vue Bits tanpa motion-v (`at` = klik pemicu, ekspor = utuh). Vue Bits dipakai hemat: 1–2 slide statement saja |
| `Tangkapan.vue`, `Foto.vue`, `AngkaNaik.vue` | – | dari SIMFONI |

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
- `public/praktik/kasus-1..3.jpg` (kuis & contoh sudah terisi dari Commons — daftar lisensi di `RUJUKAN.md`).
- `public/latihan/suara-a/b/c.m4a` SUDAH ADA (A, C = klon ElevenLabs; B = rekaman asli, sudah dibersihkan & disamakan volumenya; mentah di `bahan-mentah/`, di-gitignore) — naskah di `NASKAH-SUARA.md`.
- Rekaman demo (Google Lens, InVID-WeVerify, EXIF, WA biasa vs dokumen).
- Lembar verifikasi + Google Form.

## Aset
Semua gambar/video contoh dari Wikimedia Commons (`public/kuis`, `public/contoh`, `public/latihan`); lisensi, kredit, dan kandidat lain di `RUJUKAN.md`.
Video `.webm` (Commons); poster `.jpg` diambil dengan Playwright (tidak ada ffmpeg). Kredit CC BY/BY-SA wajib di `.sumber`.

## Privasi
Jangan pakai wajah ATAU SUARA tokoh nyata/anggota Polri untuk contoh buatan AI (klon suara hanya suara Aidil sendiri), jangan memuat data korban/kasus
yang belum dirilis resmi. Kalau repo publik: anggap semua isi bisa dibaca siapa saja.
