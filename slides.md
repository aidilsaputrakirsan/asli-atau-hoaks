---
theme: default
title: Asli atau Rekayasa? Verifikasi Foto dan Video di Era AI
info: Materi untuk kepolisian — Aidil Saputra Kirsan (DRAF untuk diskusi dengan panitia)
colorSchema: light
favicon: /favicon.svg
aspectRatio: 16/9
canvasWidth: 1280
fonts:
  sans: Plus Jakarta Sans
  mono: JetBrains Mono
  weights: '400,500,600,700,800'
  italic: true
transition: fade
drawings:
  persist: false
layout: cover
class: sampul
---

<div>
<p class="mono redup" style="font-size:16px">[Nama acara] · [Satuan/Polda] · [Tanggal]</p>

# Asli atau rekayasa? <span class="biru">Memverifikasi foto dan video di era AI</span>

<p class="redup" style="font-size:24px;max-width:860px;margin-top:20px">Cara memeriksa konten digital sebelum dipercaya, disebarkan, atau dijadikan dasar tindakan.</p>
</div>

<div class="meta">
<div>
<p><b>Aidil Saputra Kirsan, S.ST., M.Tr.Kom.</b></p>
<p class="redup">Dosen Sistem Informasi, Institut Teknologi Kalimantan</p>
</div>
<div style="text-align:right">
<p class="redup">Draf untuk diskusi dengan panitia</p>
</div>
</div>

<!--
DRAF. Judul, durasi, dan susunan menunggu kesepakatan dengan panitia (lihat BAHAN-DISKUSI.md).
Pembuka 1 kalimat: hari ini kita tidak belajar menjadi ahli forensik, tetapi belajar kapan harus curiga, apa yang dicek dulu, dan kapan harus menyerahkan ke ahli.
-->

---
bagian: Pembuka
---

# Saya melihat AI dari sisi <span class="biru">yang membangun dan yang mengaudit</span>

<div class="grid gap-12" style="grid-template-columns: 280px 1fr; margin-top:30px; align-items:start">
<div class="potret"><img src="/aidil.png" alt="Aidil Saputra Kirsan"></div>
<div>
<div class="baris" style="grid-template-columns:170px 1fr;border-top:none">
<span class="no" style="font-size:16px">KAMPUS</span>
<span><span class="nama">Dosen Sistem Informasi ITK</span><br><span class="ket">sejak 2020 · Kepala Lab Inovasi Digital FSTI</span></span>
</div>
<div class="baris" style="grid-template-columns:170px 1fr">
<span class="no" style="font-size:16px">AUDIT</span>
<span><span class="nama">Auditor Teknologi Informasi</span><br><span class="ket">tersertifikasi BNSP (2024)</span></span>
</div>
<div class="baris" style="grid-template-columns:170px 1fr">
<span class="no" style="font-size:16px">INDUSTRI</span>
<span><span class="nama"><img src="/myst-mark.svg" alt="" class="logo-sebaris"> Founder Myst Tech</span><br><span class="ket">membangun aplikasi berbasis AI, termasuk pembaca dokumen KTP/KK</span></span>
</div>
</div>
</div>

<p class="sumber">Sumber: profil aidilsaputrakirsan.github.io.</p>

<!--
30 detik. Poinnya: saya tahu cara AI dipakai untuk MEMBUAT konten, jadi saya juga tahu batas cara mendeteksinya.
Bukan ahli forensik laboratorium — untuk pembuktian di pengadilan, tetap Puslabfor/ahli.
-->

---
bagian: Kuis
clicks: 1
---

# Mana yang <span class="aksen">asli</span>, mana yang <span class="merah">buatan AI</span>?

<div style="margin-top:34px">
<Kuis :buka="$clicks >= 1" :item="[
  { src: '/kuis/a.jpg', jawab: 'ai', ket: '[keterangan: model pembuat, tanda yang bisa dicari]' },
  { src: '/kuis/b.jpg', jawab: 'asli', ket: '[keterangan: sumber foto asli]' },
  { src: '/kuis/c.jpg', jawab: 'ai', ket: '[keterangan]' },
  { src: '/kuis/d.jpg', jawab: 'asli', ket: '[keterangan]' },
]" />
</div>

