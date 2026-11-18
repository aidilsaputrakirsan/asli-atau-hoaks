<script setup>
// Perbandingan empat cara memeriksa — PETA, bukan tabel.
// Sumbu x: cepat dilakukan ← → butuh waktu & keahlian. Sumbu y: lemah ↓ ↑ kuat sebagai dasar tindakan.
// Posisi = penilaian kualitatif (bukan data terukur). Per klik (frontmatter `clicks: 5`):
// 1–4 = cara ke-n muncul + panel fokus (kuat untuk / titik buta) · 5 = garis "gabungkan" menghubungkan semua.
// Ekspor: semua titik + daftar ringkas.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const cetak = computed(() => isPrintMode.value)
const k = computed(() => (cetak.value ? 99 : $clicks.value))

const cara = [
  { nama: 'Mata', x: 0.1, y: 0.16, kuat: 'Menyaring awal, dalam hitungan detik.', buta: 'Model baru makin rapi; akurasi manusia di sekitar lempar koin.' },
  { nama: 'Alat deteksi AI', x: 0.34, y: 0.42, kuat: 'Gambar yang diubah atau dibuat AI (tingkat 03–04).', buta: 'Bisa salah menuduh dan bisa kecolongan; hasil antaralat sering berbeda.' },
  { nama: 'Asal-usul file', x: 0.5, y: 0.88, y2: 0.24, dx: 0, dy: -20, anchor: 'middle', kuat: 'Membuktikan dari mana file berasal — bila jejaknya masih ada.', buta: 'Metadata dan label umumnya hilang saat dikirim lewat WA/medsos.' },
  { nama: 'Konteks (OSINT)', x: 0.84, y: 0.8, dx: 0, dy: 34, anchor: 'middle', kuat: 'Hoaks sehari-hari: foto lama, tempat lain, cerita dipelintir.', buta: 'Butuh waktu, ketekunan, dan latihan.' },
]
const W = 560, H = 380, pad = 36
const px = (v) => pad + v * (W - pad * 2)
const py = (v) => H - pad - v * (H - pad * 2)
const fokus = computed(() => (k.value >= 1 && k.value <= 4 ? cara[k.value - 1] : null))
const hubung = `M${px(0.1)} ${py(0.16)} L${px(0.34)} ${py(0.42)} L${px(0.5)} ${py(0.88)} L${px(0.84)} ${py(0.8)}`
</script>

