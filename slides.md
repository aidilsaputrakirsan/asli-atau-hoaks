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

<p class="redup" style="font-size:23px;max-width:860px;margin-top:18px">Cara memeriksa konten digital sebelum dipercaya, disebarkan, atau dijadikan dasar tindakan.</p>
</div>

<SampulAlur />

<div class="meta">
<div>
<p><b>Aidil Saputra Kirsan, S.ST., M.Tr.Kom.</b></p>
<p class="redup">Dosen Sistem Informasi, Institut Teknologi Kalimantan</p>
</div>
<div style="text-align:right">
<p class="redup mono" style="font-size:14px">draf untuk diskusi dengan panitia</p>
</div>
</div>

<!--
DRAF. Judul, durasi, dan susunan menunggu kesepakatan dengan panitia (lihat BAHAN-DISKUSI.md).
Pembuka: hari ini kita tidak belajar menjadi ahli forensik, tetapi belajar kapan harus curiga,
apa yang dicek dulu, dan kapan harus menyerahkan ke ahli. Gambar di sampul = isi sesi ini:
konten beredar → diperiksa → asli, belum pasti, atau rekayasa.
-->

---
bagian: Pembuka
---

# Saya melihat AI dari sisi <span class="biru">yang membangun dan yang mengaudit</span>

<div class="grid gap-12" style="grid-template-columns: 280px 1fr; margin-top:30px; align-items:start">
<div class="potret"><img src="/aidil.png" alt="Aidil Saputra Kirsan"></div>
<div>
<div class="baris" style="grid-template-columns:140px 1fr;border-top:none" v-click>
<span class="label-kolom">kampus</span>
<span><span class="nama">Dosen Sistem Informasi ITK</span><br><span class="ket">sejak 2020 · Kepala Lab Inovasi Digital FSTI</span></span>
</div>
<div class="baris" style="grid-template-columns:140px 1fr" v-click>
<span class="label-kolom">audit</span>
<span><span class="nama">Auditor Teknologi Informasi</span><br><span class="ket">tersertifikasi BNSP (2024)</span></span>
</div>
<div class="baris" style="grid-template-columns:140px 1fr" v-click>
<span class="label-kolom">industri</span>
<span><span class="nama"><img src="/myst-mark.svg" alt="" class="logo-sebaris"> Founder Myst Tech</span><br><span class="ket">membangun aplikasi AI — termasuk yang membaca foto KTP dan KK</span></span>
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
  { src: '/kuis/a.jpg', jawab: 'ai', ket: 'Cahaya keemasan, setiap detail “terlalu rapi”.' },
  { src: '/kuis/b.jpg', jawab: 'asli', ket: 'Positano, Italia. Mendung, perahu berserakan.' },
  { src: '/kuis/c.jpg', jawab: 'ai', ket: 'Tata saji ala iklan, latar gelap kabur.' },
  { src: '/kuis/d.jpg', jawab: 'asli', ket: 'Sate Madura. Piring warung, cahaya apa adanya.' },
]" />
</div>

<p class="sumber">Wikimedia Commons — A: Dennis S. Hurd (AI), CC BY 4.0 · B: Stephanie Krist, CC0 · C: Dennis S. Hurd (AI), CC0 · D: Happywu, CC BY-SA 4.0.</p>

<!--
Kuis 3 menit. Minta angkat tangan per gambar; peserta daring tulis di chat "A asli, B AI…".
[klik] buka jawaban. Biasanya hasil ruangan mendekati menebak acak.
Pelajaran: gambar AI sering TERLALU SEMPURNA, foto asli tampak biasa. Tapi ini bukan aturan pasti —
AI bisa diminta membuat gambar yang "biasa" dan buram.
Bisa diganti gambar bertema lokal (Balikpapan) buatan sendiri; jangan wajah tokoh nyata / anggota Polri.
-->

---
bagian: Kuis
clicks: 3
---

# Kalau tebakan kita meleset, <span class="biru">itu wajar</span>

<div style="margin-top:22px">
<SkalaTebak />
</div>

<p class="sumber">Nightingale &amp; Farid, “AI-synthesized faces are indistinguishable from real faces and more trustworthy”, PNAS 119(8), 2022. iProov, studi “deepfake blindspot”, Feb 2025 — studi vendor, Inggris &amp; AS.</p>

<!--
[klik 1] 48%: rata-rata peserta sedikit di bawah lempar koin.
[klik 2] Dilatih dan diberi umpan balik pun hanya 59%.
[klik 3] Studi iProov: 0,1% benar semua. iProov menjual layanan verifikasi biometrik — sebut terus terang ini studi vendor.
Pesan: mata kita bukan alat ukur. Materi hari ini adalah cara memeriksa yang tidak bergantung pada mata saja.
-->

---
bagian: Ancaman
clicks: 5
---

# Ini sudah terjadi di Indonesia: <span class="biru">wajah Presiden dipakai untuk menipu</span>

<div style="margin-top:36px">
<ModusDeepfake />
</div>