<p class="redup" style="font-size:17px;margin-top:22px">Angkat tangan untuk setiap gambar. Peserta daring: tulis jawaban di kolom chat, mis. “A asli, B AI…”.</p>

<!--
Kuis 3 menit. Gambar BELUM ADA: siapkan 2 foto asli (bebas lisensi, kredit dicatat) + 2 gambar buatan AI
yang dibuat sendiri (jangan wajah tokoh nyata / anggota Polri). Sebaiknya bertema lokal: jalan Balikpapan, pasar, kerumunan.
Tips: pilih gambar AI yang BAGUS, bukan yang jelas cacat — supaya poin slide berikutnya terasa.
[klik] buka jawaban. Biasanya hasil ruangan mendekati menebak acak.
-->

---
bagian: Kuis
---

# Kalau tebakan kita meleset, <span class="biru">itu wajar</span>

<div class="grid gap-16" style="grid-template-columns: 1fr 1fr; margin-top:40px">
<div class="kolom">
<p class="no">STUDI PNAS, 2022 · 315 PESERTA</p>
<p class="sorot aksen">48%</p>
<p>akurasi menebak wajah asli vs buatan AI. <b>Lebih rendah dari lempar koin (50%).</b></p>
<p class="redup" style="font-size:17px">Setelah dilatih dan diberi umpan balik: naik hanya ke <b>59%</b>. Wajah buatan AI bahkan dinilai <b>lebih dapat dipercaya</b>.</p>
</div>
<div class="kolom" v-click>
<p class="no">STUDI iPROOV, 2025 · 2.000 PESERTA</p>
<p class="sorot merah">0,1%</p>
<p>yang berhasil membedakan <b>semua</b> foto dan video asli/palsu dengan benar, padahal sudah diberi tahu ada deepfake.</p>
<p class="redup" style="font-size:17px">Lebih dari 60% peserta yakin dengan kemampuannya.</p>
</div>
</div>

<p class="sumber">Nightingale &amp; Farid, “AI-synthesized faces are indistinguishable from real faces and more trustworthy”, PNAS 119(8), 2022. iProov, studi “deepfake blindspot”, Feb 2025 (studi vendor, Inggris &amp; AS — baca sebagai indikasi).</p>

<!--
Pesan: mata kita bukan alat ukur. Bahkan yang yakin pun salah.
Jadi materi hari ini bukan "cara melihat lebih teliti", tapi "cara memeriksa yang tidak bergantung pada mata saja".
Catatan: iProov menjual layanan verifikasi biometrik — sebut terus terang bahwa ini studi vendor.
-->

---
bagian: Ancaman
---

# Ini sudah terjadi di Indonesia: <span class="biru">wajah Presiden dipakai untuk menipu</span>

<div class="grid gap-14" style="grid-template-columns: 1.1fr 1fr; margin-top:36px; align-items:start">
<div>
<div class="tanya">“Bapak/Ibu terpilih menerima bantuan pemerintah. Hubungi nomor WhatsApp berikut…”</div>
<p class="redup" style="font-size:17px">Pola pesan dalam video deepfake (ilustrasi, bukan kutipan asli).</p>

- **Jan–Feb 2025:** Dittipidsiber Bareskrim menangkap pelaku video deepfake Presiden, Wapres, dan Menkeu yang menawarkan “bantuan”
- Bahan: video resmi pejabat yang **diunduh dari media sosial**
- Hasil analisis forensik Polri: video **dinyatakan palsu**

</div>
<div class="kotak">
<p class="no mono aksen" style="font-size:13px;margin:0">SATU PELAKU</p>
<p class="sorot-kecil">±100 korban</p>
<p class="redup" style="font-size:16px;margin-top:0">sejak 2024, keuntungan ±Rp65 juta</p>
<p class="no mono aksen" style="font-size:13px;margin:18px 0 0">SECARA NASIONAL (KOMDIGI)</p>
<p class="sorot-kecil">Rp700 miliar</p>
<p class="redup" style="font-size:16px;margin-top:0">kerugian penipuan berbasis AI yang dilaporkan</p>
</div>
</div>

