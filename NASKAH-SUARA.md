# Naskah Ronde 7 — pesan suara (slide 23)

Tiga klip, semuanya suara Aidil. **A dan C = klon ElevenLabs**, **B = rekaman asli**.
Simpan sebagai `public/latihan/suara-a.m4a`, `suara-b.m4a`, `suara-c.m4a` (AAC 128 kbps, sudah diproses — lihat bawah).

## Supaya adil (penting)
- **Durasi mirip**: 12–18 detik per klip.
- **Kualitas disamakan**: kirim ketiga file ke diri sendiri lewat WhatsApp sebagai *voice note*/audio,
  lalu unduh lagi. Dengan begitu kompresinya sama, dan peserta tidak bisa menebak dari "bersih/tidaknya" suara.
- Rekaman asli (B): pakai HP, di ruangan biasa, gaya bicara santai seperti VN sungguhan.
- Klon (A, C): di ElevenLabs, naikkan sedikit *style/expressiveness* dan beri jeda alami (koma, "eh", "ya")
  supaya tidak terdengar seperti membaca.
- Jangan sebut nomor rekening, bank, nomor HP, nama orang, atau instansi sungguhan.

## A — kloning AI · modus "darurat, minta transfer"
> Assalamualaikum, ini saya, Aidil. Maaf ya, saya lagi di bandara, HP saya sebentar lagi mati.
> Tolong bantu transfer dulu satu juta lima ratus, nomor rekeningnya saya kirim habis ini.
> Nanti sore langsung saya ganti. Jangan telepon dulu ya, saya lagi antre masuk pesawat.

## B — rekaman asli · pesan biasa
> Halo, ini Aidil. Saya kirim voice note aja karena lagi nyetir.
> Materi untuk acara besok sudah saya kirim lewat email, tolong dicek ya.
> Kalau ada yang kurang, telepon saya saja nanti malam, saya pegang HP terus kok.

## C — kloning AI · modus "kode OTP salah kirim"
> Eh, maaf ganggu. Barusan ada kode enam angka masuk ke HP kamu, nggak?
> Itu salah kirim, harusnya ke nomor saya. Tolong kirim kodenya ke sini ya, buru-buru nih,
> mau dipakai sekarang. Makasih banyak.

## Kenapa naskahnya begini
- A dan C memuat pola penipuan nyata: **mendesak + uang/OTP + menghindari telepon balik**.
- B sengaja tidak meminta apa-apa yang berisiko dan malah **mengajak telepon**. Ini kunci pelajarannya:
  yang membedakan bukan suaranya, tetapi isi dan permintaannya.
- Urutan A (AI), B (asli), C (AI) boleh diacak. Kalau diacak, ubah `jawab` di `slides.md` (Ronde 7).

## Sebelum tampil
- Isi bagian `[ISI: ...]` di catatan pembicara slide 23 (berapa lama rekaman yang dipakai untuk membuat klon).
- Uji putar di laptop dan proyektor/speaker ruangan. Klik tombol ▶ di klip, bukan tombol maju slide.

## Status file (20 Nov 2026)
- A = klon `ElevenLabs_…08_21_09…` (16,8 dtk) · B = rekaman asli `Upoji Coffe 2` · C = klon `ElevenLabs_…08_37_49…` (12,1 dtk).
  Asumsi: klip yang lebih panjang = naskah A (transfer). Kalau terbalik, tukar nama `suara-a` dan `suara-c`.
- Rekaman asli dibersihkan dari noise kafe (high-pass 85 Hz, noise reduction, kompresor ringan, gerbang jeda).
- Ketiganya disamakan: volume -16,5 LUFS, jeda awal 0,15 dtk, format AAC 128 kbps 44,1 kHz mono, tanpa metadata nama file asli.
- File mentah + skrip pemrosesan ada di `bahan-mentah/` (di-.gitignore, tidak ikut build).