<div class="grid gap-16" style="grid-template-columns: 1fr 1fr; margin-top:34px; border-top:1px solid var(--garis); padding-top:18px">
<div class="angka-baris"><p class="sorot-kecil">± 100 korban</p><p class="redup">satu pelaku, sejak 2024 — keuntungan ±Rp65 juta</p></div>
<div class="angka-baris"><p class="sorot-kecil merah">Rp<AngkaNaik :sampai="700" /> miliar</p><p class="redup">kerugian penipuan berbasis AI secara nasional (Komdigi)</p></div>
</div>

<p class="sumber">Bisnis.com (7 Feb 2025), penangkapan pelaku video AI Presiden; detik.com, analisis forensik; Bisnis.com (23 Okt 2025), Komdigi. Angka dari liputan media — cek ulang ke rilis resmi.</p>

<!--
[klik 1–5] Satu langkah per klik. Pola pesan "bantuan pemerintah" adalah ilustrasi, bukan kutipan asli.
Peserta kemungkinan lebih tahu detail kasus ini — undang mereka bercerita.
Kalau panitia punya kasus lokal Kaltim yang boleh dibahas, tambahkan di sini.
-->

---
bagian: Jenis rekayasa
clicks: 5
---

# Tidak semua hoaks butuh AI: <span class="biru">rekayasa punya empat tingkat</span>

<div style="margin-top:30px">
<SpektrumRekayasa />
</div>

<!--
[klik 1–4] Satu tingkat per klik. Banyak orang hanya membayangkan tingkat 04.
[klik 5] Pembagian penting: detektor AI hanya relevan untuk 03–04. Untuk 01–02, alatnya konteks dan asal-usul.
-->

---
bagian: Jenis rekayasa
clicks: 4
---

# Tingkat 04: rekaman bodycam polisi <span class="biru">yang tidak pernah direkam</span>

<div style="margin-top:26px">
<Sorot video="/contoh/bodycam-sora.webm" src="/contoh/bodycam-sora.jpg" :tinggi="410" :rasio="0.55" :titik="[
  { x: 50, y: 4, judul: 'Stempel waktu & kode perangkat', ket: 'Meniru tampilan kamera tubuh asli — memberi kesan resmi.' },
  { x: 58, y: 33, judul: 'Malam, sirene, kamera goyang', ket: 'Gambar buram secara wajar, sehingga cacat AI tersamar.' },
  { x: 22, y: 92, judul: 'Watermark kecil di pojok', ket: 'Satu-satunya tanda pembuatnya — dan mudah dipotong.' },
]">
<li v-click="4" class="pancing">Video seperti ini beredar setelah sebuah insiden, berjudul “rekaman bocor”. <b>Apa yang Bapak/Ibu periksa pertama kali?</b></li>
</Sorot>
</div>

<p class="sumber">“Example of Sora AI-Generated Police Body Camera Footage”, Wikimedia Commons, domain publik; orang di video = pengunggah, setuju dipublikasi. Dibuat dengan Sora, 10 detik.</p>

<!--
Slide paling relevan untuk polisi: bukan wajah pejabat, tapi "bukti" yang meniru alat kerja polisi sendiri.
Video berputar otomatis. [klik 1–3] penanda. [klik 4] pertanyaan ke peserta.
Jawaban yang diharapkan: cari sumber pertama, cek apakah ada insiden di waktu/lokasi itu,
minta rekaman asli dari sistem bodycam resmi (asal-usul).
-->

---
layout: center
class: malam
bagian: Pertanyaan inti
---

<div style="max-width:1020px">
<h1 style="font-size:60px"><TeksTerurai teks="Pertanyaannya bukan “AI atau bukan?”" /></h1>
<h1 style="font-size:60px;margin-top:14px" class="biru">Tetapi: apakah konten ini <span v-mark="{ at: 1, type: 'underline', color: '#0b7a6e', strokeWidth: 4 }">benar menunjukkan</span> apa yang diklaim?</h1>
<p v-click="2" class="mono redup" style="font-size:18px;margin-top:40px">siapa yang pertama mengunggah · kapan diambil · di mana · adakah tanda diubah</p>
</div>

<!--
Jeda. Ini pernyataan inti sesi.
Foto asli dengan klaim palsu tetap hoaks. Gambar AI yang diberi label jelas "ilustrasi" bukan hoaks.
-->

---
bagian: Perbandingan
clicks: 5
---

# Empat cara memeriksa, <span class="biru">masing-masing punya titik buta</span>

<div style="margin-top:22px">
<EmpatLensa />
</div>

<p class="sumber">Posisi pada peta = penilaian kualitatif untuk diskusi, bukan hasil pengukuran. Akurasi mata: Nightingale &amp; Farid (2022).</p>

<!--
Ini slide perbandingan yang diminta panitia. [klik 1–4] satu cara per klik, panel kanan: kuat untuk / titik buta.
Asal-usul punya garis putus-putus: sangat kuat bila jejaknya ada, lemah bila sudah hilang (lewat WA).
[klik 5] Garis biru: kesimpulan kuat = beberapa cara saling menguatkan.
Tanya peserta: selama ini satuan Bapak/Ibu paling sering memakai cara yang mana? Biasanya: mata + "tanya grup".
-->

---
bagian: Cara 1 · Mata
clicks: 5
---

# Mata manusia: <span class="biru">penyaring awal, bukan hakim</span>