<p class="sumber">Bisnis.com (7 Feb 2025), “Bareskrim kembali tangkap pelaku penipuan pakai video AI Prabowo”; detik.com, analisis forensik deepfake; Bisnis.com (23 Okt 2025), Komdigi soal kerugian penipuan berbasis AI. Angka dari liputan media — cek ulang ke rilis resmi.</p>

<!--
Peserta kepolisian kemungkinan lebih tahu detail kasus ini daripada saya — undang mereka bercerita.
Kalau panitia punya kasus lokal Kaltim/Balikpapan yang boleh dibahas, ganti/tambahkan di sini.
-->

---
bagian: Jenis rekayasa
---

# Tidak semua hoaks butuh AI: <span class="biru">rekayasa punya empat tingkat</span>

<div class="spektrum">
<div>
<div class="pita" style="background:#d9c27a"></div>
<p class="no">01</p>
<p class="judul">Konteks dipelintir</p>
<p class="ket">Foto/video <b>asli</b>, tapi waktu, tempat, atau ceritanya salah.</p>
<p class="contoh">Foto banjir tahun lalu disebut “hari ini”. Kerusuhan di negara lain disebut di kota kita.</p>
</div>
<div>
<div class="pita" style="background:#d99a6a"></div>
<p class="no">02</p>
<p class="judul">Dipotong &amp; disunting</p>
<p class="ket">Bagian dihapus, dipotong, diperlambat, ditambah teks/suara.</p>
<p class="contoh">Video pidato dipotong sehingga maknanya berbalik.</p>
</div>
<div>
<div class="pita" style="background:#cf6a4f"></div>
<p class="no">03</p>
<p class="judul">Diubah dengan AI</p>
<p class="ket">Wajah ditukar, bibir disinkronkan, suara dikloning.</p>
<p class="contoh">Video asli pejabat, mulut dan suara diganti (kasus slide sebelumnya).</p>
</div>
<div>
<div class="pita" style="background:#c0392b"></div>
<p class="no">04</p>
<p class="judul">Dibuat penuh oleh AI</p>
<p class="ket">Tidak pernah ada kamera. Seluruh gambar/video hasil perintah teks.</p>
<p class="contoh">Foto “kejadian” yang tidak pernah terjadi.</p>
</div>
</div>

<p v-click style="margin-top:40px;font-size:22px">Tingkat 01 dan 02 <b>tidak bisa ditangkap detektor AI</b>, karena gambarnya memang asli.</p>

<!--
Ini peta dasar. Banyak orang hanya membayangkan tingkat 04.
Penekanan: detektor AI hanya relevan untuk tingkat 03–04. Untuk 01–02, alatnya adalah pengecekan konteks dan asal-usul.
-->

---
bagian: Pertanyaan inti
class: malam
---

# Pertanyaannya bukan “AI atau bukan?”

<v-click>

<h1 class="biru" style="margin-top:14px">Tetapi: apakah konten ini <span v-mark="{ at: 1, type: 'underline', color: '#0b7a6e', strokeWidth: 4 }">benar menunjukkan</span> apa yang diklaim?</h1>

</v-click>

<div class="grid gap-10" style="grid-template-columns: repeat(4, 1fr); margin-top:70px" v-click>
<div class="kolom"><p class="no">SIAPA</p><p>yang pertama mengunggah?</p></div>
<div class="kolom"><p class="no">KAPAN</p><p>sebenarnya diambil?</p></div>
<div class="kolom"><p class="no">DI MANA</p><p>lokasinya cocok?</p></div>
<div class="kolom"><p class="no">BAGAIMANA</p><p>ada tanda diubah/dibuat?</p></div>
</div>

<!--
Ini pernyataan inti sesi. Foto asli dengan klaim palsu tetap hoaks.
Foto buatan AI yang diberi label jelas "ilustrasi" bukan hoaks.
-->

---
bagian: Perbandingan
---

# Empat cara memeriksa, <span class="biru">masing-masing punya titik buta</span>

<div style="margin-top:28px">

