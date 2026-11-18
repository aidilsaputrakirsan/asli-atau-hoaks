<script setup>
// Lima langkah verifikasi sebagai lima gerbang di jalur "pesan masuk → laporan" (pola LimaGerbang SIMFONI).
// Per klik (frontmatter `clicks: 6`): 1–5 = gerbang ke-n aktif + panel fokus · 6 = cabang "serahkan ke ahli".
// Ekspor: semua gerbang centang + daftar ringkas.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const cetak = computed(() => isPrintMode.value)
const k = computed(() => (cetak.value ? 99 : $clicks.value))
const aktif = computed(() => (k.value >= 6 ? 6 : k.value))

const gerbang = [
  { no: '01', nama: 'Amankan', tanya: 'Simpan file paling asli, tautan, dan tangkapan layar unggahan — sebelum dihapus.', kenapa: 'Yang hilang di langkah ini tidak bisa diperiksa di langkah berikutnya. Catat waktu dan hash file.' },
  { no: '02', nama: 'Asal-usul', tanya: 'Masih adakah metadata, Content Credentials, atau watermark?', kenapa: 'Kalau ada, ini jejak terkuat. Kalau tidak ada, jangan langsung disimpulkan palsu.' },
  { no: '03', nama: 'Konteks', tanya: 'Kapan pertama muncul, oleh siapa, di mana sebenarnya?', kenapa: 'Cari balik, sumber pertama, geolokasi, kronolokasi. Paling ampuh untuk hoaks sehari-hari.' },
  { no: '04', nama: 'Teknis', tanya: 'Ada kejanggalan visual? Apa kata beberapa detektor?', kenapa: 'Pakai lebih dari satu alat. Hasil detektor = petunjuk ke mana harus melihat, bukan vonis.' },
  { no: '05', nama: 'Simpulkan', tanya: 'Seberapa yakin — dan atas dasar temuan apa saja?', kenapa: 'Tulis tingkat keyakinan dan dasar setiap temuan, bukan sekadar “asli” atau “hoaks”.' },
]
const W = 1120, Y = 70, R = 22, x0 = 110, x1 = W - 110
const X = gerbang.map((_, i) => x0 + ((i + 1) * (x1 - x0)) / 6)
const pj = x1 - x0
const majuPj = computed(() => (aktif.value === 0 ? 0 : aktif.value >= 6 ? pj : X[aktif.value - 1] - x0))
const cabang = `M${X[3]} ${Y + R + 4} C ${X[3]} ${Y + 60}, ${X[3] + 60} ${Y + 66}, ${X[4] + 40} ${Y + 66} L ${x1} ${Y + 66}`
</script>

