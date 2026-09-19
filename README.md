# nefusoft-update

Manifest pembaruan untuk APK **Nefusoft**. Aplikasi membacanya sekali saat dibuka.

**URL yang dibaca aplikasi:**

```
https://raw.githubusercontent.com/HiuraKiyowoo/nefusoft-update/main/update.json
```

## Isi `update.json`

```json
{
  "versionCode": 21,
  "versionName": "2.1",
  "mandatory": false,
  "title": "Update Tersedia",
  "changelog": ["poin 1", "poin 2"],
  "apkUrl": "https://.../nefusoft.apk",
  "sizeMb": 14.3,
  "publishedAt": "2026-09-19"
}
```

| Field | Arti |
|---|---|
| `versionCode` | **Penting.** Harus **lebih besar** dari versionCode APK terpasang supaya dialog muncul. Sama atau lebih kecil = tidak ada dialog. |
| `versionName` | Ditampilkan di dialog (mis. `2.1`). |
| `mandatory` | `true` = tombol "NANTI" hilang, user wajib update. `false` = bisa di-skip. |
| `title` | Judul dialog. |
| `changelog` | Daftar poin "yang baru". |
| `apkUrl` | Tautan unduhan APK. Boleh GitHub Releases, CDN, atau server sendiri. |
| `sizeMb` | Ditampilkan sebagai info ukuran. |
| `publishedAt` | Tanggal rilis (info saja). |

## Cara merilis versi baru

1. Naikkan `versionCode` di `app/build.gradle.kts` (mis. 20 → 21) dan `versionName` (2.0 → 2.1).
2. Build APK rilis.
3. Buat rilis GitHub di repo ini dengan aset bernama `nefusoft.apk`
   (nama itu yang dipakai `apkUrl` di atas, lewat `/releases/latest/download/`).
4. Ubah `update.json`: naikkan `versionCode`, isi `changelog`, perbarui `publishedAt`.
5. Commit + push. Semua pengguna akan melihat dialog saat membuka aplikasi.

## Catatan

- Kalau `versionCode` di JSON **tidak lebih besar**, aplikasi langsung masuk tanpa dialog.
- Kalau file tidak bisa diambil (tidak ada internet), aplikasi tetap berjalan normal.
- Jangan menurunkan `versionCode` — pengguna yang sudah versi baru tidak akan diminta update lagi, itu memang diinginkan.