| Cara | Yang diperiksa | Kuat untuk | Titik butanya | Bisa jadi dasar tindakan? |
|---|---|---|---|---|
| **Mata** | jari, teks, bayangan, pantulan, gerak bibir | menyaring awal, cepat | model baru makin rapi; akurasi manusia ±50% | <span class="status palsu">TIDAK SENDIRIAN</span> |
| **Asal-usul file** | metadata, Content Credentials (C2PA), watermark | membuktikan sumber bila tersedia | sering hilang saat dikirim lewat WA/medsos | <span class="status asli">KUAT BILA ADA</span> |
| **Alat deteksi AI** | pola piksel, frekuensi, artefak kompresi | tingkat 03–04 | salah positif &amp; negatif; kalah oleh model baru dan kompresi ulang | <span class="status ragu">PETUNJUK</span> |
| **Konteks (OSINT)** | unggahan pertama, lokasi, waktu, saksi | tingkat 01–02 | butuh waktu dan keterampilan | <span class="status asli">KUAT</span> |

</div>

<p v-click style="margin-top:22px;font-size:21px">Tidak ada satu cara yang cukup. <b>Kesimpulan yang kuat datang dari beberapa cara yang saling menguatkan.</b></p>

<p class="sumber">Akurasi manusia: Nightingale &amp; Farid (2022). Batas detektor: lihat slide 11.</p>

<!--
Ini slide perbandingan utama yang diminta panitia. Ajak peserta: selama ini satuan Bapak/Ibu paling sering memakai cara yang mana?
Biasanya: mata + "tanya grup". Yang paling jarang: asal-usul file.
-->

---
bagian: Cara 1 · Mata
---

# Mata manusia: <span class="biru">penyaring awal, bukan hakim</span>

<div class="grid gap-14" style="grid-template-columns: 1fr 1fr; margin-top:32px">
<div>
<h2>Foto</h2>

- **Tangan dan jari** — jumlah, sambungan, menyatu dengan benda
- **Tulisan** — papan nama, plat nomor, seragam: huruf rusak/tak bermakna
- **Cahaya dan bayangan** — arah bayangan tidak konsisten
- **Pantulan** — kaca, mata, air tidak cocok dengan adegan
- **Detail berulang** — wajah kerumunan, pola latar yang “meleleh”

</div>
<div>
<h2>Video &amp; suara</h2>

- **Mulut dan gigi** — sinkron bibir, gigi kabur
- **Batas wajah** — tepi rambut, telinga, kacamata berkedip
- **Gerak kepala** — wajah “bergeser” saat menoleh
- **Suara** — datar, tanpa napas, intonasi tak wajar
- **Kualitas sengaja jelek** — buram/kecil untuk menutupi cacat

</div>
</div>

<p v-click class="kotak" style="margin-top:24px;font-size:18px;padding:14px 20px"><span class="status ragu">PERHATIAN</span>&nbsp; Tanda-tanda ini <b>cepat usang</b>. Tidak menemukan cacat ≠ asli.</p>

<!--
Kalau ada waktu: tunjukkan 1 contoh gambar AI dengan cacat (perbesar bagian tangan/tulisan).
Tekankan: daftar ini berguna untuk curiga, BUKAN untuk menyimpulkan asli.
-->

---
bagian: Cara 2 · Asal-usul
---

# Asal-usul file: <span class="biru">bukti terkuat, tapi paling mudah hilang</span>

<div class="grid gap-10" style="grid-template-columns: repeat(3, 1fr); margin-top:34px">
<div class="kolom">
<p class="no">METADATA (EXIF)</p>
<h2>Jejak kamera</h2>
<p>Merek/tipe HP, waktu ambil, kadang lokasi GPS dan perangkat lunak penyunting.</p>
<p class="redup" style="font-size:16px">Alat: ExifTool, fitur “info” di galeri.</p>
</div>
<div class="kolom">
<p class="no">CONTENT CREDENTIALS (C2PA)</p>
<h2>“Label gizi” digital</h2>
<p>Catatan bertanda tangan: dibuat dengan kamera/aplikasi apa, diedit apa saja.</p>
<p class="redup" style="font-size:16px">Alat: contentcredentials.org/verify</p>
</div>
<div class="kolom">
<p class="no">WATERMARK TAK TERLIHAT</p>
<h2>Tanda di dalam piksel</h2>
<p>Sebagian pembuat AI menanam tanda yang tetap ada meski metadata dihapus (mis. SynthID dari Google).</p>
<p class="redup" style="font-size:16px">Hanya terbaca alat dari pembuatnya.</p>
</div>
</div>

