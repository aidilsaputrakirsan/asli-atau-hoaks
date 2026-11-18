<script setup>
// Header berjalan: judul sesi + nama bagian (frontmatter `bagian`), garis tipis,
// dan nomor halaman kanan bawah. Tidak tampil di sampul. HARUS global-top.
import { computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentSlideRoute, currentPage, total } = useNav()
const fm = computed(() => currentSlideRoute.value?.meta?.slide?.frontmatter || {})
</script>

<template>
  <template v-if="fm.layout !== 'cover'">
    <header class="absolute left-0 right-0 top-0 flex justify-between items-center"
            style="margin: 0 80px; padding: 26px 0 14px; border-bottom: 1px solid #e1e4ea; font-family: 'Plus Jakarta Sans', sans-serif">
      <span style="font-weight: 800; font-size: 16px; letter-spacing: -0.01em; color: #10131a">Asli atau <span style="color: #c0392b">rekayasa?</span></span>
      <span v-if="fm.bagian" style="font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190">{{ fm.bagian }}</span>
    </header>
    <footer class="absolute right-0 bottom-0" style="padding: 0 80px 24px; font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190">
      <span style="color: #4a5160">{{ String(currentPage).padStart(2, '0') }}</span> / {{ total }}
    </footer>
  </template>
</template>
