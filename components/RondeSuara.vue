<script setup>
// Ronde suara: beberapa klip pesan suara (A, B, C…) — sebagian rekaman asli, sebagian kloning AI.
// Tiap klip: tombol putar + gelombang suara (dihitung dari file audio; kalau file belum ada → pesan path).
// Per klik (frontmatter `clicks: titik.length + 2`):
//   1..n = petunjuk ke-n (umum, tidak membocorkan jawaban) · n+1 = cara cek tercepat
//   n+2 = BARU jawaban per klip terbuka (sengaja paling akhir supaya tidak bocor kalau salah tekan).
// Ekspor (isPrintMode): jawaban + semua petunjuk tampil.
import { computed, onBeforeUnmount, onMounted, reactive, watch } from 'vue'
import { useIsSlideActive, useNav, useSlideContext } from '@slidev/client'

const props = defineProps({
  item: { type: Array, required: true },   // [{ src, jawab: 'asli'|'ai', isi }] — isi = ringkasan pesan (tampil setelah dibuka)
  asal: { type: String, default: 'pesan suara · WhatsApp' },
  klaim: { type: String, required: true },
  titik: { type: Array, default: () => [] }, // [{ judul, ket }]
  cara: String,
})
const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))
const buka = computed(() => k.value >= props.titik.length + 2)
const base = (p) => p?.startsWith('/') ? import.meta.env.BASE_URL + p.slice(1) : p
const huruf = (i) => String.fromCharCode(65 + i)

const BATANG = 64
const st = reactive(props.item.map(() => ({ peaks: null, gagal: false, main: false, maju: 0, dur: 0 })))
const audio = props.item.map(() => null)

async function hitungGelombang(i) {
  try {
    const res = await fetch(base(props.item[i].src))
    if (!res.ok) throw new Error('tidak ada')
    const buf = await res.arrayBuffer()
    const ctx = new (window.AudioContext || window.webkitAudioContext)()
    const data = await ctx.decodeAudioData(buf)
    ctx.close()
    const ch = data.getChannelData(0)
    const blok = Math.floor(ch.length / BATANG)
    const peaks = []
    for (let b = 0; b < BATANG; b++) {
      let m = 0
      for (let j = b * blok; j < (b + 1) * blok; j += 16) m = Math.max(m, Math.abs(ch[j]))
      peaks.push(m)
    }
    const max = Math.max(...peaks) || 1
    st[i].peaks = peaks.map((p) => Math.max(0.08, p / max))
    st[i].dur = data.duration
  } catch { st[i].gagal = true }
}
onMounted(() => props.item.forEach((_, i) => hitungGelombang(i)))

function putar(i) {
  if (st[i].gagal) return
  audio.forEach((a, j) => { if (a && j !== i) { a.pause(); st[j].main = false } })
  if (!audio[i]) {
    const a = new Audio(base(props.item[i].src))
    a.ontimeupdate = () => { st[i].maju = a.duration ? a.currentTime / a.duration : 0 }
    a.onended = () => { st[i].main = false; st[i].maju = 0 }
    audio[i] = a
  }
  const a = audio[i]
  if (st[i].main) { a.pause(); st[i].main = false } else { a.play().catch(() => {}); st[i].main = true }
}
function hentikanSemua() { audio.forEach((a, j) => { if (a) { a.pause(); a.currentTime = 0; st[j].main = false; st[j].maju = 0 } }) }
const aktif = useIsSlideActive()
watch(aktif, (a) => { if (!a) hentikanSemua() })
onBeforeUnmount(hentikanSemua)

const warna = (j) => (j === 'ai' ? '#c0392b' : '#0b7a6e')
const detik = (d) => d ? `0:${String(Math.round(d)).padStart(2, '0')}` : ''
</script>