<div v-click class="kotak" style="margin-top:28px;padding:16px 22px">
<p style="margin:0;font-size:18px"><span class="status ragu">PENTING</span>&nbsp; Foto yang dikirim biasa lewat WhatsApp/medsos umumnya <b>kehilangan metadata</b>. Minta file asli (kirim sebagai <b>dokumen</b>, atau ambil langsung dari perangkat). <b>Metadata kosong bukan bukti palsu</b> — dan metadata juga bisa dipalsukan.</p>
</div>

<p class="sumber">C2PA: Coalition for Content Provenance and Authenticity (c2pa.org). Perilaku WhatsApp: pengujian umum, dapat berubah per versi — demo ulang sebelum acara.</p>

<!--
Bagi penyidik, ini poin paling praktis: amankan file paling asli sedini mungkin.
Demo singkat (opsional): kirim satu foto lewat WA biasa vs sebagai dokumen, lalu bandingkan metadata.
-->

---
bagian: Cara 3 · Alat deteksi
---

# Alat deteksi AI memberi <span class="biru">peluang, bukan vonis</span>

<div class="grid gap-14" style="grid-template-columns: 1fr 1fr; margin-top:32px; align-items:start">
<div>
<h2>Contoh alat (gratis/terbuka)</h2>

- **InVID-WeVerify** — ekstensi browser: pecah video jadi bingkai kunci, cari balik, baca metadata
- **Forensically** — analisis level error (ELA), deteksi bagian yang disalin-tempel
- **Detektor AI komersial** — memberi skor “kemungkinan buatan AI”

</div>
<div class="kotak">
<p class="mono" style="font-size:13px;margin:0 0 6px;color:var(--samar)">CONTOH HASIL DETEKTOR</p>
<p class="sorot-kecil merah" style="margin:0">87% AI</p>
<p style="font-size:17px">artinya <b>bukan</b> “87% pasti palsu”. Artinya: menurut model ini, pola gambarnya mirip contoh AI yang pernah ia pelajari.</p>

- Bisa **salah menuduh** foto asli yang banyak diedit/kompres
- Bisa **lolos** untuk model AI terbaru
- Hasil beda alat bisa **saling bertentangan**

</div>
</div>

<p class="sumber">InVID-WeVerify: proyek Uni Eropa untuk verifikasi media (weverify.eu). Forensically: 29a.ch/photo-forensics. Contoh skor = ilustrasi.</p>

<!--
Kalimat kunci untuk penyidik: "Jangan pernah menulis di laporan 'menurut aplikasi X, 87% palsu' sebagai satu-satunya dasar."
Gunakan detektor untuk memutuskan APA yang perlu diperiksa lebih dalam.
-->

---
bagian: Cara 4 · Konteks
---

# Konteks (OSINT): <span class="biru">cara paling kuat untuk hoaks sehari-hari</span>

<div class="alur" style="grid-template-columns: repeat(4, 1fr); margin-top:40px">
<div><p class="tahap">CARI BALIK</p><p class="judul">Pernah muncul sebelumnya?</p><p class="ket">Google Lens, TinEye, Yandex. Video: ambil bingkai kunci dulu.</p></div>
<div><p class="tahap">SUMBER PERTAMA</p><p class="judul">Siapa yang mengunggah pertama?</p><p class="ket">Urutkan waktu unggah; akun asli atau baru dibuat?</p></div>
<div><p class="tahap">GEOLOKASI</p><p class="judul">Tempatnya cocok?</p><p class="ket">Rambu, toko, bangunan → cocokkan dengan Google Maps/Street View.</p></div>
<div><p class="tahap">KRONOLOKASI</p><p class="judul">Waktunya cocok?</p><p class="ket">Arah bayangan matahari (SunCalc), cuaca, peristiwa pada hari itu.</p></div>
</div>