<div style="margin-top:24px">
<Sorot src="/contoh/kerangka-raksasa.jpg" :tinggi="360" :rasio="1.5" kredit="“Penggalian kerangka raksasa” — seluruhnya buatan Midjourney · domain publik, Wikimedia Commons" :titik="[
  { x: 16, y: 63, judul: 'Tangan', ket: 'Tenggelam ke tanah, menyatu dengan benda.' },
  { x: 52, y: 30, judul: 'Wajah di kerumunan', ket: 'Mirip satu sama lain, ekspresi seragam.' },
  { x: 47, y: 66, judul: 'Objek utama', ket: 'Terlalu utuh, gigi terlalu rapi untuk fosil.' },
  { x: 82, y: 12, judul: 'Cahaya', ket: 'Sinematik seperti poster film, bukan foto lapangan.' },
]">
<li v-click="5" class="pancing">Tanda-tanda ini <b>cepat usang</b>. Tidak menemukan cacat bukan berarti asli.</li>
</Sorot>
</div>

<!--
Ajak peserta mencari kejanggalan dulu sebelum klik. [klik 1–4] penanda.
Lalu tanya: kalau gambarnya dikecilkan dan dikirim di grup WA dengan judul "penemuan di Kalimantan", masihkah kita melihatnya?
Untuk video: perhatikan sinkron bibir, tepi wajah, gigi kabur, suara tanpa napas; kualitas sengaja jelek untuk menutupi cacat.
-->

---
bagian: Cara 2 · Asal-usul
clicks: 4
---

# Asal-usul file: <span class="biru">jejak terkuat, tapi paling mudah hilang</span>

<div style="margin-top:34px">
<PerjalananFile />
</div>

<p v-click="4" style="margin-top:26px;font-size:21px">Minta <b>file paling asli</b> — kirim sebagai dokumen, atau ambil langsung dari perangkat. <span class="biru"><b>Metadata kosong bukan bukti palsu</b></span>, dan metadata juga bisa dipalsukan.</p>

<p class="sumber">C2PA / Content Credentials: c2pa.org, cek di contentcredentials.org/verify. Watermark tak terlihat mis. SynthID (Google), terbaca hanya oleh alat pembuatnya. Perilaku WhatsApp dapat berubah per versi — demo ulang sebelum acara.</p>

<!--
[klik 1] Di kamera: jejak lengkap. [klik 2] WA biasa: dicoret. [klik 3] Screenshot: tinggal piksel.
[klik 4] Poin paling praktis untuk penyidik: amankan file paling asli sedini mungkin.
Demo opsional: kirim satu foto lewat WA biasa vs sebagai dokumen, lalu bandingkan metadatanya.
-->

---
bagian: Cara 3 · Alat deteksi
clicks: 2
---

# Alat deteksi AI memberi <span class="biru">peluang, bukan vonis</span>

<div style="margin-top:32px">
<SkorDetektor src="/kuis/a.jpg" />
</div>

<p class="mono redup" style="font-size:14px;margin-top:30px">alat gratis untuk mulai: InVID-WeVerify (pecah video jadi bingkai, cari balik, metadata) · Forensically (analisis error level, salin-tempel)</p>

<p class="sumber">Skor = ilustrasi. InVID-WeVerify: weverify.eu. Forensically: 29a.ch/photo-forensics. Gambar: Dennis S. Hurd (AI), CC BY 4.0.</p>

<!--
[klik 1] Satu gambar, tiga alat, tiga jawaban. [klik 2] Arti angka.
Kalimat kunci: jangan menulis di laporan "menurut aplikasi X, 87% palsu" sebagai satu-satunya dasar.
Detektor dipakai untuk memutuskan APA yang perlu diperiksa lebih dalam.
-->

---
bagian: Cara 4 · Konteks
clicks: 4
---

# Konteks (OSINT): <span class="biru">cara paling ampuh untuk hoaks sehari-hari</span>

<div style="margin-top:30px">
<JejakUnggahan />
</div>

<p class="sumber">Seluruh kasus di slide ini ilustrasi. Alat: Google Lens, TinEye, Yandex (cari balik); Google Maps/Street View; SunCalc. Rujukan cek fakta: turnbackhoax.id (Mafindo), cekfakta.com.</p>

<!--
[klik 1] Cari balik menemukan unggahan lebih lama. [klik 2] Sumber pertama: 2019, kota lain.
[klik 3] Geolokasi & kronolokasi. [klik 4] Kesimpulan: konteks dipelintir — tidak ada detektor AI yang menangkapnya.
Demo 2 menit (disarankan): ambil satu foto viral lama → Google Lens → ketemu unggahan aslinya.
-->

---
bagian: Alur kerja
clicks: 6
---

# Lima langkah sebelum menyimpulkan, <span class="biru">dari pesan masuk sampai laporan</span>

<div style="margin-top:22px">
<AlurVerifikasi />
</div>

<!--
[klik 1–5] Satu gerbang per klik. [klik 6] Cabang: bila akan jadi alat bukti → laboratorium forensik.
Ini bisa jadi draf SOP satuan — tawarkan untuk disusun bersama di sesi diskusi/praktik.
-->

