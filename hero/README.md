# Poster Hero (CDN)

Folder ini disajikan lewat jsDelivr:

```
https://cdn.jsdelivr.net/gh/HiuraKiyowoo/nefusoft-update@main/hero/<nama-berkas>
```

Aplikasi membaca `hero.json` saat beranda dibuka. Urutan prioritas gambar hero:

1. **CDN** (berkas ini) — bisa diganti kapan saja, tanpa rilis APK
2. poster yang **ditanam di APK**
3. gambar dari **API** (selalu ada)

## Ganti poster

1. Taruh gambar di folder ini: 16:9, ideal 1280×720, `.webp`/`.jpg`, < 300 KB.
2. Isi `hero.json`:
   - per anime → `"byId": { "one-piece": "https://cdn.jsdelivr.net/gh/.../one_piece.webp" }`
   - per urutan slide → `"byOrder": ["https://.../slot_1.webp", "https://.../slot_2.webp"]`
3. Commit + push. jsDelivr menyegarkan cache otomatis (±12 jam; untuk instan tambahkan `?v=2` di URL).

Id anime = bagian akhir URL-nya, misal `/anime/one-piece` → `one-piece`.
Kalau JSON rusak atau CDN mati, aplikasi diam-diam memakai gambar API — tidak pernah kosong.

## Sesudah push: segarkan cache jsDelivr

jsDelivr menyimpan cache untuk ref `@main` sampai ±12 jam. Kalau poster baru
belum muncul, paksa segarkan:

```bash
curl -s "https://purge.jsdelivr.net/gh/HiuraKiyowoo/nefusoft-update@main/hero/hero.json"
curl -s "https://purge.jsdelivr.net/gh/HiuraKiyowoo/nefusoft-update@main/hero/slot_2.webp"
```

Alternatif instan: panggil lewat commit sha, mis.
`https://cdn.jsdelivr.net/gh/HiuraKiyowoo/nefusoft-update@<sha-commit>/hero/slot_2.webp`

## Yang sudah terpasang

| berkas | isi |
|---|---|
| `slot_1.webp` | poster anti-judi "Sudah lah, JANGAN JUDI LAGI" (1280×720, 100 KB) |

Menambah slide: taruh `slot_2.webp`, `slot_3.webp`, … lalu tambahkan URL-nya ke
`byOrder` pada `hero.json`. Jumlah slide di beranda mengikuti jumlah isi
`byOrder`.