<div class="grid gap-10" style="grid-template-columns: 1fr 1fr; margin-top:40px" v-click>
<div class="kolom"><p class="no">KEUNGGULAN</p><p>Tetap bekerja walau gambar sudah dikompres, dipotong, atau dibuat oleh AI terbaru.</p></div>
<div class="kolom"><p class="no">RUJUKAN CEK FAKTA</p><p>turnbackhoax.id (Mafindo), cekfakta.com, laman klarifikasi Komdigi.</p></div>
</div>

<!--
Ini yang paling bisa langsung dipakai anggota di lapangan dan humas.
Demo 2 menit (disarankan): ambil 1 foto viral lama → Google Lens → ketemu unggahan aslinya bertahun-tahun lalu.
-->

---
bagian: Alur kerja
---

# Lima langkah sebelum menyimpulkan: <span class="biru">dari pesan masuk sampai laporan</span>

<div class="alur" style="margin-top:44px">
<div><p class="tahap">01</p><p class="judul">Amankan</p><p class="ket">Simpan file paling asli + tautan + tangkapan layar unggahan. Catat waktu &amp; hash.</p></div>
<div><p class="tahap">02</p><p class="judul">Asal-usul</p><p class="ket">Metadata, Content Credentials, watermark.</p></div>
<div><p class="tahap">03</p><p class="judul">Konteks</p><p class="ket">Cari balik, sumber pertama, lokasi, waktu.</p></div>
<div><p class="tahap">04</p><p class="judul">Teknis</p><p class="ket">Periksa visual + alat deteksi. Bandingkan beberapa alat.</p></div>
<div><p class="tahap">05</p><p class="judul">Simpulkan</p><p class="ket">Pakai tingkat keyakinan, catat dasar setiap temuan.</p></div>
</div>

<div class="grid gap-10" style="grid-template-columns: 1fr 1fr; margin-top:44px">
<div class="kolom" v-click><p class="no">KENAPA “AMANKAN” DULUAN</p><p>Unggahan bisa dihapus, file bisa dikompres ulang. Yang hilang di langkah 01 tidak bisa diperiksa di langkah 02–04.</p></div>
<div class="kolom" v-click><p class="no">KAPAN DISERAHKAN KE AHLI</p><p>Bila konten akan menjadi <b>alat bukti</b> atau dasar penindakan: ke laboratorium forensik / ahli digital.</p></div>
</div>

<!--
Ini bisa menjadi draf SOP sederhana untuk satuan. Tawarkan untuk disusun bersama di sesi diskusi/praktik.
Hash: sidik jari file (mis. SHA-256). Bila satu bit berubah, hash berubah — membuktikan file tidak diutak-atik sejak diamankan.
-->

---
bagian: Alur kerja
---

# Jangan hanya “asli” atau “hoaks”: <span class="biru">tulis tingkat keyakinannya</span>

<div class="tangga" style="margin-top:34px">
<div><span class="status asli">TERVERIFIKASI ASLI</span><p>Sumber pertama jelas, konteks cocok, asal-usul file mendukung.</p></div>
<div><span class="status asli" style="opacity:.75">KONSISTEN, BELUM TERVERIFIKASI</span><p>Tidak ditemukan kejanggalan, tapi sumber pertama belum ditemukan.</p></div>
<div><span class="status ragu">TIDAK DAPAT DITENTUKAN</span><p>Bukti tidak cukup ke arah mana pun. <b>Ini jawaban yang sah.</b></p></div>
<div><span class="status palsu" style="opacity:.75">ADA INDIKASI REKAYASA</span><p>Beberapa temuan janggal (visual/alat), belum dikonfirmasi.</p></div>
<div><span class="status palsu">TERBUKTI REKAYASA</span><p>Ditemukan versi asli, konteks terbantah, atau dikonfirmasi ahli.</p></div>
</div>