---
bagian: Alur kerja
clicks: 3
---

# Jangan hanya “asli” atau “hoaks”: <span class="biru">tulis tingkat keyakinannya</span>

<div style="margin-top:30px">
<SkalaKeyakinan />
</div>

<!--
Kasus: video bodycam dari slide 7. Jarum bergeser setiap ada temuan baru.
[klik 1] Baru masuk: tidak dapat ditentukan — jawaban yang sah. [klik 2] Indikasi. [klik 3] Terbukti.
Menulis tingkat keyakinan melindungi dua arah: tidak gegabah menuduh, tidak gegabah membenarkan.
-->

---
bagian: Latihan antar-Polres
---

# Latihan antar-Polres: <span class="biru">tujuh konten, tebak dulu baru dibuka</span>

<div style="margin-top:30px">
<div class="baris" style="grid-template-columns:64px 1fr 1.3fr;border-top:none">
<span class="kartu" style="background:#0b7a6e" /><span class="nama">Kartu hijau: asli</span><span class="ket">Gambarnya asli, klaimnya juga benar.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.3fr">
<span class="kartu" style="background:#d99a00" /><span class="nama">Kartu kuning: asli, klaimnya salah</span><span class="ket">Gambarnya asli, tetapi waktu, tempat, atau ceritanya dipelintir.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.3fr">
<span class="kartu" style="background:#c0392b" /><span class="nama">Kartu merah: buatan AI</span><span class="ket">Dibuat atau diubah dengan AI.</span>
</div>
</div>

<p style="margin-top:28px;font-size:21px">Tiap Polres berunding <b>15 detik</b>, lalu angkat kartu bersamaan. Benar = 1 poin. <span class="redup">Yang dinilai bukan hanya jawabannya, tetapi <b>alasannya</b>.</span></p>

<!--
Peserta: perwakilan Polres se-Kaltim (maks. 150 orang). Satu tim = satu Polres; kalau satu Polres terlalu banyak orang, pecah jadi 2 tim.
Panitia menyiapkan 3 kartu (hijau/kuning/merah) per tim — seperti lampu lalu lintas, gampang diingat.
Skor dicatat panitia di papan/kertas. Setiap ronde: tunjuk 1–2 Polres yang jawabannya berbeda untuk menyebutkan alasannya.
Total ±18 menit (7 ronde × ±2,5 menit). Kalau waktu sempit: pakai ronde 1, 2, 4, 7 saja.
Pilihan lain: pecah jadi dua blok (ronde 1–3 setelah slide Mata, ronde 4–7 di sini) supaya suasana tetap cair.
Ronde 7 (suara) cukup kartu hijau dan merah.
-->

---
bagian: Latihan · Ronde 1/7
clicks: 6
---

# Ronde 1: <span class="biru">banjir di Samarinda, katanya pagi ini</span>

<div style="margin-top:18px">
<Ronde src="/latihan/banjir-2009.jpg" :tinggi="340" :rasio="1.333" jawab="klaim"
  klaim="Samarinda banjir lagi pagi ini, Lembuswana lumpuh! Hindari jalur ini."
  cara="Perbesar foto, lalu cari gambar serupa di Google Lens: sudah beredar sejak 2009."
  :titik="[
    { x: 69, y: 89, judul: 'Cap tanggal kamera: 2009/04/23 17:58', ket: 'Tercetak di foto. Tujuh belas tahun lalu, dan sore hari, bukan pagi.' },
    { x: 52, y: 9, judul: 'Baliho kepala daerah periode lama', ket: 'Wajah di baliho sudah lama tidak menjabat. Baliho = penanda zaman.' },
    { x: 22, y: 28, judul: 'Cahaya miring dari barat', ket: 'Gedung disinari matahari rendah: cocok untuk sore, bukan pagi.' },
    { judul: 'Data di dalam file', ket: 'File aslinya mencatat kamera Samsung S630, kamera saku tahun 2007.' },
  ]" />
</div>

<p class="sumber">Foto: Bloesafir Pamanjagau, “Banjir Lembuswana”, CC BY 3.0, Wikimedia Commons (Panoramio). Klaim di atas = rekaan untuk latihan.</p>

<!--
Biarkan peserta melihat ±15 detik, lalu hitung mundur, kartu diangkat. [klik 1] jawaban: KUNING.
[klik 2–5] petunjuk satu per satu. [klik 6] cara cek tercepat.
Pesan: ini tingkat 01 (konteks dipelintir) — tidak perlu alat canggih, cukup MATA YANG TELITI + pertanyaan "kapan?".
Banyak yang angkat hijau karena fotonya memang asli. Tekankan: fotonya asli, tapi klaimnya salah = tetap hoaks.
Jangan menyebut nama tokoh di baliho; cukup "kepala daerah periode lama".
-->

---
bagian: Latihan · Ronde 2/7
clicks: 5
---

# Ronde 2: <span class="biru">“waspada, pelaku hipnotis di swalayan”</span>