<template>
  <div :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + 104" :viewBox="`0 0 ${W} ${Y + 104}`" fill="none" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#e1e4ea" stroke-width="2" stroke-dasharray="3 7" />
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#0b7a6e" stroke-width="3" class="maju" :style="{ strokeDasharray: pj, strokeDashoffset: pj - majuPj }" />
      <circle :cx="x0" :cy="Y" r="6" fill="#7b8190" />
      <text :x="x0" :y="Y - 22" text-anchor="middle" fill="#4a5160" style="font-size:14px;font-family:'Plus Jakarta Sans'">pesan masuk</text>
      <path :d="`M${x1 - 10} ${Y - 9} L${x1} ${Y} L${x1 - 10} ${Y + 9}`" :stroke="k >= 5 ? '#0b7a6e' : '#cbd0d9'" stroke-width="3" />
      <text :x="x1" :y="Y - 22" text-anchor="middle" :fill="k >= 5 ? '#10131a' : '#7b8190'" style="font-size:14px;font-weight:700;font-family:'Plus Jakarta Sans'">laporan</text>

      <g v-for="(g, i) in gerbang" :key="g.no">
        <circle :cx="X[i]" :cy="Y" :r="aktif === i + 1 ? R + 4 : R" :fill="aktif > i + 1 ? '#0b7a6e' : '#fff'"
                :stroke="aktif > i ? '#0b7a6e' : '#cbd0d9'" :stroke-width="aktif === i + 1 ? 3 : 2" class="titik" />
        <path v-if="aktif > i + 1" :d="`M${X[i] - 8} ${Y + 1} L${X[i] - 2} ${Y + 7} L${X[i] + 9} ${Y - 6}`" stroke="#fff" stroke-width="3.2" />
        <text v-else :x="X[i]" :y="Y + 5" text-anchor="middle" :fill="aktif === i + 1 ? '#0b7a6e' : '#7b8190'" style="font-size:14px;font-weight:800;font-family:'JetBrains Mono'">{{ g.no }}</text>
        <text :x="X[i]" :y="Y - 34" text-anchor="middle" :fill="aktif >= i + 1 ? '#10131a' : '#7b8190'" style="font-size:16px;font-weight:700;font-family:'Plus Jakarta Sans'">{{ g.nama }}</text>
      </g>

      <g class="muncul" :class="{ ya: k >= 6 }">
        <path :d="cabang" stroke="#1f62d6" stroke-width="2.4" stroke-dasharray="6 6" />
        <path :d="`M${x1 - 10} ${Y + 57} L${x1} ${Y + 66} L${x1 - 10} ${Y + 75}`" stroke="#1f62d6" stroke-width="2.4" />
        <text :x="x1" :y="Y + 98" text-anchor="end" fill="#1f62d6" style="font-size:14px;font-weight:700;font-family:'Plus Jakarta Sans'">akan jadi alat bukti → ahli forensik digital</text>
      </g>
    </svg>

    <div v-if="!cetak" class="fokus">
      <Transition name="ganti" mode="out-in">
        <div v-if="k >= 6" key="ahli" class="isi">
          <p class="besar biru">→</p>
          <div>
            <p class="pertanyaan">Bila konten akan jadi <span class="biru">alat bukti</span> atau dasar penindakan, serahkan ke laboratorium forensik.</p>
            <p class="contoh">Lima langkah ini menyaring dan mengamankan. Pembuktian di persidangan tetap oleh ahli.</p>
          </div>
        </div>
        <div v-else-if="aktif > 0" :key="aktif" class="isi">
          <p class="besar">{{ gerbang[aktif - 1].no }}</p>
          <div>
            <p class="nama">{{ gerbang[aktif - 1].nama }}</p>
            <p class="pertanyaan">{{ gerbang[aktif - 1].tanya }}</p>
            <p class="contoh">{{ gerbang[aktif - 1].kenapa }}</p>
          </div>
        </div>
      </Transition>
    </div>
    <div v-else class="ringkas">
      <div v-for="g in gerbang" :key="g.no"><span class="no">{{ g.no }}</span><b>{{ g.nama }}</b><span>{{ g.tanya }}</span></div>
    </div>
  </div>
</template>

<style scoped>
.maju { transition: stroke-dashoffset .7s cubic-bezier(.45,.05,.25,1); }
.titik { transition: r .3s ease, fill .3s ease, stroke .3s ease; }
.muncul { opacity: 0; transition: opacity .5s ease; }
.muncul.ya { opacity: 1; }
.fokus { margin-top: 10px; border-top: 1px solid #e1e4ea; padding-top: 24px; min-height: 200px; }
.isi { display: grid; grid-template-columns: 140px 1fr; gap: 24px; align-items: start; }
.isi p { margin: 0; }
.besar { font-weight: 800; font-size: 92px; line-height: .9; letter-spacing: -0.04em; color: #0b7a6e; }
.besar.biru, .biru { color: #1f62d6; }
.nama { font-family: 'JetBrains Mono', monospace; font-size: 15px; color: #0b7a6e; margin-bottom: 8px !important; }
.pertanyaan { font-weight: 800; font-size: 32px; line-height: 1.18; letter-spacing: -0.02em; color: #10131a; }
.contoh { font-size: 19px; line-height: 1.45; color: #4a5160; margin-top: 14px !important; max-width: 860px; }
.ganti-enter-active, .ganti-leave-active { transition: opacity .25s ease, transform .3s cubic-bezier(.2,.7,.2,1); }
.ganti-enter-from { opacity: 0; transform: translateY(12px); }
.ganti-leave-to { opacity: 0; transform: translateY(-8px); }
.ringkas { margin-top: 8px; border-top: 1px solid #e1e4ea; }
.ringkas > div { display: grid; grid-template-columns: 44px 130px 1fr; gap: 14px; padding: 10px 0; border-bottom: 1px solid #e1e4ea; font-size: 17px; align-items: baseline; }
.ringkas .no { font-family: 'JetBrains Mono', monospace; color: #0b7a6e; font-size: 14px; }
.ringkas span:last-child { color: #4a5160; }
@media (prefers-reduced-motion: reduce) { .maju, .titik, .muncul, .ganti-enter-active, .ganti-leave-active { transition: none; } }
</style>