<!--
Menulis tingkat keyakinan melindungi dua arah: tidak gegabah menuduh, tidak gegabah membenarkan.
"Tidak dapat ditentukan" lebih jujur daripada memaksa vonis — sama seperti AI yang lebih baik bilang "tidak tahu" daripada menebak.
-->

---
bagian: Bahaya sebaliknya
class: malam
---

# Bahaya baru: bukti asli <span class="merah">disangkal sebagai “itu AI”</span>

<div class="grid gap-14" style="grid-template-columns: 1.2fr 1fr; margin-top:44px; align-items:start">
<div>
<p style="font-size:23px">Saat semua orang tahu deepfake itu ada, pelaku bisa berkata <b>“video itu rekayasa”</b> terhadap rekaman yang sebenarnya asli.</p>
<p class="redup" style="font-size:19px">Para peneliti hukum menyebutnya <b><i>liar’s dividend</i></b> — “keuntungan bagi si pembohong”.</p>
</div>
<div class="kotak">
<p class="mono" style="font-size:13px;margin:0 0 8px;color:var(--samar)">IMPLIKASI UNTUK PENYIDIK</p>

- Verifikasi bukan hanya untuk membongkar yang palsu, tetapi untuk **mempertahankan yang asli**
- Rantai pengamanan bukti (*chain of custody*) makin penting
- Rekaman resmi (bodycam, CCTV) perlu dijaga asal-usulnya sejak awal

</div>
</div>

<p class="sumber">Chesney &amp; Citron, “Deep Fakes: A Looming Challenge for Privacy, Democracy, and National Security”, California Law Review 107 (2019).</p>

<!--
Ini sering jadi poin "aha" untuk aparat: deepfake bukan cuma soal hoaks, tapi soal pembuktian di pengadilan.
-->

---
bagian: Hukum & pembuktian
---

# Dari temuan ke alat bukti: <span class="biru">yang perlu dijaga sejak awal</span>

<div class="grid gap-14" style="grid-template-columns: 1fr 1fr; margin-top:32px">
<div class="kolom">
<p class="no">DASAR HUKUM YANG RELEVAN</p>

- **UU ITE** (UU 11/2008 jo. UU 1/2024): informasi elektronik sebagai alat bukti (Ps. 5); manipulasi informasi elektronik agar seolah-olah otentik (Ps. 35); pemberitahuan bohong yang menimbulkan kerusuhan (Ps. 28 ayat 3)
- **KUHP baru** (UU 1/2023), berlaku sejak 2 Januari 2026

</div>
<div class="kolom">
<p class="no">YANG MEMBUAT TEMUAN BERTAHAN</p>

- File asli diamankan, **hash** dicatat
- Bekerja pada **salinan**, bukan file asli
- Setiap langkah dan alat **dicatat** (siapa, kapan, alat apa)
- Kesimpulan teknis untuk persidangan oleh **ahli forensik digital**

</div>
</div>

<p class="sumber">Rujukan pasal untuk diskusi; teks resmi di JDIH dan penafsiran oleh ahli hukum. Peserta dari kepolisian lebih berwenang di bagian ini — DRAF, minta masukan panitia.</p>

<!--
Saya bukan ahli hukum: bagian ini saya sampaikan sebagai pengantar, lalu serahkan ke peserta/penyidik yang lebih paham.
Usulkan ke panitia: apakah ada narasumber dari Ditressiber/Labfor yang bisa mengisi bagian ini?
-->

---
bagian: Praktik
---

# Praktik 15 menit: <span class="biru">periksa tiga konten bersama</span>

<div class="grid gap-10" style="grid-template-columns: repeat(3, 1fr); margin-top:34px">
<div>
<Tangkapan src="/praktik/kasus-1.jpg" label="Kasus 1 — foto lama, klaim baru" :tinggi="200" />
<p class="redup" style="font-size:16px">Alat: Google Lens → temukan unggahan pertama.</p>
</div>
<div>
<Tangkapan src="/praktik/kasus-2.jpg" label="Kasus 2 — gambar buatan AI" :tinggi="200" />
<p class="redup" style="font-size:16px">Alat: periksa visual + 2 detektor, bandingkan.</p>
</div>
<div>
<Tangkapan src="/praktik/kasus-3.jpg" label="Kasus 3 — foto asli, metadata lengkap" :tinggi="200" />
<p class="redup" style="font-size:16px">Alat: baca EXIF, cocokkan lokasi &amp; waktu.</p>
</div>
</div>

