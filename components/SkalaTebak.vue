<script setup>
// Akurasi manusia membedakan wajah asli vs AI, di atas skala 0–100% dengan penanda "lempar koin" (50%).
// Per klik (frontmatter `clicks: 3`): 1 = 48% tanpa latihan · 2 = 59% setelah dilatih · 3 = iProov 0,1%.
// Sumber: Nightingale & Farid, PNAS 2022; iProov 2025. Ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const W = 1120, Y = 120, x0 = 30, x1 = W - 30
const X = (p) => x0 + (p / 100) * (x1 - x0)
const titik = [
  { p: 48, label: '48%', ket: 'menebak tanpa latihan', n: 1 },
  { p: 59, label: '59%', ket: 'setelah dilatih & diberi umpan balik', n: 2 },
]
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + 50" :viewBox="`0 0 ${W} ${Y + 50}`" fill="none" aria-hidden="true">
      <!-- zona "lebih buruk dari koin" -->
      <rect :x="x0" :y="Y - 8" :width="X(50) - x0" height="16" rx="8" fill="#eef0f4" />
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#cbd0d9" stroke-width="2" />
      <g v-for="t in [0, 25, 50, 75, 100]" :key="t">
        <line :x1="X(t)" :x2="X(t)" :y1="Y + 10" :y2="Y + 18" stroke="#cbd0d9" stroke-width="2" />
        <text :x="X(t)" :y="Y + 40" text-anchor="middle" fill="#7b8190" style="font-size:14px;font-family:'JetBrains Mono'">{{ t }}%</text>
      </g>
      <!-- lempar koin -->
      <line :x1="X(50)" :x2="X(50)" :y1="16" :y2="Y + 4" stroke="#10131a" stroke-width="2" stroke-dasharray="4 6" />
      <text :x="X(50) - 12" y="22" text-anchor="end" fill="#10131a" style="font-size:15px;font-weight:700;font-family:'Plus Jakarta Sans'">lempar koin</text>
      <text :x="X(100)" y="22" text-anchor="end" fill="#7b8190" style="font-size:14px;font-family:'JetBrains Mono'">selalu benar →</text>

      <g v-for="t in titik" :key="t.p" class="muncul" :class="{ ya: k >= t.n }">
        <circle :cx="X(t.p)" :cy="Y" r="13" :fill="t.n === 1 ? '#c0392b' : '#a86b00'" stroke="#fff" stroke-width="3" />
        <line :x1="X(t.p)" :x2="X(t.p) + (t.n === 1 ? -60 : 60)" :y1="Y - 16" :y2="Y - 52" stroke="#cbd0d9" stroke-width="1.5" />
        <text :x="X(t.p) + (t.n === 1 ? -66 : 66)" :y="Y - 64" :text-anchor="t.n === 1 ? 'end' : 'start'" :fill="t.n === 1 ? '#c0392b' : '#a86b00'"
              style="font-size:34px;font-weight:800;font-family:'Plus Jakarta Sans';letter-spacing:-0.03em">{{ t.label }}</text>
        <text :x="X(t.p) + (t.n === 1 ? -66 : 66)" :y="Y - 42" :text-anchor="t.n === 1 ? 'end' : 'start'" fill="#4a5160"
              style="font-size:14px;font-family:'Plus Jakarta Sans'">{{ t.ket }}</text>
      </g>
    </svg>

    <div class="bawah">
      <p class="muncul-html" :class="{ ya: k >= 1 }">315 peserta, 128 wajah masing-masing. Rata-rata <b>sedikit di bawah lempar koin</b> — dan wajah buatan AI justru dinilai <b>lebih dapat dipercaya</b>.</p>
      <div class="iproov muncul-html" :class="{ ya: k >= 3 }">
        <p class="angka">0,1%</p>
        <p>dari 2.000 orang yang benar <b>semua</b> saat memilah foto dan video asli/palsu — padahal sudah diberi tahu ada deepfake. Lebih dari 60% yakin dengan kemampuannya.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.muncul { opacity: 0; transition: opacity .5s ease; }
.muncul.ya { opacity: 1; }
.bawah { display: grid; grid-template-columns: 1fr 1fr; gap: 56px; margin-top: 26px; border-top: 1px solid #e1e4ea; padding-top: 22px; }
.bawah p { margin: 0; font-size: 19px; line-height: 1.45; color: #10131a; }
.iproov { display: grid; grid-template-columns: 150px 1fr; gap: 18px; align-items: start; }
.iproov .angka { font-weight: 800; font-size: 64px; line-height: .95; letter-spacing: -0.04em; color: #c0392b; }
.muncul-html { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.muncul-html.ya { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) { .muncul, .muncul-html { transition: none; } }
</style>
