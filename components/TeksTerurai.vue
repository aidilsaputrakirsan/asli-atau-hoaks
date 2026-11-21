<script setup>
// Teks yang mulai "teracak" lalu terurai huruf demi huruf menjadi kalimat asli.
// Diadaptasi dari DecryptedText — Vue Bits (https://vue-bits.dev, MIT + Commons Clause),
// disederhanakan: tanpa motion-v, tanpa hover, dipicu oleh slide/klik Slidev.
//
// Pakai: <TeksTerurai teks="Pertanyaannya bukan “AI atau bukan?”" />        → main saat slide dibuka
//        <TeksTerurai teks="..." :at="2" />                                  → main saat klik ke-2
// Slide tidak aktif & mode ekspor: selalu kalimat utuh (thumbnail/PDF rapi).
import { computed, ref, watch, onBeforeUnmount } from 'vue'
import { useSlideContext, useNav, useIsSlideActive } from '@slidev/client'

const props = defineProps({
  teks: { type: String, required: true },
  at: { type: Number, default: 0 },          // klik pemicu; 0 = saat slide dibuka
  kecepatan: { type: Number, default: 38 },  // ms per langkah
  jeda: { type: Number, default: 250 },      // ms sebelum huruf pertama terbuka
  karakter: { type: String, default: 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789#%&*/<>' },
})

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const aktif = useIsSlideActive()

const huruf = computed(() => Array.from(props.teks))
const spasi = (c) => /\s/.test(c)
const acak = () => props.karakter[Math.floor(Math.random() * props.karakter.length)]

// Kelompokkan per kata supaya baris tidak patah di tengah kata.
const kata = computed(() => {
  const out = []
  let k = null
  huruf.value.forEach((c, i) => {
    if (spasi(c)) { out.push({ spasi: c, i }); k = null; return }
    if (!k) { k = { i, isi: [] }; out.push(k) }
    k.isi.push(i)
  })
  return out
})

// terbuka[i] = huruf ke-i sudah asli; tampil[i] = glyph acak untuk yang belum.
const terbuka = ref(huruf.value.map(() => true))
const tampil = ref([...huruf.value])
let timer, mulaiTimer

const berhenti = () => { clearInterval(timer); clearTimeout(mulaiTimer) }
const utuh = () => { berhenti(); terbuka.value = huruf.value.map(() => true) }
const tutup = () => {
  berhenti()
  terbuka.value = huruf.value.map((c) => spasi(c))
  tampil.value = huruf.value.map((c) => (spasi(c) ? c : acak()))
}
const main = () => {
  tutup()
  let n = 0
  const urutan = huruf.value.map((_, i) => i).filter((i) => !spasi(huruf.value[i]))
  mulaiTimer = setTimeout(() => {
    timer = setInterval(() => {
      const t = [...terbuka.value]
      if (n < urutan.length) t[urutan[n++]] = true
      terbuka.value = t
      tampil.value = huruf.value.map((c, i) => (t[i] ? c : acak()))
      if (n >= urutan.length) berhenti()
    }, props.kecepatan)
  }, props.jeda)
}

const reduksi = typeof window !== 'undefined' && window.matchMedia?.('(prefers-reduced-motion: reduce)').matches

// Keadaan: 'utuh' (slide tidak aktif / ekspor), 'tertutup' (aktif tapi klik belum sampai), 'main'.
const keadaan = computed(() => {
  if (isPrintMode.value || reduksi || !aktif.value) return 'utuh'
  return $clicks.value >= props.at ? 'main' : 'tertutup'
})

watch(keadaan, (k) => {
  if (k === 'utuh') utuh()
  else if (k === 'tertutup') tutup()
  else main()
}, { immediate: true })

watch(() => props.teks, () => { if (keadaan.value === 'utuh') utuh() })
onBeforeUnmount(berhenti)
</script>

<template>
  <span class="terurai">
    <span class="sr-only">{{ teks }}</span>
    <span aria-hidden="true">
      <template v-for="k in kata" :key="k.i">
        <template v-if="k.spasi">{{ k.spasi }}</template>
        <span v-else class="kata">
          <span v-for="i in k.isi" :key="i" class="sel" :class="{ acak: !terbuka[i] }">
            <template v-if="terbuka[i]">{{ huruf[i] }}</template>
            <template v-else>
              <!-- huruf asli tak terlihat menjaga lebar, glyph acak ditumpuk di atasnya: tidak ada loncatan layout -->
              <span class="bayang">{{ huruf[i] }}</span>
              <span class="glyph">{{ tampil[i] }}</span>
            </template>
          </span>
        </span>
      </template>
    </span>
  </span>
</template>

<style scoped>
.terurai { white-space: pre-wrap; }
.kata { white-space: nowrap; }
.sel { transition: color 0.5s cubic-bezier(0.22, 1, 0.36, 1); }
.sel.acak { position: relative; display: inline-block; color: var(--samar); }
.bayang { visibility: hidden; }
.glyph {
  position: absolute; top: 0; left: 50%; transform: translateX(-50%);
  font-family: 'JetBrains Mono', monospace; font-weight: 500; font-size: 0.74em; line-height: 1.35;
}
.sr-only {
  position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px;
  overflow: hidden; clip: rect(0, 0, 0, 0); white-space: nowrap; border: 0;
}
</style>