<p style="margin-top:26px;font-size:19px">Per kelompok: isi <b>lembar verifikasi</b> (5 langkah + tingkat keyakinan). Peserta daring: versi Google Form.</p>

<!--
OPSIONAL — tergantung durasi & format dari panitia. Bisa diganti demo langsung oleh pembicara bila tidak ada sesi praktik.
Semua kasus harus dibuat/dipilih sendiri: tanpa korban nyata, tanpa wajah anggota Polri/tokoh nyata.
-->

---
bagian: Rekomendasi
---

# Tiga hal yang bisa dimulai <span class="biru">minggu ini</span>

<div style="margin-top:34px">
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr">
<span class="no">01</span><span class="nama">Satu alur verifikasi tertulis</span><span class="ket">Lima langkah + lima tingkat keyakinan, satu halaman, dipakai semua anggota yang menangani laporan konten.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr">
<span class="no">02</span><span class="nama">Kebiasaan “amankan dulu”</span><span class="ket">File asli + tautan + tangkapan layar + hash, sebelum konten dihapus pengunggah.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr">
<span class="no">03</span><span class="nama">Jejaring verifikasi</span><span class="ket">Kanal cepat dengan pemeriksa fakta, Komdigi, dan kampus untuk kasus yang butuh analisis lebih dalam.</span>
</div>
</div>

<!--
Kampus (ITK) bisa membantu di nomor 3: pelatihan lanjutan, riset alat deteksi untuk konteks lokal.
Sampaikan sebagai tawaran, bukan jualan.
-->

---
bagian: Penutup
class: malam
---

# Membuat konten palsu sudah murah.

<v-click>

<h1 class="biru" style="margin-top:10px">Yang mahal adalah kebiasaan <span v-mark="{ at: 1, type: 'underline', color: '#0b7a6e', strokeWidth: 4 }">memeriksa sebelum percaya</span>.</h1>

</v-click>

<div class="grid gap-12" style="grid-template-columns: 1fr 1fr; margin-top:70px; align-items:end">
<div class="kolom">
<p class="no">KONTAK</p>
<p>aidil@lecturer.itk.ac.id · 085398952880</p>
</div>
<div class="ikuti">
<img src="/qr-instagram.svg" alt="QR ke Instagram @aidilsaputrakirsan">
<div><p><b>Konten edukasi AI</b> <span class="mono aksen">@aidilsaputrakirsan</span></p><p class="redup">Instagram · pindai dengan kamera HP</p></div>
</div>
</div>

<!--
Kalimat penutup. Lalu tanya jawab.
-->

---
bagian: Referensi
---

# Sumber

<div style="margin-top:28px;font-size:17px">

- Nightingale, S. J., &amp; Farid, H. (2022). AI-synthesized faces are indistinguishable from real faces and more trustworthy. *PNAS*, 119(8).
- iProov (Feb 2025). Studi “deepfake blindspot” — 2.000 responden Inggris &amp; AS (studi vendor).
- Bisnis.com (7 Feb 2025); detik.com — penangkapan dan analisis forensik video deepfake Presiden oleh Dittipidsiber Bareskrim.
- Bisnis.com (23 Okt 2025) — Komdigi: kerugian penipuan berbasis AI.
- Chesney, R., &amp; Citron, D. (2019). Deep Fakes: A Looming Challenge for Privacy, Democracy, and National Security. *California Law Review*, 107.
- C2PA / Content Credentials (c2pa.org, contentcredentials.org); InVID-WeVerify (weverify.eu); Forensically (29a.ch).
- UU 11/2008 jo. UU 19/2016 jo. UU 1/2024 tentang ITE; UU 1/2023 tentang KUHP.

</div>

<p class="sumber">DRAF — angka dari liputan media akan dicek ulang ke sumber primer sebelum acara.</p>