<template>
  <div class="lensa">
    <svg :width="W" :height="H" :viewBox="`0 0 ${W} ${H}`" fill="none" stroke-linecap="round" aria-hidden="true">
      <line :x1="pad" :x2="W - 10" :y1="H - pad" :y2="H - pad" stroke="#cbd0d9" stroke-width="2" />
      <line :x1="pad" :x2="pad" :y1="H - pad" y2="8" stroke="#cbd0d9" stroke-width="2" />
      <path :d="`M${W - 18} ${H - pad - 6} L${W - 10} ${H - pad} L${W - 18} ${H - pad + 6}`" stroke="#cbd0d9" stroke-width="2" />
      <path :d="`M${pad - 6} 16 L${pad} 8 L${pad + 6} 16`" stroke="#cbd0d9" stroke-width="2" />
      <text :x="pad" :y="H - 8" fill="#7b8190" style="font-size:13px;font-family:'JetBrains Mono'">cepat</text>
      <text :x="W - 10" :y="H - 8" text-anchor="end" fill="#7b8190" style="font-size:13px;font-family:'JetBrains Mono'">butuh waktu &amp; keahlian</text>
      <text :x="pad + 12" y="20" fill="#7b8190" style="font-size:13px;font-family:'JetBrains Mono'">kuat sebagai dasar tindakan</text>

      <path :d="hubung" stroke="#1f62d6" stroke-width="2.5" stroke-dasharray="6 7" class="muncul" :class="{ ya: k >= 5 }" />

      <g v-for="(c, i) in cara" :key="c.nama" class="muncul" :class="{ ya: k > i, redup: fokus && fokus !== c }">
        <line v-if="c.y2" :x1="px(c.x)" :x2="px(c.x)" :y1="py(c.y)" :y2="py(c.y2)" stroke="#0b7a6e" stroke-width="2" stroke-dasharray="3 5" />
        <circle v-if="c.y2" :cx="px(c.x)" :cy="py(c.y2)" r="7" fill="#fff" stroke="#0b7a6e" stroke-width="2" stroke-dasharray="3 3" />
        <circle :cx="px(c.x)" :cy="py(c.y)" r="11" :fill="fokus === c ? '#1f62d6' : '#10131a'" />
        <text :x="px(c.x) + (c.dx ?? 18)" :y="py(c.y) + (c.dy ?? 6)" :text-anchor="c.anchor || 'start'" fill="#10131a"
              style="font-size:17px;font-weight:800;font-family:'Plus Jakarta Sans'">{{ c.nama }}</text>
        <text v-if="c.y2" :x="px(c.x) + 16" :y="py(c.y2) + 5" fill="#0b7a6e" style="font-size:13px;font-family:'JetBrains Mono'">bila jejaknya hilang</text>
      </g>
    </svg>

    <div v-if="!cetak" class="fokus">
      <Transition name="ganti" mode="out-in">
        <div v-if="k >= 5" key="akhir">
          <p class="besar">Tidak ada satu cara yang cukup.</p>
          <p class="isi"><span class="biru">Kesimpulan yang kuat</span> datang dari beberapa cara yang saling menguatkan — terutama asal-usul dan konteks.</p>
        </div>
        <div v-else-if="fokus" :key="fokus.nama">
          <p class="nama">{{ fokus.nama }}</p>
          <p class="label">kuat untuk</p><p class="isi">{{ fokus.kuat }}</p>
          <p class="label merah">titik buta</p><p class="isi">{{ fokus.buta }}</p>
        </div>
      </Transition>
    </div>
    <div v-else class="ringkas">
      <div v-for="c in cara" :key="c.nama"><b>{{ c.nama }}</b><span>{{ c.kuat }} <i>Titik buta:</i> {{ c.buta }}</span></div>
    </div>
  </div>
</template>

<style scoped>
.lensa { display: grid; grid-template-columns: 560px 1fr; gap: 48px; align-items: center; }
.muncul { opacity: 0; transition: opacity .45s ease; }
.muncul.ya { opacity: 1; }
.muncul.ya.redup { opacity: .3; }
.fokus { min-height: 300px; display: flex; align-items: center; border-left: 1px solid #e1e4ea; padding-left: 36px; }
.fokus p { margin: 0; }
.nama { font-weight: 800; font-size: 40px; line-height: 1.05; letter-spacing: -0.03em; color: #1f62d6; margin-bottom: 18px !important; }
.label { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #0b7a6e; margin-top: 14px !important; }
.label.merah { color: #c0392b; }
.isi { font-size: 21px; line-height: 1.4; color: #10131a; margin-top: 4px !important; }
.besar { font-weight: 800; font-size: 34px; line-height: 1.15; letter-spacing: -0.02em; margin-bottom: 14px !important; }
.biru { color: #1f62d6; font-weight: 700; }
.ganti-enter-active, .ganti-leave-active { transition: opacity .25s ease, transform .3s cubic-bezier(.2,.7,.2,1); }
.ganti-enter-from { opacity: 0; transform: translateY(12px); }
.ganti-leave-to { opacity: 0; transform: translateY(-8px); }
.ringkas > div { display: grid; grid-template-columns: 150px 1fr; gap: 12px; padding: 9px 0; border-bottom: 1px solid #e1e4ea; font-size: 15px; line-height: 1.4; }
.ringkas span { color: #4a5160; }
@media (prefers-reduced-motion: reduce) { .muncul, .ganti-enter-active, .ganti-leave-active { transition: none; } }
</style>
