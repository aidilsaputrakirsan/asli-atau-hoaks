<script setup>
// Gambar/video dengan penanda bernomor di atasnya + catatan bernomor di sampingnya.
// Per klik: penanda ke-n dan catatannya muncul ($clicks >= n). Ekspor: semua tampil, video diganti poster (src).
// titik: [{ x: 50, y: 10, judul, ket }] — x/y dalam persen dari bingkai media.
import { computed, ref, watch } from 'vue'
import { useIsSlideActive, useNav, useSlideContext } from '@slidev/client'

const props = defineProps({
  src: String, video: String,
  titik: { type: Array, required: true },
  tinggi: { type: Number, default: 400 },
  rasio: { type: Number, default: 1.5 }, // lebar / tinggi media
  kredit: String,
})
const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))
const base = (p) => p?.startsWith('/') ? import.meta.env.BASE_URL + p.slice(1) : p
const aktif = useIsSlideActive()
const vid = ref(null)
const pakaiVideo = computed(() => props.video && !isPrintMode.value)
watch([aktif, vid], ([a, v]) => {
  if (!v) return
  if (a) { v.currentTime = 0; v.play().catch(() => {}) } else { v.pause(); v.currentTime = 0 }
}, { immediate: true })
const lebar = computed(() => Math.round(props.tinggi * props.rasio))
</script>

<template>
  <div class="sorot">
    <figure :style="{ width: lebar + 'px' }">
      <div class="media" :style="{ height: tinggi + 'px' }">
        <video v-if="pakaiVideo" ref="vid" :src="base(video)" :poster="base(src)" muted loop playsinline preload="auto" />
        <img v-else :src="base(src)" alt="">
        <span v-for="(t, i) in titik" :key="i" class="penanda" :class="{ ya: k > i }" :style="{ left: t.x + '%', top: t.y + '%' }">{{ i + 1 }}</span>
      </div>
      <figcaption v-if="kredit">{{ kredit }}</figcaption>
    </figure>
    <ol class="catatan">
      <li v-for="(t, i) in titik" :key="i" :class="{ ya: k > i }">
        <span class="no">{{ i + 1 }}</span>
        <div><p class="judul">{{ t.judul }}</p><p class="ket">{{ t.ket }}</p></div>
      </li>
      <slot />
    </ol>
  </div>
</template>

<style scoped>
.sorot { display: flex; gap: 44px; align-items: flex-start; }
figure { margin: 0; flex: none; }
.media { position: relative; border-radius: 14px; overflow: hidden; background: #10131a; }
.media img, .media video { width: 100%; height: 100%; object-fit: cover; display: block; }
figcaption { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #7b8190; margin-top: 6px; line-height: 1.35; }
.penanda { position: absolute; transform: translate(-50%, -50%) scale(.6); width: 34px; height: 34px; border-radius: 50%; background: #fff; color: #10131a;
  font-weight: 800; font-size: 16px; display: flex; align-items: center; justify-content: center; box-shadow: 0 0 0 3px #c0392b; opacity: 0;
  transition: opacity .35s ease, transform .45s cubic-bezier(.2,1.4,.4,1); }
.penanda.ya { opacity: 1; transform: translate(-50%, -50%) scale(1); }
.catatan { list-style: none; padding: 0; margin: 0; flex: 1; }
.catatan li { display: grid; grid-template-columns: 40px 1fr; gap: 14px; padding: 14px 0; border-top: 1px solid #e1e4ea; margin: 0;
  opacity: .18; transition: opacity .4s ease; }
.catatan li::before { display: none; }
.catatan li.ya { opacity: 1; }
.catatan .no { width: 30px; height: 30px; border-radius: 50%; border: 2px solid #c0392b; color: #c0392b; font-weight: 800; font-size: 14px; display: flex; align-items: center; justify-content: center; }
.catatan p { margin: 0; }
.judul { font-weight: 800; font-size: 20px; line-height: 1.25; letter-spacing: -0.01em; color: #10131a; }
.ket { font-size: 16px; line-height: 1.45; color: #4a5160; margin-top: 4px !important; }
@media (prefers-reduced-motion: reduce) { .penanda, .catatan li { transition: none; } }
</style>