<div style="margin-top:18px">
<Ronde src="/latihan/wajah-ai.jpg" :tinggi="380" :rasio="0.6" jawab="ai"
  klaim="Waspada! Perempuan ini pelaku hipnotis di swalayan, korbannya sudah banyak. Sebarkan!"
  cara="Cari wajahnya di Google Lens. Tidak ada jejak orang ini di mana pun, dan tidak ada laporan polisi yang cocok."
  :titik="[
    { x: 84, y: 4, judul: 'Tulisan papan tidak terbaca', ket: 'Hurufnya mirip huruf, tapi bukan kata. AI masih sering gagal menulis teks di latar.' },
    { x: 30, y: 13, judul: 'Wajah dan kulit terlalu mulus', ket: 'Seperti foto model, padahal katanya foto “tangkapan” di swalayan.' },
    { x: 14, y: 42, judul: 'Rak dan kemasan tanpa merek jelas', ket: 'Kotak-kotak berulang, labelnya kabur. Swalayan sungguhan penuh merek yang terbaca.' },
  ]" />
</div>

<p class="sumber">Gambar: Benlisquare, dibuat dengan Stable Diffusion, “This AI-generated woman does not exist”, domain publik, Wikimedia Commons. Orang ini tidak pernah ada. Klaim = rekaan untuk latihan.</p>

<!--
[klik 1] MERAH. [klik 2–4] petunjuk. [klik 5] cara cek.
Pesan paling penting untuk polisi: hoaks "wajah pelaku" bisa memfitnah orang sungguhan kalau wajahnya mirip seseorang.
Jangan ikut meneruskan foto "DPO/pelaku" yang tidak berasal dari rilis resmi.
Catatan: model AI terbaru sudah bisa menulis teks rapi. Tanda di slide ini masih berguna, tapi bisa usang.
-->

---
bagian: Latihan · Ronde 3/7
clicks: 5
---

# Ronde 3: <span class="biru">video permukiman di Samarinda Utara</span>

<div style="margin-top:18px">
<Ronde video="/latihan/samarinda-asli.webm" src="/latihan/samarinda-asli.jpg" :tinggi="380" :rasio="0.556" jawab="asli"
  asal="video dari warga · dikirim langsung ke petugas"
  klaim="Ini kondisi lingkungan kami di Samarinda Utara, Mei 2026. Saya yang merekam."
  cara="Hubungi perekamnya, minta file asli dari HP-nya (kirim sebagai dokumen), cocokkan lokasinya."
  :titik="[
    { x: 80, y: 9, judul: 'Kamera goyang, berjalan apa adanya', ket: 'Gerak tangan manusia, fokus naik-turun, tidak ada sudut “sinematik”.' },
    { x: 55, y: 18, judul: 'Detail berantakan tapi konsisten', ket: 'Jemuran, kabel, pagar, motor: bentuknya tetap sama dari awal sampai akhir video.' },
    { judul: 'Perekamnya jelas dan bisa ditanya', ket: 'Ini petunjuk terkuat. Konten palsu jarang datang dengan pembuat yang mau dihubungi.' },
  ]" />
</div>

<p class="sumber">Video: Sri Wahyuni Nur Indah Sari, “Warunadwipa Timeline – Documentation at North Samarinda” (Mei 2026), CC BY-SA 3.0, Wikimedia Commons; orang di video setuju dipublikasikan.</p>

<!--
[klik 1] HIJAU. [klik 2–4] petunjuk. [klik 5] cara cek.
Pesan: kualitas jelek dan goyang BUKAN tanda palsu. Justru sering sebaliknya.
Ini juga contoh "tingkat keyakinan": tanpa file asli dan konfirmasi perekam, kita baru di "kemungkinan asli".
-->

---
bagian: Latihan · Ronde 4/7
clicks: 5
---

# Ronde 4: <span class="biru">papan Hollywood ikut terbakar</span>

<div style="margin-top:18px">
<Ronde src="/latihan/hollywood-ai.jpg" :tinggi="380" :rasio="1.335" jawab="ai"
  asal="unggahan viral · media sosial, Januari 2025"
  klaim="Papan HOLLYWOOD terbakar! Kebakaran Los Angeles makin tak terkendali."
  cara="Cek media dan pemadam kebakaran setempat. Saat itu mereka memastikan papan Hollywood tidak terbakar."
  :titik="[
    { x: 46, y: 30, judul: 'Huruf berlubang seperti jendela', ket: 'Papan aslinya huruf putih polos. AI “mengarang” rangka dan lubang.' },
    { x: 25, y: 58, judul: 'Api tersebar rata seperti lava', ket: 'Titik api merata di seluruh bukit, hampir tanpa asap tebal.' },
    { judul: 'Terlalu dramatis, terlalu pas', ket: 'Momen yang “sempurna untuk diviralkan” justru alasan untuk berhenti sejenak.' },
  ]" />
</div>

<p class="sumber">Gambar buatan AI yang viral saat kebakaran California, Jan 2025; pembuat tidak diketahui, domain publik, Wikimedia Commons.</p>

<!--
[klik 1] MERAH. [klik 2–4] petunjuk. [klik 5] cara cek.
Kaitkan ke Kaltim: saat musim karhutla atau banjir, pola yang sama bisa muncul — gambar AI "bencana" yang menimbulkan panik.
Bencana = saat orang paling cepat meneruskan, paling jarang memeriksa.
-->

