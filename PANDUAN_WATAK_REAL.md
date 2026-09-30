# Panduan Watak Realistik — ProFighter

Dua cara untuk jadikan pahlawan yang bertarung nampak "real". **Cara A sudah disokong dalam app (v1.7.0)** — cuma letak gambar dalam folder yang betul.

---

## CARA A — Gambar pose dari ChatGPT (sprite)

### Struktur fail
Letak gambar PNG dalam folder ikut nama pahlawan (huruf kecil):

```
img/jebat/idle.png   img/jebat/punch.png   img/jebat/kick.png ...
img/mawar/...   img/badang/...   img/kilat/...   img/naga/...   img/meka/...
```

| Fail | Pose | Wajib? |
|---|---|---|
| `idle.png` | Berdiri kuda-kuda | **WAJIB** (tanpanya app guna 3D) |
| `punch.png` | Tumbuk | Sangat digalakkan |
| `kick.png` | Tendang | Sangat digalakkan |
| `hit.png` | Kena pukul | Digalakkan |
| `down.png` | Jatuh terbaring | Digalakkan |
| `block.png` | Menahan | Pilihan |
| `walk.png` | Berjalan | Pilihan |
| `crouch.png` | Tunduk | Pilihan |
| `jump.png` | Melompat | Pilihan |
| `win.png` | Menang | Pilihan |
| `special.png` | Jurus khas / super | Pilihan |

Pose yang tiada → app guna pose terdekat (contoh: tiada `walk` → guna `idle`).
App **buang latar hijau (#00FF00) atau putih polos secara automatik**, dan **tapak kaki sentiasa dijejakkan ke lantai**.

### Langkah di ChatGPT
1. Buka **satu perbualan baru untuk setiap pahlawan**.
2. Lampirkan potret pahlawan itu (contoh `img/jebat.jpg`) dan hantar **PROMPT UTAMA** di bawah.
3. Selepas itu hantar prompt pose **satu demi satu** (mula dengan IDLE).
4. Muat turun setiap gambar → namakan ikut jadual → upload ke `img/<pahlawan>/` di GitHub.
5. Naikkan `APP_VERSION` dalam `index.html` supaya phone muat gambar baru.

### PROMPT UTAMA (hantar sekali, bersama potret)
```
I am making a 2D fighting video game. The attached image is my character's reference.
I will ask you for several poses of THIS SAME character, one image per message.
Rules for EVERY image:
- exactly the same person: same face, same outfit, same colours, same body proportions as the reference
- FULL BODY visible from the top of the head to the feet, nothing cropped
- side view, the character faces to the RIGHT
- same camera distance and same zoom in every image, so the character is always the same size
- character centred, feet near the bottom of the image
- transparent background PNG (if transparency is not possible, use a plain solid pure green #00FF00 background)
- no floor, no ground shadow, no scenery, no text, no watermark
- photorealistic, cinematic lighting, sharp details
- square 1024x1024
Reply "ready" and wait for the first pose.
```

### PROMPT POSE (hantar satu demi satu)
```
Pose 1 – IDLE: fighting stance, fists raised in a guard, knees slightly bent, weight balanced, facing right.
```
```
Pose 2 – PUNCH: powerful straight punch, the front arm fully extended forward to the right with a clenched fist, body leaning into the punch.
```
```
Pose 3 – KICK: high side kick, the front leg fully extended straight forward to the right at waist height, standing on the back leg, arms in guard.
```
```
Pose 4 – HIT: getting hit in the face, head snapped back, body leaning backwards, pained expression, arms loose.
```
```
Pose 5 – DOWN: knocked out, lying flat on the back on the ground, body horizontal, head on the LEFT and feet on the RIGHT.
```
```
Pose 6 – BLOCK: blocking, both forearms raised and crossed in front of the face, bracing.
```
```
Pose 7 – WALK: stepping forward mid-stride towards the right, guard up.
```
```
Pose 8 – CROUCH: crouching low, knees deeply bent, guard up.
```
```
Pose 9 – JUMP: in mid-air jump, knees tucked up, fists raised, whole body visible.
```
```
Pose 10 – WIN: victory pose, one fist raised high to the sky, proud expression.
```
**Pose 11 – SPECIAL** (ikut pahlawan):
- **Jebat:** `Pose 11 – SPECIAL: both palms thrust forward to the right, a golden glowing crescent-shaped energy wave forming at the hands.`
- **Mawar:** `Pose 11 – SPECIAL: spinning roundhouse kick, leg extended, pink rose petals swirling around.`
- **Badang:** `Pose 11 – SPECIAL: both fists raised high above the head, about to smash the ground with huge force.`
- **Kilat:** `Pose 11 – SPECIAL: dashing lunge punch to the right, blue electric lightning crackling around the fist.`
- **Naga:** `Pose 11 – SPECIAL: both palms pushed forward to the right, shooting a blazing fireball, flames around the hands.`
- **Meka-X:** `Pose 11 – SPECIAL: arm extended to the right firing a rocket fist, glowing green thrusters.`

### Tips supaya hasil kemas
- Kalau rupa berubah: balas `Keep EXACTLY the same character as Pose 1 — same face, same outfit. Regenerate.`
- Kalau badan terpotong: `Show the full body including both feet, zoom out a little. Regenerate.`
- Kalau saiz berubah: `Same size and camera distance as Pose 1.`
- Pastikan semua menghadap **KANAN** (app terbalikkan sendiri untuk pemain kanan).
- Mulakan dengan 1 pahlawan dan 3 pose (`idle`, `punch`, `kick`) untuk cuba dulu.
- Tetapan → **Watak gambar realistik** boleh ON/OFF (muncul bila ada gambar pose).

---

## CARA B — Model 3D realistik (Meshy.ai)

> Hasil paling mirip game sebenar, tetapi fail besar (3–15 MB setiap pahlawan). Selepas anda dapat fail `.glb`, hantar kepada saya untuk dipasang dalam enjin game.

1. **Sediakan gambar seluruh badan menghadap depan.** Di ChatGPT (bersama potret):
   ```
   Full body of this exact same character, standing straight in an A-pose (arms slightly away from the body), facing the camera, from head to feet, plain white background, photorealistic, 1024x1024.
   ```
2. Pergi ke **meshy.ai** → daftar (Google login) → **Image to 3D** → upload gambar A-pose itu.
3. Tetapan: **Topology: Triangle**, **Polycount: 10k–30k** (lebih kecil = lebih laju di phone), **Texture: ON** → *Generate*. Pilih hasil paling baik.
4. Klik **Animate / Rig** → pilih **Humanoid** → letak titik (dagu, pergelangan, siku, lutut) ikut arahan → *Next*.
5. Pilih animasi: **Idle (fighting)**, **Walk**, **Punch**, **Kick**, **Hit Reaction**, **Death / Knockdown**, **Victory**, **Block**.
6. **Download** → format **GLB**, tekstur **1024** (jangan 4K) → satu fail `.glb` dengan semua animasi.
7. Ulang untuk 6 pahlawan → namakan `jebat.glb`, `mawar.glb`, `badang.glb`, `kilat.glb`, `naga.glb`, `meka.glb` → hantar kepada saya.

⚠️ Pakej percuma Meshy ada had kredit sebulan & mungkin perlu langganan untuk rig/animasi dan muat turun.
