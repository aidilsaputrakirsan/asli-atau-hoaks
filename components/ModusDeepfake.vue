<script setup>
// Modus penipuan deepfake Presiden (kasus Bareskrim, Jan–Feb 2025) sebagai alur lima langkah.
// Per klik (frontmatter `clicks: 5`): langkah ke-n muncul, garis tergambar. Ekspor: semua tampil.
// Fakta dari liputan media (Bisnis.com 7 Feb 2025; detik.com) — lihat CLAUDE.md.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const langkah = [
  { judul: 'Video resmi pejabat', ket: 'diunduh dari akun media sosial', ikon: 'video' },
  { judul: 'Wajah & suara diganti', ket: 'mulut dan isi ucapan dibuat AI', ikon: 'ai' },
  { judul: 'Disebar + nomor WA', ket: '“Bapak/Ibu terpilih menerima bantuan…”', ikon: 'sebar' },
  { judul: 'Korban mentransfer', ket: '“biaya administrasi” untuk bantuan', ikon: 'uang' },
  { judul: 'Ditangkap', ket: 'Dittipidsiber Bareskrim, Jan–Feb 2025; forensik: video palsu', ikon: 'tangkap' },
]
const W = 1120, Y = 46, R = 30
const X = langkah.map((_, i) => (W / 5) * (i + 0.5))
const pj = X[4] - X[0]
const maju = computed(() => (k.value <= 1 ? 0 : X[Math.min(k.value, 5) - 1] - X[0]))
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + R + 6" :viewBox="`0 0 ${W} ${Y + R + 6}`" fill="none" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <line :x1="X[0]" :x2="X[4]" :y1="Y" :y2="Y" stroke="#e1e4ea" stroke-width="2" stroke-dasharray="3 7" />
      <line :x1="X[0]" :x2="X[4]" :y1="Y" :y2="Y" :stroke="k >= 5 ? '#0b7a6e' : '#c0392b'" stroke-width="3" class="maju" :style="{ strokeDasharray: pj, strokeDashoffset: pj - maju }" />
      <g v-for="(l, i) in langkah" :key="i" class="muncul" :class="{ ya: k > i }">
        <circle :cx="X[i]" :cy="Y" :r="R" fill="#fff" :stroke="i === 4 ? '#0b7a6e' : '#10131a'" stroke-width="2" />
        <g :stroke="i === 4 ? '#0b7a6e' : '#10131a'" stroke-width="2.2" :transform="`translate(${X[i] - 12} ${Y - 12})`">
          <template v-if="l.ikon === 'video'"><rect x="0" y="4" width="17" height="16" rx="3" /><path d="M17 10l7-4v12l-7-4" /></template>
          <template v-else-if="l.ikon === 'ai'"><circle cx="12" cy="9" r="6" /><path d="M3 24c1-6 5-8 9-8s8 2 9 8" /><path d="M2 3l20 18" stroke="#c0392b" /></template>
          <template v-else-if="l.ikon === 'sebar'"><path d="M2 20l4-4h14a2 2 0 002-2V4a2 2 0 00-2-2H4a2 2 0 00-2 2z" /><path d="M7 8h10M7 12h6" /></template>
          <template v-else-if="l.ikon === 'uang'"><rect x="0" y="5" width="24" height="15" rx="3" /><circle cx="12" cy="12.5" r="3.5" fill="#c0392b" stroke="#c0392b" /></template>
          <template v-else><path d="M4 12l6 6L21 5" /></template>
        </g>
      </g>
    </svg>
    <div class="teks">
      <div v-for="(l, i) in langkah" :key="i" class="muncul-html" :class="{ ya: k > i }">
        <p class="no">0{{ i + 1 }}</p>
        <p class="judul">{{ l.judul }}</p>
        <p class="ket">{{ l.ket }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.maju { transition: stroke-dashoffset .7s cubic-bezier(.45,.05,.25,1), stroke .4s ease; }
.muncul { opacity: 0; transition: opacity .4s ease; }
.muncul.ya { opacity: 1; }
.teks { display: grid; grid-template-columns: repeat(5, 1fr); margin-top: 14px; text-align: center; }
.teks > div { padding: 0 12px; }
.teks p { margin: 0; }
.no { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190; }
.judul { font-weight: 800; font-size: 19px; line-height: 1.2; letter-spacing: -0.01em; margin-top: 4px !important; color: #10131a; }
.ket { font-size: 15px; line-height: 1.4; color: #4a5160; margin-top: 6px !important; }
.muncul-html { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.muncul-html.ya { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) { .maju, .muncul, .muncul-html { transition: none; } }
</style>