<template>
  <p class="klaim"><span class="asal">{{ asal }}</span>“{{ klaim }}”</p>
  <div class="suara">
    <div class="klip">
      <div v-for="(it, i) in item" :key="i" class="satu" :class="{ buka }" :style="{ '--w': warna(it.jawab) }">
        <span class="huruf">{{ huruf(i) }}</span>
        <button class="putar" :class="{ main: st[i].main }" :disabled="st[i].gagal" @click.stop="putar(i)" :aria-label="'Putar klip ' + huruf(i)">
          <svg v-if="!st[i].main" viewBox="0 0 24 24" width="18" height="18"><path d="M7 4.5v15l12.5-7.5z" fill="currentColor" /></svg>
          <svg v-else viewBox="0 0 24 24" width="18" height="18"><path d="M6.5 4.5h4v15h-4zM13.5 4.5h4v15h-4z" fill="currentColor" /></svg>
        </button>
        <div class="gelombang">
          <div v-if="st[i].gagal" class="kosong">audio {{ huruf(i) }} belum ada → public{{ it.src }}</div>
          <template v-else>
            <span v-for="(p, b) in (st[i].peaks || Array(BATANG).fill(0.15))" :key="b" class="batang"
                  :class="{ lewat: b / BATANG < st[i].maju }" :style="{ height: Math.round(p * 100) + '%' }" />
          </template>
        </div>
        <span class="durasi">{{ detik(st[i].dur) }}</span>
        <div class="jawab">
          <span class="label">{{ it.jawab === 'ai' ? 'kloning AI' : 'rekaman asli' }}</span>
          <span class="isi">{{ it.isi }}</span>
        </div>
      </div>
    </div>

    <div class="kanan">
      <ol class="catatan">
        <li v-for="(t, i) in titik" :key="i" :class="{ ya: k > i }">
          <span class="no">{{ i + 1 }}</span>
          <div><p class="judul">{{ t.judul }}</p><p class="ket">{{ t.ket }}</p></div>
        </li>
      </ol>
      <p v-if="cara" class="cara" :class="{ ya: k >= titik.length + 1 }">
        <span class="label-kolom">cara cek tercepat</span>{{ cara }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.klaim { margin: 0 0 14px; max-width: 1000px; font-size: 20px; font-weight: 700; line-height: 1.3; color: #10131a; }
.asal { display: block; font-family: 'JetBrains Mono', monospace; font-size: 12px; font-weight: 400; color: #7b8190; margin-bottom: 2px; }
.suara { display: flex; gap: 40px; align-items: flex-start; }
/* Tanpa kotak/latar: tiap klip = satu baris dipisah garis tipis; jawaban = gelombang berwarna + garis bawah + label mono. */
.klip { flex: none; width: 600px; }
.satu { display: grid; grid-template-columns: 34px 46px 1fr 44px; grid-template-rows: auto auto; column-gap: 14px; align-items: center;
  padding: 16px 0 14px; border-bottom: 1px solid #e1e4ea; }
.satu:first-child { border-top: 1px solid #e1e4ea; }
.huruf { font-weight: 800; font-size: 26px; line-height: 1; color: #10131a; }
.putar { width: 44px; height: 44px; border-radius: 50%; border: 1.5px solid #10131a; background: #fff; color: #10131a; display: flex;
  align-items: center; justify-content: center; cursor: pointer; padding: 0; transition: background .2s ease, color .2s ease; }
.putar.main { background: #10131a; color: #fff; }
.putar:disabled { opacity: .3; cursor: default; }
.gelombang { height: 52px; display: flex; align-items: center; gap: 3px; border-bottom: 2px solid transparent; transition: border-color .4s ease; }
.buka .gelombang { border-bottom-color: var(--w); }
.batang { flex: 1; min-height: 3px; border-radius: 2px; background: #cbd0d9; transition: background .15s ease; }
.batang.lewat { background: #10131a; }
.buka .batang { background: var(--w); opacity: .55; }
.buka .batang.lewat { opacity: 1; }
.buka .batang.lewat { background: var(--w); }
.kosong { font-family: 'JetBrains Mono', monospace; font-size: 12px; color: #7b8190; }
.durasi { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #7b8190; text-align: right; }
.jawab { grid-column: 3 / 5; display: flex; gap: 12px; align-items: baseline; margin-top: 6px; opacity: 0; transform: translateY(4px);
  transition: opacity .4s ease, transform .4s ease; }
.buka .jawab { opacity: 1; transform: none; }
.jawab .label { font-family: 'JetBrains Mono', monospace; font-size: 15px; font-weight: 700; color: var(--w); flex: none; }
.jawab .isi { font-size: 14px; color: #4a5160; }

.kanan { flex: 1; min-width: 0; }
.catatan { list-style: none; padding: 0; margin: 0; }
.catatan li { display: grid; grid-template-columns: 34px 1fr; gap: 12px; padding: 8px 0; margin: 0; opacity: 0; transform: translateY(6px);
  transition: opacity .4s ease, transform .4s ease; }
.catatan li::before { display: none; }
.catatan li.ya { opacity: 1; transform: none; }
.catatan .no { width: 26px; height: 26px; border-radius: 50%; border: 2px solid #c0392b; color: #c0392b; font-weight: 800; font-size: 13px;
  display: flex; align-items: center; justify-content: center; }
.catatan p { margin: 0; }
.judul { font-weight: 800; font-size: 18px; line-height: 1.25; color: #10131a; }
.catatan .ket { font-size: 15px; line-height: 1.4; color: #4a5160; margin-top: 2px !important; }
.cara { margin: 12px 0 0; padding-top: 10px; border-top: 1px solid #e1e4ea; font-size: 16px; line-height: 1.4; color: #10131a; opacity: 0; transition: opacity .4s ease; }
.cara.ya { opacity: 1; }
.cara .label-kolom { display: block; margin-bottom: 2px; }
@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }
</style>
