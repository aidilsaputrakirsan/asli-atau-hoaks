<script setup>
// Kuis pembuka "asli atau AI?": 4 gambar berlabel A–D. Jawaban muncul saat `buka` = true
// (di slide: :buka="$clicks >= 1"). Mode ekspor: jawaban langsung tampil.
// Gambar belum ada → bingkai putus-putus berisi petunjuk nama file.
import { reactive } from 'vue'
import { useNav } from '@slidev/client'

const props = defineProps({
  item: { type: Array, required: true }, // [{ src: '/kuis/a.jpg', jawab: 'asli'|'ai', ket: 'keterangan singkat' }]
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
    <figure v-for="(it, i) in props.item" :key="i">
      <div class="bingkai" :style="{ height: tinggi + 'px' }">
        <img v-if="!gagal[i]" :src="base(it.src)" :alt="'Gambar ' + huruf(i)" @error="gagal[i] = true">
        <div v-else class="kosong mono">gambar {{ huruf(i) }} belum ada<br>→ public{{ it.src }}</div>
        <span class="huruf">{{ huruf(i) }}</span>
      </div>
      <figcaption :class="{ tampak: buka || isPrintMode }">
        <span class="status" :class="it.jawab === 'ai' ? 'palsu' : 'asli'">{{ it.jawab === 'ai' ? 'BUATAN AI' : 'ASLI' }}</span>
        <span class="ket">{{ it.ket }}</span>
      </figcaption>
    </figure>
  </div>
</template>

<style scoped>
.kuis { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; }
figure { margin: 0; }
.bingkai { position: relative; overflow: hidden; border: 1px solid #cbd0d9; border-radius: 14px; background: #fff; }
img { width: 100%; height: 100%; object-fit: cover; display: block; }
.kosong { height: 100%; display: flex; align-items: center; justify-content: center; text-align: center; font-size: 13px; color: #7b8190; border-radius: 14px; outline: 1px dashed #cbd0d9; outline-offset: -8px; padding: 16px; }
.huruf { position: absolute; left: 10px; top: 10px; width: 34px; height: 34px; border-radius: 8px; background: #10131a; color: #fff; font-weight: 800; font-size: 18px; display: flex; align-items: center; justify-content: center; }
figcaption { margin-top: 12px; opacity: 0; transform: translateY(6px); transition: opacity .4s ease, transform .4s ease; }
figcaption.tampak { opacity: 1; transform: none; }
.ket { display: block; font-size: 14px; color: #4a5160; margin-top: 8px; line-height: 1.35; }
</style>
