<script setup>
// Sampul: konten yang beredar (titik abu-abu) masuk ke titik "diperiksa", lalu keluar ke tiga muara:
// asli (teal), belum pasti (kuning), rekayasa (merah, jatuh). Berulang terus (SMIL).
// Ekspor / reduced-motion: hanya kerangka diam.
import { useNav } from '@slidev/client'
const { isPrintMode } = useNav()
const gerak = !isPrintMode.value && !(typeof window !== 'undefined' && window.matchMedia?.('(prefers-reduced-motion: reduce)').matches)

const P = { x: 520, y: 80 }
const muara = [
  { y: 26, warna: '#0b7a6e', label: 'asli' },
  { y: 80, warna: '#a86b00', label: 'belum pasti' },
  { y: 134, warna: '#c0392b', label: 'rekayasa' },
]
const XM = 1030
const ys = [12, 34, 58, 102, 126, 148, 24, 138]
const partikel = Array.from({ length: 18 }, (_, i) => {
  const y = ys[i % ys.length]
  const m = muara[[0, 2, 0, 1, 2, 0][i % 6]]
  const masuk = `M${10 + (i * 41) % 130},${y} C250,${y} 330,${P.y} ${P.x},${P.y}`
  const keluar = m.label === 'rekayasa'
    ? ` C${P.x + 140},${P.y} ${P.x + 180},${m.y} ${P.x + 260},${m.y} Q${P.x + 300},${m.y} ${P.x + 310},${m.y + 70}`
    : ` C${P.x + 140},${P.y} ${P.x + 260},${m.y} ${XM},${m.y}`
  return { d: masuk + keluar, warna: m.warna, begin: -(i * 0.36) }
})
const kaca = `M${P.x + 6},${P.y + 6} l8,8`
</script>

<template>
  <svg class="sampul-alur" viewBox="0 0 1120 170" aria-hidden="true">
    <path v-for="y in ys.slice(0, 6)" :key="y" :d="`M10,${y} C250,${y} 330,${P.y} ${P.x},${P.y}`" class="jalur" />
    <path v-for="m in muara" :key="m.label" :d="`M${P.x},${P.y} C${P.x + 140},${P.y} ${P.x + 260},${m.y} ${XM},${m.y}`" class="jalur kuat" />

    <circle :cx="P.x" :cy="P.y" r="20" class="simpul" />
    <path :d="kaca" class="gagang" />
    <circle :cx="P.x" :cy="P.y" r="8" class="lensa" />
    <g v-for="m in muara" :key="'u' + m.label">
      <circle :cx="XM" :cy="m.y" r="8" :fill="m.warna" />
      <text :x="XM + 18" :y="m.y + 5" class="label">{{ m.label }}</text>
    </g>

    <text x="10" y="168" class="label">konten beredar</text>
    <text :x="P.x" :y="P.y + 46" class="label tengah">diperiksa</text>

    <template v-if="gerak">
      <circle v-for="(p, i) in partikel" :key="i" r="3.6" fill="#9aa1ad">
        <animateMotion :path="p.d" dur="7s" :begin="p.begin + 's'" repeatCount="indefinite" calcMode="spline" keyTimes="0;1" keySplines="0.4 0 0.6 1" />
        <animate attributeName="fill" :values="`#9aa1ad;#9aa1ad;${p.warna};${p.warna}`" keyTimes="0;0.5;0.58;1" dur="7s" :begin="p.begin + 's'" repeatCount="indefinite" />
        <animate attributeName="opacity" values="0;1;1;0" keyTimes="0;0.08;0.88;1" dur="7s" :begin="p.begin + 's'" repeatCount="indefinite" />
      </circle>
    </template>
  </svg>
</template>

<style scoped>
.sampul-alur { width: 100%; height: auto; display: block; overflow: visible; }
.jalur { fill: none; stroke: #d5d9e0; stroke-width: 1; }
.jalur.kuat { stroke: #c3c8d1; stroke-width: 1.4; }
.simpul { fill: #fff; stroke: #10131a; stroke-width: 1.6; }
.lensa { fill: none; stroke: #1f62d6; stroke-width: 2.4; }
.gagang { stroke: #1f62d6; stroke-width: 3; stroke-linecap: round; }
.label { fill: #4a5160; font-family: 'JetBrains Mono', monospace; font-size: 13px; }
.label.tengah { text-anchor: middle; }
</style>
