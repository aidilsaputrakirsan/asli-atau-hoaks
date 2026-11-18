<script setup>
// OSINT dalam satu garis waktu (SEMUA ILUSTRASI): foto "banjir pagi ini" di grup WA 2026,
// cari balik menemukan unggahan lebih lama → sumber pertama 2019 di kota lain → konteks dipelintir.
// Per klik (frontmatter `clicks: 4`): 1 = cari balik (titik lama muncul) · 2 = sumber pertama disorot
// 3 = geolokasi & kronolokasi · 4 = kesimpulan. Ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const W = 1120, Y = 110, x0 = 40, x1 = W - 40
const tahun = [2019, 2020, 2021, 2022, 2023, 2024, 2025, 2026]
const X = (t) => x0 + ((t - 2019) / 7) * (x1 - x0)
const lama = [
  { t: 2019.2, label: 'akun berita, kota lain', pertama: true },
  { t: 2021.6, label: 'diunggah ulang' },
  { t: 2023.9, label: 'diunggah ulang' },
]
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + 46" :viewBox="`0 0 ${W} ${Y + 46}`" fill="none" stroke-linecap="round" aria-hidden="true">
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#cbd0d9" stroke-width="2" />
      <text v-for="t in tahun" :key="t" :x="X(t)" :y="Y + 32" text-anchor="middle" fill="#7b8190" style="font-size:13px;font-family:'JetBrains Mono'">{{ t }}</text>

      <!-- klaim hari ini -->
      <circle :cx="X(2026)" :cy="Y" r="11" fill="#c0392b" />
      <rect :x="X(2026) - 228" :y="Y - 96" width="236" height="56" rx="14" fill="#fff" stroke="#cbd0d9" />
      <text :x="X(2026) - 214" :y="Y - 72" fill="#10131a" style="font-size:15px;font-weight:700;font-family:'Plus Jakarta Sans'">“Banjir di Balikpapan pagi ini!”</text>
      <text :x="X(2026) - 214" :y="Y - 52" fill="#7b8190" style="font-size:12px;font-family:'JetBrains Mono'">grup WhatsApp · 2026</text>

      <!-- sapuan cari balik -->
      <line :x1="X(2026)" :x2="X(2019.2)" :y1="Y - 22" :y2="Y - 22" stroke="#1f62d6" stroke-width="2" stroke-dasharray="5 6"
            class="sapu" :style="{ strokeDashoffset: 0, opacity: k >= 1 ? 1 : 0 }" />
      <text :x="X(2025.4)" :y="Y - 30" text-anchor="middle" fill="#1f62d6" class="muncul" :class="{ ya: k >= 1 }" style="font-size:13px;font-family:'JetBrains Mono'">← cari balik</text>

      <g v-for="(l, i) in lama" :key="i" class="muncul" :class="{ ya: k >= 1 }" :style="{ transitionDelay: (0.3 + (2 - i) * 0.2) + 's' }">
        <circle :cx="X(l.t)" :cy="Y" :r="l.pertama && k >= 2 ? 14 : 9" :fill="l.pertama && k >= 2 ? '#0b7a6e' : '#10131a'" class="titik" />
        <text :x="l.pertama ? X(l.t) - 14 : X(l.t)" :y="Y - 34" :text-anchor="l.pertama ? 'start' : 'middle'" :fill="l.pertama && k >= 2 ? '#0b7a6e' : '#4a5160'"
              :style="{ fontSize: '14px', fontWeight: l.pertama && k >= 2 ? 800 : 500, fontFamily: 'Plus Jakarta Sans' }">{{ l.pertama && k >= 2 ? 'sumber pertama: ' + l.label : l.label }}</text>
      </g>
    </svg>

    <div class="bawah">
      <div class="muncul-html" :class="{ ya: k >= 3 }">
        <p class="label">geolokasi</p><p>Rambu dan bangunan tidak cocok dengan jalan mana pun di Balikpapan (Google Maps / Street View).</p>
      </div>
      <div class="muncul-html" :class="{ ya: k >= 3 }" style="transition-delay:.15s">
        <p class="label">kronolokasi</p><p>Bayangan jatuh panjang ke timur — diambil sore hari, bukan “pagi ini” (SunCalc).</p>
      </div>
      <div class="muncul-html simpul" :class="{ ya: k >= 4 }">
        <p class="label merah">kesimpulan</p><p><b>Foto asli, konteks dipelintir</b> — tingkat 01. Tidak satu pun detektor AI akan menangkapnya.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sapu { transition: opacity .6s ease; }
.muncul { opacity: 0; transition: opacity .45s ease; }
.muncul.ya { opacity: 1; }
.titik { transition: r .3s ease, fill .3s ease; }
.bawah { display: grid; grid-template-columns: 1fr 1fr 1.15fr; gap: 36px; margin-top: 20px; border-top: 1px solid #e1e4ea; padding-top: 18px; }
.bawah p { margin: 0; font-size: 17px; line-height: 1.45; }
.label { font-family: 'JetBrains Mono', monospace; font-size: 13px !important; color: #0b7a6e; margin-bottom: 6px !important; }
.label.merah { color: #c0392b; }
.simpul p:last-child { font-size: 19px; }
.muncul-html { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.muncul-html.ya { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) { .muncul, .muncul-html, .sapu, .titik { transition: none; } }
</style>
