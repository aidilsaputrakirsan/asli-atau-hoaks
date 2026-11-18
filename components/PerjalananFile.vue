<script setup>
// Asal-usul file: apa yang tersisa dari jejak sebuah foto saat ia berpindah tangan.
// Pola chip-dicoret dari AlurData (SIMFONI). Per klik (frontmatter `clicks: 3`):
// 1 = di kamera (semua jejak ada) · 2 = setelah WhatsApp biasa (metadata & label umumnya hilang)
// 3 = setelah di-screenshot/unggah ulang (watermark mungkin rusak). Ekspor: semua tampil.
// Perilaku platform bisa berubah per versi — ditulis "umumnya".
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const jejak = [
  { nama: 'merek & tipe HP', lapis: 'exif' }, { nama: 'waktu ambil', lapis: 'exif' }, { nama: 'lokasi GPS', lapis: 'exif' },
  { nama: 'Content Credentials', lapis: 'c2pa' }, { nama: 'watermark tak terlihat', lapis: 'wm' },
]
const tahap = [
  { label: 'di kamera / aplikasi pembuat', hilang: [], ragu: [], ket: 'Jejak lengkap: dibuat kapan, dengan apa, kadang di mana.' },
  { label: 'dikirim biasa lewat WhatsApp', hilang: ['exif', 'c2pa'], ragu: [], ket: 'Dikompres ulang: metadata dan label umumnya hilang. Watermark di piksel masih bisa terbaca.' },
  { label: 'di-screenshot, diunggah ulang', hilang: ['exif', 'c2pa'], ragu: ['wm'], ket: 'Tinggal pikselnya. Watermark mungkin masih ada, mungkin rusak.' },
]
</script>

<template>
  <div class="perjalanan">
    <template v-for="(t, i) in tahap" :key="i">
      <span v-if="i > 0" class="panah" :class="{ ya: k > i }" aria-hidden="true" />
      <section :class="{ ya: k > i }">
        <p class="tahap">{{ t.label }}</p>
        <div class="chips">
          <span v-for="j in jejak" :key="j.nama" class="chip" :class="[j.lapis, { hilang: t.hilang.includes(j.lapis), ragu: t.ragu.includes(j.lapis) }]">{{ j.nama }}</span>
        </div>
        <p class="ket">{{ t.ket }}</p>
      </section>
    </template>
  </div>
</template>

<style scoped>
.perjalanan { display: grid; grid-template-columns: 1fr 44px 1fr 44px 1fr; align-items: start; column-gap: 6px; }
section { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
section.ya { opacity: 1; transform: none; }
section p { margin: 0; }
.tahap { font-family: 'JetBrains Mono', monospace; font-size: 14px; color: #0b7a6e; margin-bottom: 14px !important; }
.chips { display: flex; flex-direction: column; align-items: flex-start; gap: 9px; }
.chip { font-size: 17px; line-height: 1; padding: 9px 14px; border-radius: 999px; border: 1px solid #10131a; color: #10131a; white-space: nowrap; background: #fff; transition: all .5s ease; }
.chip.c2pa { border-color: #1f62d6; color: #1f62d6; }
.chip.wm { border-color: #0b7a6e; color: #0b7a6e; }
.chip.hilang { color: #9aa1ad; border-color: #cbd0d9; border-style: dashed; text-decoration: line-through; background: transparent; }
.chip.ragu { border-style: dashed; color: #a86b00; border-color: #a86b00; }
.ket { font-size: 16px; line-height: 1.45; color: #4a5160; margin-top: 16px !important; }
.panah { position: relative; height: 210px; margin-top: 30px; opacity: 0; transition: opacity .4s ease; }
.panah.ya { opacity: 1; }
.panah::before { content: ''; position: absolute; left: 4px; right: 8px; top: 50%; border-top: 2px solid #10131a; }
.panah::after { content: ''; position: absolute; right: 4px; top: calc(50% - 5px); border: solid #10131a; border-width: 0 2px 2px 0; padding: 4px; transform: rotate(-45deg); }
@media (prefers-reduced-motion: reduce) { section, .panah, .chip { transition: none; } }
</style>
