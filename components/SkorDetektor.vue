<script setup>
// Satu gambar, tiga detektor, tiga jawaban berbeda. ANGKA = ILUSTRASI (bukan hasil uji nyata).
// Per klik (frontmatter `clicks: 2`): 1 = tiga batang tumbuh · 2 = arti skor "87%". Ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const props = defineProps({ src: String })
const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))
const base = (p) => p?.startsWith('/') ? import.meta.env.BASE_URL + p.slice(1) : p
const skor = [
  { nama: 'detektor A', p: 87 },
  { nama: 'detektor B', p: 41 },
  { nama: 'detektor C', p: 12 },
]
</script>

<template>
  <div class="skor">
    <div class="gambar"><img :src="base(src)" alt=""><p class="label">gambar yang sama <span>(ilustrasi skor)</span></p></div>
    <div class="kanan">
      <div v-for="(s, i) in skor" :key="s.nama" class="baris">
        <span class="nama">{{ s.nama }}</span>
        <span class="batang"><span :style="{ width: (k >= 1 ? s.p : 0) + '%', transitionDelay: i * 0.18 + 's', background: s.p > 60 ? '#c0392b' : s.p > 30 ? '#a86b00' : '#0b7a6e' }" /></span>
        <span class="p">{{ k >= 1 ? s.p : 0 }}% <small>“AI”</small></span>
      </div>
      <div class="arti" :class="{ ya: k >= 2 }">
        <p class="besar">“87% AI” <span class="biru">bukan</span> “87% pasti palsu”.</p>
        <p class="kecil">Artinya: menurut model ini, polanya mirip contoh AI yang pernah ia pelajari. Foto asli yang banyak dikompres bisa dituduh; model AI terbaru bisa lolos.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.skor { display: grid; grid-template-columns: 300px 1fr; gap: 48px; align-items: start; }
.gambar img { width: 300px; height: 230px; object-fit: cover; border-radius: 14px; display: block; }
.label { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #0b7a6e; margin: 8px 0 0; }
.label span { color: #7b8190; }
.baris { display: grid; grid-template-columns: 120px 1fr 110px; gap: 16px; align-items: center; padding: 12px 0; border-bottom: 1px solid #e1e4ea; }
.nama { font-family: 'JetBrains Mono', monospace; font-size: 15px; color: #4a5160; }
.batang { height: 16px; border-radius: 8px; background: #eceff3; overflow: hidden; }
.batang > span { display: block; height: 100%; border-radius: 8px; transition: width .9s cubic-bezier(.2,.7,.2,1); }
.p { font-weight: 800; font-size: 22px; text-align: right; font-variant-numeric: tabular-nums; }
.p small { font-weight: 500; font-size: 13px; color: #7b8190; }
.arti { margin-top: 26px; opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.arti.ya { opacity: 1; transform: none; }
.arti p { margin: 0; }
.besar { font-weight: 800; font-size: 30px; line-height: 1.2; letter-spacing: -0.02em; }
.biru { color: #1f62d6; }
.kecil { font-size: 18px; line-height: 1.45; color: #4a5160; margin-top: 10px !important; }
@media (prefers-reduced-motion: reduce) { .batang > span, .arti { transition: none; } }
</style>
