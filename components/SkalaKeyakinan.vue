<script setup>
// Lima tingkat keyakinan sebagai SKALA dengan jarum, memakai kasus video bodycam (slide sebelumnya).
// Jarum bergeser saat temuan bertambah. Per klik (frontmatter `clicks: 3`):
// 1 = video masuk → "tidak dapat ditentukan" · 2 = dua detektor menilai mirip AI → "ada indikasi"
// 3 = sumber pertama: akun pembuat, berlabel Sora → "terbukti rekayasa". Ekspor: posisi akhir + semua catatan.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const tingkat = [
  { nama: 'terbukti rekayasa', warna: '#c0392b' },
  { nama: 'ada indikasi rekayasa', warna: '#c0392b' },
  { nama: 'tidak dapat ditentukan', warna: '#a86b00' },
  { nama: 'konsisten, belum terverifikasi', warna: '#0b7a6e' },
  { nama: 'terverifikasi asli', warna: '#0b7a6e' },
]
const temuan = [
  { teks: 'Video “rekaman bocor” masuk lewat grup. Belum ada temuan.', pos: 2 },
  { teks: 'Watermark terpotong. Dua dari tiga detektor menilai mirip AI.', pos: 1 },
  { teks: 'Sumber pertama ditemukan: akun pembuat konten, berlabel Sora.', pos: 0 },
]
const W = 1120, Y = 64, x0 = 100, x1 = W - 100
const X = tingkat.map((_, i) => x0 + (i * (x1 - x0)) / 4)
const pos = computed(() => (k.value < 1 ? null : temuan[Math.min(k.value, 3) - 1].pos))
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + 70" :viewBox="`0 0 ${W} ${Y + 70}`" fill="none" stroke-linecap="round" aria-hidden="true">
      <line :x1="X[0]" :x2="X[2]" :y1="Y" :y2="Y" stroke="#e8b4ad" stroke-width="6" />
      <line :x1="X[2]" :x2="X[4]" :y1="Y" :y2="Y" stroke="#a9d8d1" stroke-width="6" />
      <g v-for="(t, i) in tingkat" :key="i">
        <circle :cx="X[i]" :cy="Y" r="9" fill="#fff" :stroke="t.warna" stroke-width="3" />
        <text :x="X[i]" :y="Y + 40" text-anchor="middle" :fill="pos === i ? t.warna : '#4a5160'"
              :style="{ fontSize: '15px', fontWeight: pos === i ? 800 : 500, fontFamily: 'Plus Jakarta Sans' }">{{ t.nama }}</text>
      </g>
      <g v-if="pos !== null" class="jarum" :style="{ transform: `translateX(${X[pos]}px)` }">
        <path d="M0 -6 L-11 -30 L11 -30 Z" :fill="tingkat[pos].warna" />
      </g>
    </svg>

    <ol class="catatan">
      <li v-for="(t, i) in temuan" :key="i" :class="{ ya: k > i, kini: k === i + 1 || isPrintMode }">
        <span class="no">temuan {{ i + 1 }}</span><span>{{ t.teks }}</span><span class="hasil" :style="{ color: tingkat[t.pos].warna }">→ {{ tingkat[t.pos].nama }}</span>
      </li>
    </ol>
  </div>
</template>

<style scoped>
.jarum { transition: transform .8s cubic-bezier(.45,.05,.25,1); }
.jarum path { transform: translateY(64px); }
.catatan { list-style: none; margin: 18px 0 0; padding: 0; border-top: 1px solid #e1e4ea; }
.catatan li { display: grid; grid-template-columns: 110px 1fr 280px; gap: 18px; padding: 14px 0; margin: 0; border-bottom: 1px solid #e1e4ea; font-size: 19px; line-height: 1.4;
  opacity: 0; transform: translateY(8px); transition: opacity .4s ease, transform .4s ease; }
.catatan li::before { display: none; }
.catatan li.ya { opacity: .45; transform: none; }
.catatan li.ya.kini { opacity: 1; }
.no { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190; padding-top: 4px; }
.hasil { font-weight: 700; font-size: 17px; }
@media (prefers-reduced-motion: reduce) { .jarum, .catatan li { transition: none; } }
</style>
