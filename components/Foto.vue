<script setup>
// Foto dokumenter: warna asli, sedikit diredupkan agar menyatu dengan latar, sudut bulat, kredit lisensi di bawahnya.
// Saat slide aktif, foto membesar sangat pelan (Ken Burns) — tidak di mode ekspor.
import { computed } from 'vue'
import { useIsSlideActive, useNav } from '@slidev/client'

const props = defineProps({
  src: String,
  kredit: String, // wajib untuk CC BY / BY-SA: "Pembuat, Lisensi"
  ket: String,
  tinggi: { type: Number, default: 240 },
  posisi: { type: String, default: 'center' },
  atas: { type: Number, default: 0 }, // jarak atas (px)
})
// path "/foto/x.jpg" → ikut base deploy (GitHub Pages: /asli-atau-hoaks/)
const url = computed(() => props.src?.startsWith('/') ? import.meta.env.BASE_URL + props.src.slice(1) : props.src)
const aktif = useIsSlideActive()
const { isPrintMode } = useNav()
</script>

<template>
  <figure class="foto" :style="{ margin: `${atas}px 0 0` }">
    <div class="bingkai" :style="{ height: tinggi + 'px' }">
      <img :src="url" :alt="ket || ''" :class="{ hidup: aktif && !isPrintMode }" :style="{ objectPosition: posisi }">
    </div>
    <figcaption>
      <span v-if="ket">{{ ket }}</span><span v-if="ket && kredit"> · </span><span v-if="kredit" class="mono">Foto: {{ kredit }}</span>
    </figcaption>
  </figure>
</template>

<style scoped>
.bingkai { overflow: hidden; background: #ffffff; border: 1px solid #e1e4ea; border-radius: 14px; }
img {
  width: 100%; height: 100%; object-fit: cover; display: block;
  filter: saturate(1.05) contrast(1.04) brightness(1);
  transform: scale(1.0);
  transition: transform 24s ease-out;
}
img.hidup { transform: scale(1.06); }
figcaption { font-size: 12px; color: #7b8190; margin-top: 6px; line-height: 1.35; }
figcaption .mono { font-size: 11px; }
</style>