---
bagian: Latihan · Ronde 5/7
clicks: 5
---

# Ronde 5: <span class="biru">rangkong di tepi sungai Kalimantan</span>

<div style="margin-top:18px">
<Ronde video="/latihan/borneo-sora.webm" src="/latihan/borneo-sora.jpg" :tinggi="350" :rasio="1.765" jawab="ai"
  asal="video viral · media sosial"
  klaim="Kawanan rangkong muncul di tepi Sungai Mahakam! Direkam warga pagi tadi."
  cara="Putar pelan dan lihat pojok-pojok video, lalu cari potongan gambarnya di Google Lens."
  :titik="[
    { x: 89, y: 87, judul: 'Watermark samar di pojok', ket: 'Logo pembuat video AI. Mudah dipotong, jadi kalau tidak ada pun belum tentu asli.' },
    { x: 62, y: 46, judul: 'Burung terlalu mulus, gerak kaku', ket: 'Bulu seperti mainan; burung menoleh bersamaan seperti boneka.' },
    { judul: 'Lokasinya pun bukan Mahakam', ket: 'Perintah teksnya: “satwa Kalimantan di Sungai Kinabatangan” (Sabah, Malaysia).' },
  ]" />
</div>

<p class="sumber">Video: dibuat dengan Sora (OpenAI) dari perintah teks “Borneo wildlife on the Kinabatangan River”, 8 detik, domain publik, Wikimedia Commons.</p>

<!--
[klik 1] MERAH. [klik 2–4] petunjuk. [klik 5] cara cek.
Ini contoh yang "tidak berbahaya" — tapi itulah intinya: konten AI yang tampak lucu atau indah membiasakan orang percaya tanpa memeriksa.
Bandingkan dengan ronde 3: video asli goyang & berantakan, video AI mulus & sinematik.
-->

---
bagian: Latihan · Ronde 6/7
clicks: 5
---

# Ronde 6: <span class="biru">banjir di Samarinda, katanya sore ini</span>

<div style="margin-top:18px">
<Ronde src="/latihan/banjir-2026.jpg" :tinggi="380" :rasio="0.75" jawab="asli"
  klaim="Banjir di jalan depan Pegadaian sore ini, 22 Mei 2026. Hati-hati yang lewat."
  cara="Minta file asli dari pengirim, cocokkan lokasi di Google Maps, dan cocokkan dengan laporan BPBD hari itu."
  :titik="[
    { x: 82, y: 38, judul: 'Papan nama dan toko yang bisa dicek', ket: 'Pegadaian, toko motor, nomor telepon: semuanya bisa dicocokkan dengan lokasi sebenarnya.' },
    { x: 45, y: 62, judul: 'Hujan, arus, dan cipratan konsisten', ket: 'Air keruh mengalir searah, roda mobil menembus genangan secara wajar.' },
    { judul: 'File asli menyimpan waktu ambil', ket: 'Data di file pengunggah: 22 Mei 2026, pukul 17.08. Cocok dengan klaim “sore ini”.' },
  ]" />
</div>

<p class="sumber">Foto: Bernadetta Alice Caroline, “Banjir Samarinda (4)”, 22 Mei 2026, CC BY-SA 4.0, Wikimedia Commons. Klaim = rekaan untuk latihan.</p>

<!--
[klik 1] HIJAU. [klik 2–4] petunjuk. [klik 5] cara cek.
Ronde penutup sengaja yang ASLI: setelah lima ronde, peserta cenderung curiga pada semua hal.
Pesan: curiga itu baik, tapi menyebut konten asli sebagai "hoaks/AI" juga kesalahan — dan bisa merugikan pelapor yang jujur.
Masih ada satu ronde lagi — ronde suara.
-->

---
bagian: Latihan · Ronde 7/7
clicks: 5
---

# Ronde 7: <span class="biru">mana suara saya yang asli?</span>

<div style="margin-top:18px">
<RondeSuara
  klaim="Tiga pesan suara masuk atas nama Aidil Saputra Kirsan. Semuanya terdengar seperti saya."
  :item="[
    { src: '/latihan/suara-a.m4a', jawab: 'ai', isi: 'minta transfer, katanya di bandara dan HP mau mati' },
    { src: '/latihan/suara-b.m4a', jawab: 'asli', isi: 'titip cek email, minta ditelepon nanti malam' },
    { src: '/latihan/suara-c.m4a', jawab: 'ai', isi: 'minta kode OTP yang “salah kirim”' },
  ]"
  cara="Tutup, lalu telepon balik ke nomor lama yang sudah Bapak/Ibu simpan. Atau tanyakan hal yang hanya orang itu yang tahu."
  :titik="[
    { judul: 'Suaranya tidak bisa jadi pegangan', ket: 'Logat, jeda, dan napas bisa ditiru. Kloning ini dibuat dari rekaman suara saya sendiri.' },
    { judul: 'Isi pesannya yang membongkar', ket: 'Mendesak, minta uang atau kode OTP, dan “jangan telepon dulu”. Itu pola penipuan, siapa pun suaranya.' },
    { judul: 'Nomor baru, alasan klasik', ket: 'HP rusak, baterai habis, ganti nomor: alasan supaya korban tidak menelepon nomor lama.' },
  ]" />
