<script setup>
// Empat tingkat rekayasa di satu garis: dari "foto asli, cerita salah" sampai "tidak pernah ada kamera".
// Per klik (frontmatter `clicks: 5`): 1–4 = tingkat ke-n muncul · 5 = dua kurung di bawah: cara memeriksa
// untuk 01–02 (konteks & asal-usul) vs 03–04 (detektor AI bisa membantu). Ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const tingkat = [
  { nama: 'Konteks dipelintir', ket: 'Gambarnya asli. Waktu, tempat, atau ceritanya salah.', contoh: 'Foto banjir lama disebut “pagi ini”.', warna: '#a86b00' },
  { nama: 'Dipotong & disunting', ket: 'Bagian dihapus, diperlambat, diberi teks atau suara.', contoh: 'Pidato dipotong sampai maknanya berbalik.', warna: '#b9531f' },
  { nama: 'Diubah dengan AI', ket: 'Wajah ditukar, bibir disinkronkan, suara dikloning.', contoh: 'Video resmi pejabat, mulut & suara diganti.', warna: '#c0392b' },
  { nama: 'Dibuat penuh oleh AI', ket: 'Tidak pernah ada kamera. Semua dari perintah teks.', contoh: 'Rekaman “kejadian” yang tidak pernah terjadi.', warna: '#8e2a20' },
]
const W = 1120, Y = 40
const X = tingkat.map((_, i) => (W / 4) * (i + 0.5))
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" height="70" :viewBox="`0 0 ${W} 70`" fill="none" stroke-linecap="round" aria-hidden="true">
      <line x1="8" :x2="W - 18" :y1="Y" :y2="Y" stroke="#cbd0d9" stroke-width="2" />
      <path :d="`M${W - 26} ${Y - 7} L${W - 16} ${Y} L${W - 26} ${Y + 7}`" stroke="#cbd0d9" stroke-width="2" />
      <text x="8" y="14" fill="#0b7a6e" style="font-size:13px;font-family:'JetBrains Mono'">gambar asli</text>
      <text :x="W - 16" y="14" text-anchor="end" fill="#8e2a20" style="font-size:13px;font-family:'JetBrains Mono'">tidak pernah ada kamera</text>
      <g v-for="(t, i) in tingkat" :key="i" class="muncul" :class="{ ya: k > i }">
        <circle :cx="X[i]" :cy="Y" r="17" fill="#fff" :stroke="t.warna" stroke-width="3" />
        <text :x="X[i]" :y="Y + 5" text-anchor="middle" :fill="t.warna" style="font-size:13px;font-weight:800;font-family:'JetBrains Mono'">0{{ i + 1 }}</text>
      </g>
    </svg>

    <div class="empat">
      <div v-for="(t, i) in tingkat" :key="i" class="muncul-html" :class="{ ya: k > i }">
        <p class="nama" :style="{ color: t.warna }">{{ t.nama }}</p>
        <p class="ket">{{ t.ket }}</p>
        <p class="contoh">{{ t.contoh }}</p>
      </div>
    </div>

    <div class="kurung muncul-html" :class="{ ya: k >= 5 }">
      <div><span class="garis" /><p>Detektor AI <b>tidak menangkapnya</b> — gambarnya memang asli. Alatnya: <b>konteks &amp; asal-usul</b>.</p></div>
      <div><span class="garis" /><p>Di sini <b>detektor AI bisa membantu</b>, tetapi tetap bukan vonis.</p></div>
    </div>
  </div>
</template>

<style scoped>
.muncul { opacity: 0; transition: opacity .4s ease; }
.muncul.ya { opacity: 1; }
.empat { display: grid; grid-template-columns: repeat(4, 1fr); text-align: center; }
.empat > div { padding: 0 18px; }
.empat p { margin: 0; }
.nama { font-weight: 800; font-size: 22px; line-height: 1.15; letter-spacing: -0.015em; margin-top: 4px !important; }
.ket { font-size: 16px; line-height: 1.4; color: #10131a; margin-top: 8px !important; }
.contoh { font-size: 14.5px; line-height: 1.4; color: #4a5160; margin-top: 8px !important; font-style: italic; }
.kurung { display: grid; grid-template-columns: 1fr 1fr; margin-top: 28px; }
.kurung > div { padding: 0 24px; text-align: center; }
.kurung .garis { display: block; height: 14px; border: 2px solid #10131a; border-top: none; border-radius: 0 0 10px 10px; margin: 0 6px 12px; }
.kurung > div:last-child .garis { border-color: #c0392b; }
.kurung p { margin: 0; font-size: 18px; line-height: 1.4; }
.muncul-html { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.muncul-html.ya { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) { .muncul, .muncul-html { transition: none; } }
</style>
