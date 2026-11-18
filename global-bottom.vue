<script setup>
// Latar terang + kisi titik "piksel" yang sangat samar (tema: memeriksa gambar sampai ke pikselnya).
// Slide pernyataan (class: malam) memakai latar sedikit lebih tegas. Statis: aman untuk ekspor.
// Latar dilukis di sini karena .slidev-layout dibuat transparan (lihat styles/index.css).
import { computed } from 'vue'
import { injectLocal } from '@vueuse/core'

const konteks = injectLocal('$$slidev-context')
const fm = computed(() => konteks.nav?.currentSlideRoute?.meta?.slide?.frontmatter || {})
const malam = computed(() => String(fm.value.class || '').includes('malam'))
</script>

<template>
  <div class="absolute inset-0 latar" :class="{ malam }" aria-hidden="true" />
</template>

<style scoped>
.latar {
  pointer-events: none;
  background-color: #f6f7f9;
  background-image: radial-gradient(circle, rgba(16, 19, 26, 0.09) 1px, transparent 1.2px);
  background-size: 24px 24px;
  transition: background-color .5s ease;
}
.latar.malam { background-color: #e9edf3; }
</style>