</div>

<p class="sumber">Klip A dan C dibuat dengan kloning suara ElevenLabs dari suara pembicara sendiri, dengan izin pemilik suara. Klip B = rekaman asli. Naskah = rekaan untuk latihan; nomor, rekening, dan nama lain tidak ada.</p>

<!--
Cara main: putar A, B, C bergantian (klik tombol ▶ di tiap klip, bukan tombol maju slide).
Setelah tiap klip, Polres angkat kartu: hijau = suara asli saya, merah = kloning AI.
[klik 1–3] petunjuk (umum, belum membocorkan jawaban). [klik 4] cara cek. [klik 5] BARU jawaban A/B/C terbuka.
Pastikan semua Polres sudah angkat kartu untuk ketiga klip sebelum klik 1.

Kalimat puncak: "Dari tadi Bapak/Ibu mendengar suara asli saya langsung di ruangan ini. Dan tetap tertipu.
Klon ini cukup dibuat dari [ISI: berapa lama rekaman yang dipakai untuk klon] rekaman suara saya."
Lalu hubungkan ke slide 5: "Modus yang sama, dengan suara dan wajah Presiden, sudah ditangani Bareskrim tahun 2025."

Pesan untuk masyarakat (Bhabinkamtibmas bisa pakai): sepakati "kata sandi keluarga" untuk permintaan uang lewat telepon.
Jangan pernah membuat klon suara orang lain tanpa izin — termasuk untuk demo.
Umumkan skor akhir per Polres, beri apresiasi.
-->

---
layout: center
class: malam
bagian: Latihan antar-Polres
---

<div style="max-width:1020px">
<h1 style="font-size:56px">Yang membongkar hoaks bukan mata yang paling tajam.</h1>
<h1 style="font-size:56px;margin-top:14px" class="biru">Tetapi pertanyaan yang tepat: <span v-mark="{ at: 1, type: 'underline', color: '#0b7a6e', strokeWidth: 4 }">kapan, di mana, siapa yang pertama</span>.</h1>
<p v-click="2" class="mono redup" style="font-size:18px;margin-top:40px">cap tanggal · wajah tanpa jejak · perekam bisa ditanya · file asli · telepon balik</p>
</div>

<!--
Rangkum: dari enam ronde, hanya sebagian yang bisa dijawab dengan mata.
Yang paling menentukan justru asal-usul dan konteks — persis tabel perbandingan tadi.
-->

---
layout: center
class: malam
bagian: Bahaya sebaliknya
---

<div style="max-width:1060px">
<h1 style="font-size:56px">Bahaya baru: bukti asli <span class="merah">disangkal sebagai “itu AI”</span></h1>

<div class="dua-arah">
<div v-click><span class="label-kolom">video palsu</span><span class="panah-teks" /><span>dipercaya sebagai asli</span></div>
<div v-click><span class="label-kolom">video asli</span><span class="panah-teks merah" /><span><b>“itu cuma AI”</b> — bukti disangkal</span></div>
</div>

<p v-click style="font-size:21px;margin-top:34px;max-width:900px">Peneliti hukum menyebutnya <i>liar’s dividend</i>. Karena itu verifikasi bukan hanya untuk membongkar yang palsu, tetapi untuk <b>mempertahankan yang asli</b> — rekaman bodycam dan CCTV perlu dijaga asal-usulnya sejak awal.</p>
</div>

<p class="sumber">Chesney &amp; Citron, California Law Review 107 (2019). Europol Innovation Lab, “Facing reality? Law enforcement and the challenge of deepfakes” (2022, diperbarui 2024): deepfake dapat dipakai untuk memalsukan maupun meragukan bukti di persidangan.</p>

<!--
Sering jadi poin "aha" untuk aparat: deepfake bukan cuma soal hoaks, tapi soal pembuktian di pengadilan.
-->

---
bagian: Hukum & pembuktian
clicks: 3
---

# Dari temuan ke alat bukti: <span class="biru">rantai yang dijaga sejak awal</span>

<div style="margin-top:40px">
<RantaiBukti />
</div>

<p class="mono redup" style="font-size:14px;margin-top:30px">dasar hukum untuk diskusi: UU ITE (UU 11/2008 jo. UU 1/2024) Ps. 5 — informasi elektronik sebagai alat bukti · Ps. 35 — manipulasi agar seolah otentik · Ps. 28 ayat 3 — pemberitahuan bohong yang menimbulkan kerusuhan · KUHP baru (UU 1/2023), berlaku 2 Januari 2026</p>

<p class="sumber">Hash = SHA-256 nyata dari file kuis D dan salinannya yang diubah 1 byte. Teks pasal: rujuk JDIH; penafsiran oleh ahli hukum — DRAF, minta masukan panitia.</p>

<!--
[klik 1] Rantai. [klik 2] Sidik jari file asli. [klik 3] Ubah satu byte → hash berubah total.
Hash membuktikan file tidak diutak-atik sejak diamankan.
Saya bukan ahli hukum: bagian pasal saya sampaikan sebagai pengantar, lalu serahkan ke penyidik yang lebih paham.
Usulkan ke panitia: adakah narasumber Ditressiber/Labfor untuk bagian ini?
-->

