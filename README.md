# ProFighter by ProKuiz 👊

Game bertarung gaya arked — **6 pahlawan original Nusantara**, **Lawan Bot 4 level**, **Lawan Online 1v1** dengan rating, pangkat & ranking, dan mod **Latihan**.
Konsep sama macam ProChess/ProSudoku: APK buka versi live di GitHub Pages → **kemas kini automatik tanpa download APK baru**.

## Pahlawan
| Pahlawan | Gaya | ✨ Khas | ⚡ Super |
|---|---|---|---|
| JEBAT | Pendekar Silat (seimbang) | Gelombang Keris | Amukan Jebat |
| MAWAR | Srikandi Pantas | Tendangan Puting Beliung | Taufan Mawar |
| BADANG | Gergasi Perkasa | Hentakan Bumi | Batu Gergasi |
| KILAT | Ninja Petir | Langkah Kilat (muncul di belakang lawan) | Petir Seribu |
| NAGA | Pahlawan Api | Bola Api | Nafas Naga |
| MEKA-X | Robot Wira | Tumbukan Roket | Laser Meka |

## Level
- **Bot:** Mudah ★ · Sederhana ★★ · Sukar ★★★ · Juara 👑 (dibuka selepas menang level Sukar)
- **Pemain:** Level (Lv) naik dengan XP — menang bot / online beri XP
- **Online:** Rating ELO + pangkat 🥉 Gangsa → 🥈 Perak (1100) → 🥇 Emas (1250) → 💠 Platinum (1400) → 💎 Berlian (1600) → 👑 Legenda (1800). "Cari Lawan Setara" padankan rating yang hampir sama.

## Kawalan
Joystick kiri (gerak / ⬆ lompat / ⬇ tunduk) · 👊 Tumbuk · 🦵 Tendang · 🛡️ Tahan (atau tolak ke belakang) · ✨ Khas · ⚡ Super (meter penuh).
Kombo: 👊 → 👊 → 🦵 → ✨. Papan kekunci PC: A/D/W/S, J tumbuk, K tendang, L khas, O super, I tahan.

## Grafik 3D
Pahlawan & pentas dilukis dalam **3D sebenar** (enjin WebGL sendiri dalam `index.html`, tiada library luar — ringan & boleh main offline): badan berlampu gaya kartun dengan garis hitam, pentas 3D dengan lantai, pokok/tiang/batu & latar jauh, kamera zum ikut jarak pemain dan fokus semasa SUPER.
Phone lama/lambat: **Tetapan → Grafik 3D → matikan** untuk guna mod 2D ringan. Jika phone tak sokong WebGL, app tukar ke 2D sendiri.

## Potret AI realistik (pilihan)
Letak 6 gambar potret dalam folder `img/` (`jebat.jpg`, `mawar.jpg`, `badang.jpg`, `kilat.jpg`, `naga.jpg`, `meka.jpg`). Prompt siap ada dalam **`PROMPT_POTRET.md`**.
Potret dipapar di skrin pilih pahlawan, skrin **VS** sebelum bertarung, bar nyawa, skrin SUPER dan skrin menang/kalah. Tiada gambar = guna potret 3D. Selepas tukar gambar, naikkan `APP_VERSION` supaya gambar baru dimuat.

## Ciri lain
BM | EN · keyboard dalam app · butang back Android + pop up keluar · skrin melintang (landscape) · pusingan terbaik 3 · kombo, K.O., PERFECT · bunyi & getaran · PWA iPhone · halaman offline · auto update.

## Setup (sekali sahaja)
1. **Repo GitHub `alemmaxx/ProFighter`** (Public) → upload semua fail ini ke branch `main` (termasuk `.github`, `.nojekyll`).
2. **GitHub Pages**: Settings → Pages → *Deploy from a branch* → `main` / `(root)` → Save.
   App hidup di `https://alemmaxx.github.io/ProFighter/`
3. **Secret** `KEYSTORE_BASE64` (Settings → Secrets and variables → Actions) — isi sama macam ProSudoku/ProChess.
4. **Firebase** (projek `prokuiz-aplikasi-b518a`, sama dengan ProChess):
   - Authentication → Anonymous → sepatutnya dah **Enable**
   - **Firestore Database → Rules** → ganti dengan isi fail `firestore.rules` → **Publish**
     (fail ini = rules ProSudoku + ProChess sedia ada + blok ProFighter; app lain tak terjejas)
5. Tab **Actions** → build siap → **Releases** → muat turun `ProFighter.apk` → pasang.

## Online — macam mana ia berfungsi
- Firebase digunakan untuk cari lawan, bilik kod, ajakan, rating & ranking (koleksi `fight_*`).
- Semasa bertarung, dua phone disambung **terus (P2P, WebRTC)** — laju & tak guna kuota Firestore.
- Kalau rangkaian tak benarkan sambungan terus, app automatik tukar ke **Relay** melalui Firestore (sedikit lambat, tapi masih boleh main). Label ⚡ P2P / ☁️ Relay dipapar bawah jam.

## Kemas kini app selepas ini
1. Edit `index.html` → **naikkan `APP_VERSION`** (cth `'1.0.0'` → `'1.0.1'`).
2. Push ke `main`. Dalam beberapa minit, app pengguna tunjuk bar **Kemas Kini** berkelip → tekan → siap.
   APK baru hanya perlu kalau tukar `capacitor.config.json` / ikon / plugin.

## Password admin padam ranking
Sama dengan ProSudoku/ProChess (`adminPassword()` dalam `firestore.rules`). ProFighter guna dokumen `config/fight`, jadi padam ranking ProFighter tak kacau app lain.

## Struktur
| Fail | Fungsi |
|---|---|
| `index.html` | Seluruh game (enjin, pahlawan, bot, online) |
| `sw.js`, `manifest.webmanifest`, `icons/` | PWA / iPhone / cache offline |
| `offline.html` | Skrin "Tiada Internet" dalam APK |
| `capacitor.config.json` | APK buka `https://alemmaxx.github.io/ProFighter/` |
| `firestore.rules` | Rules gabungan ProSudoku + ProChess + ProFighter |
| `.github/workflows/build-apk.yml` | Build APK (landscape, skrin penuh) + release |
