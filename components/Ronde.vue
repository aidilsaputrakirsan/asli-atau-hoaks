<script setup>
// Satu ronde latihan antar-Polres: media + klaim yang menyertainya → tiap Polres angkat kartu → buka.
// Tiga kemungkinan jawaban (sesuai pertanyaan inti, bukan sekadar "AI atau bukan"):
//   'asli' = asli & klaim benar · 'ai' = dibuat/diubah AI · 'klaim' = gambar asli, klaimnya salah.
// Petunjuk tanpa x/y = temuan di luar gambar (data file, konteks): lingkaran putus-putus + label "di luar gambar".
// Per klik (frontmatter `clicks: titik.length + 2`):
//   1 = jawaban terbuka · 2..n+1 = petunjuk ke-n (penanda di media + catatan) · n+2 = cara cek tercepat.
// Ekspor (isPrintMode): semua tampil, video diganti poster (src).
import { computed, ref, watch } from 'vue'
import { useIsSlideActive, useNav, useSlideContext } from '@slidev/client'

const props = defineProps({
  src: String, video: String,
  klaim: { type: String, required: true },   // teks yang beredar bersama media
  asal: { type: String, default: 'pesan diteruskan · grup WhatsApp' },
  jawab: { type: String, required: true },   // 'asli' | 'ai' | 'klaim'
  titik: { type: Array, required: true },    // [{ x, y, judul, ket }] — x/y persen; tanpa x = catatan saja
  cara: String,                              // cara cek tercepat
  tinggi: { type: Number, default: 400 },
  rasio: { type: Number, default: 1.5 },
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

const pilihan = [
  { id: 'asli', nama: 'asli', ket: 'gambar dan klaimnya benar', warna: '#0b7a6e' },
  { id: 'klaim', nama: 'asli, klaimnya salah', ket: 'waktu, tempat, atau ceritanya dipelintir', warna: '#a86b00' },
  { id: 'ai', nama: 'buatan AI', ket: 'dibuat atau diubah dengan AI', warna: '#c0392b' },
]
const buka = computed(() => k.value >= 1)
const warnaJawab = computed(() => pilihan.find((p) => p.id === props.jawab)?.warna)
</script>

<template>
  <p class="klaim"><span class="asal">{{ asal }}</span>“{{ klaim }}”</p>
  <div class="ronde">
    <figure :style="{ width: lebar + 'px' }">
      <div class="media" :style="{ height: tinggi + 'px', boxShadow: buka ? `0 0 0 3px ${warnaJawab}` : 'none' }">
        <video v-if="pakaiVideo" ref="vid" :src="base(video)" :poster="base(src)" muted loop playsinline preload="auto" />
        <img v-else :src="base(src)" alt="">
        <template v-for="(t, i) in titik" :key="i">
          <span v-if="t.x != null" class="penanda" :class="{ ya: k > i + 1 }" :style="{ left: t.x + '%', top: t.y + '%', boxShadow: `0 0 0 3px ${warnaJawab}` }">{{ i + 1 }}</span>
        </template>
      </div>
      <figcaption v-if="kredit">{{ kredit }}</figcaption>
    </figure>

    <div class="kanan">
      <div class="pilihan">
        <div v-for="p in pilihan" :key="p.id" class="opsi"
             :class="{ benar: buka && p.id === jawab, redup: buka && p.id !== jawab }"
             :style="{ '--w': p.warna }">
          <span class="nama">{{ p.nama }}</span>
          <span class="ket">{{ p.ket }}</span>
        </div>
      </div>

      <ol class="catatan">
        <li v-for="(t, i) in titik" :key="i" :class="{ ya: k > i + 1 }">
          <span class="no" :class="{ luar: t.x == null }" :style="{ borderColor: warnaJawab, color: warnaJawab }">{{ i + 1 }}</span>
          <div>
            <p class="judul">{{ t.judul }}<span v-if="t.x == null" class="tag-luar">di luar gambar</span></p>
            <p class="ket">{{ t.ket }}</p>
          </div>
        </li>
      </ol>

      <p v-if="cara" class="cara" :class="{ ya: k >= titik.length + 2 }">
        <span class="label-kolom">cara cek tercepat</span>{{ cara }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.ronde { display: flex; gap: 40px; align-items: flex-start; }
figure { margin: 0; flex: none; }
.klaim { margin: 0 0 12px; max-width: 1000px; font-size: 20px; font-weight: 700; line-height: 1.3; color: #10131a; }
.asal { display: block; font-family: 'JetBrains Mono', monospace; font-size: 12px; font-weight: 400; color: #7b8190; margin-bottom: 2px; }
.media { position: relative; border-radius: 14px; overflow: hidden; background: #10131a; transition: box-shadow .4s ease; }
.media img, .media video { width: 100%; height: 100%; object-fit: cover; display: block; }
figcaption { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #7b8190; margin-top: 6px; line-height: 1.35; }
.penanda { position: absolute; transform: translate(-50%, -50%) scale(.6); width: 32px; height: 32px; border-radius: 50%; background: #fff; color: #10131a;
  font-weight: 800; font-size: 15px; display: flex; align-items: center; justify-content: center; opacity: 0;
  transition: opacity .35s ease, transform .45s cubic-bezier(.2,1.4,.4,1); }
.penanda.ya { opacity: 1; transform: translate(-50%, -50%) scale(1); }

.kanan { flex: 1; min-width: 0; }
/* Tiga jawaban berjajar; jawaban benar = garis atas berwarna + nama berwarna (pola Kuis), tanpa kotak/latar. */
.pilihan { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
.opsi { padding-top: 10px; border-top: 3px solid #e1e4ea; transition: opacity .4s ease, border-color .4s ease; }
.opsi .nama { display: block; font-family: 'JetBrains Mono', monospace; font-size: 15px; color: #10131a; }
.opsi .ket { display: block; font-size: 13.5px; line-height: 1.35; color: #7b8190; margin-top: 3px; }
.opsi.benar { border-top-color: var(--w); }
.opsi.benar .nama { color: var(--w); font-weight: 700; }
.opsi.redup { opacity: .3; }

.catatan { list-style: none; padding: 0; margin: 22px 0 0; }
.catatan li { display: grid; grid-template-columns: 34px 1fr; gap: 12px; padding: 8px 0; margin: 0; opacity: 0; transform: translateY(6px);
  transition: opacity .4s ease, transform .4s ease; }
.catatan li::before { display: none; }
.catatan li.ya { opacity: 1; transform: none; }
.catatan .no { width: 26px; height: 26px; border-radius: 50%; border: 2px solid; font-weight: 800; font-size: 13px; display: flex; align-items: center; justify-content: center; }
.catatan .no.luar { border-style: dashed; }
.tag-luar { font-family: 'JetBrains Mono', monospace; font-size: 13px; font-weight: 400; color: #7b8190; margin-left: 10px; letter-spacing: 0; }
.catatan p { margin: 0; }
.judul { font-weight: 800; font-size: 18px; line-height: 1.25; color: #10131a; }
.catatan .ket { font-size: 15px; line-height: 1.4; color: #4a5160; margin-top: 2px !important; }
.cara { margin: 12px 0 0; padding-top: 10px; border-top: 1px solid #e1e4ea; font-size: 16px; line-height: 1.4; color: #10131a;
  opacity: 0; transition: opacity .4s ease; }
.cara.ya { opacity: 1; }
.cara .label-kolom { display: block; margin-bottom: 2px; }
@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }
</style>