---
bagian: Praktik
---

# Praktik 15 menit: <span class="biru">periksa tiga konten bersama</span>

<div style="margin-top:30px">
<div class="baris" style="grid-template-columns:64px 1fr 1.1fr;border-top:none">
<span class="no">01</span><span class="nama">Foto lama, klaim baru</span><span class="ket">Google Lens → temukan unggahan pertama, cocokkan lokasi.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.1fr">
<span class="no">02</span><span class="nama">Gambar buatan AI</span><span class="ket">Periksa visual, lalu bandingkan dua detektor.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.1fr">
<span class="no">03</span><span class="nama">Foto asli dengan metadata</span><span class="ket">Baca EXIF, cocokkan waktu dan tempat.</span>
</div>
</div>

<p style="margin-top:28px;font-size:20px">Tiap kelompok mengisi <b>lembar verifikasi</b>: lima langkah + tingkat keyakinan. <span class="redup">Peserta daring: versi Google Form.</span></p>

<!--
OPSIONAL — tergantung durasi & format dari panitia. Bisa diganti demo langsung oleh pembicara.
Semua kasus dibuat/dipilih sendiri: tanpa korban nyata, tanpa wajah anggota Polri atau tokoh nyata.
-->

---
bagian: Rekomendasi
---

# Tiga hal yang bisa dimulai <span class="biru">minggu ini</span>

<div style="margin-top:34px">
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr;border-top:none" v-click>
<span class="no">01</span><span class="nama">Satu alur verifikasi tertulis</span><span class="ket">Lima langkah + tingkat keyakinan, satu halaman, dipakai semua yang menangani laporan konten.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr" v-click>
<span class="no">02</span><span class="nama">Kebiasaan “amankan dulu”</span><span class="ket">File asli, tautan, tangkapan layar, dan hash — sebelum konten dihapus pengunggahnya.</span>
</div>
<div class="baris" style="grid-template-columns:64px 1fr 1.2fr" v-click>
<span class="no">03</span><span class="nama">Jejaring verifikasi</span><span class="ket">Kanal cepat dengan pemeriksa fakta, Komdigi, dan kampus untuk kasus yang perlu analisis lebih dalam.</span>
</div>
</div>

<!--
Kampus (ITK) bisa membantu di nomor 3: pelatihan lanjutan, riset alat deteksi untuk konteks lokal.
Sampaikan sebagai tawaran, bukan jualan.
-->

---
layout: center
class: malam
bagian: Penutup
---

<div style="max-width:1020px">
<h1 style="font-size:64px">Membuat konten palsu sudah murah.</h1>
<h1 style="font-size:64px;margin-top:12px" class="biru">Yang mahal adalah kebiasaan <span v-mark="{ at: 1, type: 'underline', color: '#0b7a6e', strokeWidth: 4 }">memeriksa sebelum percaya</span>.</h1>

<div class="grid gap-12" style="grid-template-columns: 1fr 1fr; margin-top:60px; align-items:center">
<div>
<p class="label-kolom">kontak</p>
<p style="margin-top:6px">aidil@lecturer.itk.ac.id · 085398952880</p>
</div>
<div class="ikuti">
<img src="/qr-instagram.svg" alt="QR ke Instagram @aidilsaputrakirsan">
<div><p><b>Konten edukasi AI</b> <span class="mono aksen">@aidilsaputrakirsan</span></p><p class="redup">Instagram · pindai dengan kamera HP</p></div>
</div>
</div>
</div>

<!--
Kalimat penutup. Lalu tanya jawab.
-->

---
bagian: Referensi
---

# Sumber

<div style="margin-top:28px;font-size:16.5px">

- Nightingale, S. J., &amp; Farid, H. (2022). AI-synthesized faces are indistinguishable from real faces and more trustworthy. *PNAS*, 119(8).
- iProov (Feb 2025). Studi “deepfake blindspot” — 2.000 responden Inggris &amp; AS (studi vendor).
- Bisnis.com (7 Feb 2025); detik.com — penangkapan dan analisis forensik video deepfake Presiden oleh Dittipidsiber Bareskrim. Bisnis.com (23 Okt 2025) — Komdigi.
- Europol Innovation Lab (2022, diperbarui 2024). *Facing reality? Law enforcement and the challenge of deepfakes*.
- INTERPOL (Juni 2024). *Beyond Illusions: Unmasking the Threat of Synthetic Media for Law Enforcement*.
- Chesney, R., &amp; Citron, D. (2019). Deep Fakes: A Looming Challenge for Privacy, Democracy, and National Security. *California Law Review*, 107.
- C2PA / Content Credentials; InVID-WeVerify; Forensically. UU 11/2008 jo. UU 19/2016 jo. UU 1/2024 tentang ITE; UU 1/2023 tentang KUHP.
- Gambar &amp; video contoh: Wikimedia Commons (domain publik, CC0, CC BY 4.0, CC BY-SA 4.0); kredit di tiap slide.

</div>

<p class="sumber">DRAF — angka dari liputan media akan dicek ulang ke sumber primer sebelum acara.</p>
