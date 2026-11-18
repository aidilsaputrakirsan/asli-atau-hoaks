<script setup>
// Rantai pengamanan bukti digital + demo hash. Hash = SHA-256 ASLI dari public/kuis/d.jpg
// dan dari salinannya yang diubah 1 byte (dihitung dengan `shasum -a 256`).
// Per klik (frontmatter `clicks: 3`): 1 = rantai · 2 = hash file asli · 3 = ubah 1 byte → hash berubah total.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const mata = [
  { nama: 'File asli', ket: 'dari sumber terdekat' },
  { nama: 'Sidik jari (hash)', ket: 'dicatat saat diamankan' },
  { nama: 'Salinan kerja', ket: 'semua analisis di sini' },
  { nama: 'Catatan langkah', ket: 'siapa, kapan, alat apa' },
  { nama: 'Ahli forensik', ket: 'untuk persidangan' },
]
const asli = '4588f2a76f11c51746314dbf8d6ba9ee2e14724264894b1d104dc978744b2d50'
const ubah = 'da703413f2adf0f4eaaf1cf6c969ced0093948100b167c42035338b3d7357c5a'
</script>

<template>
  <div>
    <div class="rantai" :class="{ ya: k >= 1 }">
      <template v-for="(m, i) in mata" :key="i">
        <span v-if="i" class="mata-rantai" aria-hidden="true" />
        <div class="mata" :style="{ transitionDelay: i * 0.1 + 's' }">
          <p class="nama">{{ m.nama }}</p><p class="ket">{{ m.ket }}</p>
        </div>
      </template>
    </div>

    <div class="hash">
      <div class="baris" :class="{ ya: k >= 2 }">
        <span class="label">sate.jpg — asli</span><code>{{ asli }}</code>
      </div>
      <div class="baris ubah" :class="{ ya: k >= 3 }">
        <span class="label merah">1 byte diubah</span><code>{{ ubah }}</code>
      </div>
      <p class="arti" :class="{ ya: k >= 3 }">Satu perubahan sekecil apa pun → sidik jari berubah total. Hash yang sama = file belum disentuh sejak diamankan.</p>
    </div>
  </div>
</template>

<style scoped>
p { margin: 0; }
.rantai { display: flex; align-items: center; }
.mata { flex: 1; border: 2px solid #10131a; border-radius: 999px; padding: 12px 18px; text-align: center; background: #fff;
  opacity: 0; transform: translateY(8px); transition: opacity .4s ease, transform .4s ease; }
.rantai.ya .mata { opacity: 1; transform: none; }
.mata:last-child { border-color: #1f62d6; }
.mata-rantai { width: 22px; height: 10px; border: 2px solid #10131a; border-radius: 6px; flex: none; margin: 0 -4px; position: relative; z-index: 1; background: #f6f7f9; }
.nama { font-weight: 800; font-size: 17px; line-height: 1.2; }
.mata:last-child .nama { color: #1f62d6; }
.ket { font-size: 13.5px; color: #4a5160; margin-top: 2px !important; }
.hash { margin-top: 40px; }
.baris { display: grid; grid-template-columns: 170px 1fr; gap: 18px; align-items: baseline; padding: 12px 0; border-top: 1px solid #e1e4ea;
  opacity: 0; transition: opacity .45s ease; }
.baris.ya { opacity: 1; }
.label { font-family: 'JetBrains Mono', monospace; font-size: 14px; color: #0b7a6e; }
.label.merah { color: #c0392b; }
code { font-family: 'JetBrains Mono', monospace; font-size: 17px; letter-spacing: 0.02em; color: #10131a; background: none; padding: 0; word-break: break-all; }
.ubah code { color: #c0392b; }
.arti { font-size: 19px; line-height: 1.45; margin-top: 14px !important; opacity: 0; transition: opacity .45s ease .3s; }
.arti.ya { opacity: 1; }
@media (prefers-reduced-motion: reduce) { .mata, .baris, .arti { transition: none; } }
</style>
