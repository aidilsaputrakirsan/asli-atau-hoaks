<script setup>
// Kuis pembuka "asli atau AI?": 4 gambar berhuruf A–D. Jawaban muncul saat `buka` (di slide: :buka="$clicks >= 1").
// Jawaban = garis warna di bawah gambar + label mono kecil (bukan badge). Ekspor: jawaban tampil.
import { reactive } from 'vue'
import { useNav } from '@slidev/client'

const props = defineProps({
  item: { type: Array, required: true }, // [{ src, jawab: 'asli'|'ai', ket }]
  buka: Boolean,
  tinggi: { type: Number, default: 250 },
})
const { isPrintMode } = useNav()
const gagal = reactive({})
const base = (p) => p?.startsWith('/') ? import.meta.env.BASE_URL + p.slice(1) : p
const huruf = (i) => String.fromCharCode(65 + i)
</script>

<template>
  <div class="kuis">
    <figure v-for="(it, i) in props.item" :key="i" :class="[{ buka: buka || isPrintMode }, it.jawab]">
      <div class="bingkai" :style="{ height: tinggi + 'px' }">
        <img v-if="!gagal[i]" :src="base(it.src)" :alt="'Gambar ' + huruf(i)" @error="gagal[i] = true">
        <div v-else class="kosong">gambar {{ huruf(i) }} belum ada<br>→ public{{ it.src }}</div>
      </div>
      <figcaption>
        <span class="huruf">{{ huruf(i) }}</span>
        <span class="jawab">{{ it.jawab === 'ai' ? 'buatan AI' : 'asli' }}</span>
      </figcaption>
      <p class="ket">{{ it.ket }}</p>
    </figure>
  </div>
</template>

<style scoped>
.kuis { display: grid; grid-template-columns: repeat(4, 1fr); gap: 22px; }
figure { margin: 0; }
.bingkai { overflow: hidden; border-radius: 14px; background: #fff; border: 1px solid #e1e4ea; transition: box-shadow .4s ease; }
img { width: 100%; height: 100%; object-fit: cover; display: block; }
.kosong { height: 100%; display: flex; align-items: center; justify-content: center; text-align: center; font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190; }
figcaption { display: flex; align-items: baseline; gap: 12px; margin-top: 12px; padding-top: 10px; border-top: 3px solid #e1e4ea; transition: border-color .4s ease; }
.huruf { font-weight: 800; font-size: 26px; line-height: 1; color: #10131a; }
.jawab { font-family: 'JetBrains Mono', monospace; font-size: 15px; opacity: 0; transition: opacity .4s ease; }
.ket { margin: 6px 0 0; font-size: 15px; line-height: 1.4; color: #4a5160; opacity: 0; transform: translateY(6px); transition: opacity .4s ease .1s, transform .4s ease .1s; }
.buka .jawab, .buka .ket { opacity: 1; transform: none; }
.buka.ai figcaption { border-top-color: #c0392b; }
.buka.ai .jawab { color: #c0392b; }
.buka.asli figcaption { border-top-color: #0b7a6e; }
.buka.asli .jawab { color: #0b7a6e; }
.buka.ai .bingkai { box-shadow: 0 0 0 3px #c0392b; }
@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }
</style>
