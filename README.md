# 🏰 The Enchanted Chess — Kinematik 3D Sehrli Shaxmat O'yini








> **"Qadimiy yerosti qasrining zulmatida 64 ta marmar katak va 32 ta tirik tosh jangchi sizning buyrug'ingizni kutmoqda..."**

**The Enchanted Chess** — bu *Harry Potter and the Philosopher's Stone* filmidagi afsonaviy gigant sehrli shaxmat jangidan ilhomlangan, to'liq o'ynash mumkin bo'lgan **3D kinematik fantaziya shaxmat veb-ilovasi**. O'yin oddiy 2D taxta yoki statik sahna emas, balki haqiqiy shaxmat qoidalari, sun'iy intellekt (AI), 6 bosqichli kinematik jang sahnalari, fizikaga asoslangan tosh parchalanish effektlari va protsessual Web Audio ovoz tizimini o'zida mujassam etgan interaktiv 3D dunyodir.



## 🌟 Loyihaning Asosiy Imkoniyatlari

| Yo'nalish | Asosiy Xususiyatlar | Texnik Yechim |
| :--- | :--- | :--- |
| **Gotik Qasr Muhiti** | 16 ta baland ustunlar, oy nuri shu'lalari, 8 ta yonib turgan mash'ala va atrofda sochilgan qadimiy haykal bo'laklari | `THREE.FogExp2`, dinamik `PointLight` va `SpotLight` soyalar, uchuvchi chang zarralari (`THREE.Points`) |
| **Monumental 8×8 Shaxmat Taxtasi** | Oq alebastr va to'q ko'k obsidian marmar kataklar, atrofi qadimiy runik belgilar bilan o'ralgan | Protsessual `CanvasTexture` PBR materiallar (`bumpMap`, `roughness`, `metalness`) |
| **32 ta Tirik Tosh Jangchilar** | Har bir sipoh o'zining nafas olishi, qurol tutishi, og'ir qadamlari va jang uslubiga ega | Bo'g'inlarga ajratilgan (`THREE.Group`) 3D iyerarxik haykallar (`bodyPivot`, `headGroup`, `weaponPivot`) |
| **6 Bosqichli Kinematik Jang** | Sipohni urib olishda maxsus kamera rakursi, yaqinlashish, zarba va toshning 36+ bo'lakka parchalanishi | `GSAP` animatsion taymlaynlari + 3D rigid-body/impuls fizikasi (gravitatsiya va sakrash) |
| **To'liq Shaxmat Qoidalari va AI** | Shoh, Mot, Pat, Rokirovka, En Passant, Piyoda o'zgarishi va 3 darajali AI raqib | `chess.js` + Minimax va Alfa-Beta kesish (`Alpha-Beta Pruning`) algoritmi |
| **Kinematik Ovoz Dizayni** | Qasr g'uvillashi, shamol, og'ir tosh qadamlar, qilich/bolg'a zarbasi, sehrli nur va tosh sinishi | Tashqi MP3 fayllarsiz toza **Web Audio API** ko'p kanalli sintezatori |

## 🗿 Tirik 3D Tosh Jangchilar Kodeksi (Sipohlar Tavsifi)

O'yindagi har bir shaxmat donasi oddiy shakl emas, balki o'z xarakteri, vazni va jangovar animatsiyasiga ega bo'lgan qadimiy tosh jangchidir:



| Belgisi | Sipoh Nomi | Jangchi Sinfi | Tashqi Ko'rinishi va Quroli | Harakat va Hujum Uslubi |
| :---: | :--- | :--- | :--- | :--- |
| **♙ / ♟** | **Piyoda (Pawn)** | *Stone Soldier* (Tosh Askar) | Zirhli o'rta asr piyoda askari, chap qo'lida dumaloq qalqon, o'ng qo'lida keng qilich | Og'ir qadamlar bilan oldinga yuradi; raqibni yuqoridan qilich bilan keskin chopib parchalaydi |
| **♘ / ♞** | **Ot (Knight)** | *Armored Horse Rider* (Zirhli Suvoriy) | Zirhlangan jangovar tulpor ustidagi nayzali ritsar | Oyoqqa kalkib, boshqa sipohlar ustidan parabolik yoy bo'ylab sakrab o'tadi va nayza sanchadi |
| **♗ / ♝** | **Fil (Bishop)** | *Magical Guardian* (Sehrli Qo'riqchi) | Uzun rido va toj kiygan mistik ruhoniy, uchida aylanuvchi kristall sharli hassa tutadi | Diagonal bo'ylab sirpanib harakatlanadi; hassasidan kuchli sehrli nur yo'llab raqibni portlatadi |
| **♖ / ♜** | **Rux / To'ra (Rook)** | *Fortress Guardian* (Qal'a Golemi) |Yelkalarida qal'a tishlari bo'lgan ulkan tosh dev, qo'lida ikki qo'lli ulkan tosh bolg'a | Har qadamida zaminni titratadi; jangda bolg'asi bilan yuqoridan zarba berib ekranni silkitadi |
| **♕ / ♛** | **Farzin (Queen)** | *Supreme Magical Warrior* (Oliy Jangchi Qirolicha) | Qanotli zirh, toj va boshida aylanuvchi runik halqaga ega qudratli malika | Nafis va salobatli harakatlanadi; oltin-moviy sehrli to'lqin va saltanat tig'i bilan yakson qiladi |
| **♔ / ♚** | **Shoh (King)** | *Royal Stone Guardian* (Qirollik Qo'riqchisi) | Imperator toji kiygan eng baland haykal, oldida ikki qo'lli qirollik qilichini tutib turadi | Salobatli qadam tashlaydi; **Shoh** holatida qizil runalar yonadi, **Mot** bo'lganda tiz cho'kib qilichini tushiradi |

## ⚔️ 6 Bosqichli Kinematik Jang Tizimi (Capture Sequence)

O'yinning eng hayajonli qismi — raqib sipohini urib olish jarayonidir. Oddiy shaxmat o'yinlaridek dona shunchaki g'oyib bo'lmaydi, balki haqiqiy film sahnasi ishga tushadi:



1. **1-Bosqich — Tanishuv va Himoya (Recognition):** Hujum qiluvchi jangchi nishon tomonga buriladi. Himoyalanuvchi tosh jangchi ham xavfni sezib, hujumchiga yuzlanadi va qalqoni yoki qurolini himoya holatiga keltiradi. Zaldagi yorug'lik kuchayadi.
2. **2-Bosqich — Yaqinlashuv (Approach):** Hujumchi o'z vazniga mos ovoz va qadamlar bilan (Ot sakrab, Rux yerni titratib, Fil sirpanib) raqib katagining oldigacha yurib boradi.
3. **3-Bosqich — Kinematik Kamera (Director Camera):** Kamera avtomatik ravishda pastki dramatik rakursga (Close-Up Tracking Shot) o'tadi va ekranning yuqori-pastki qismida qora *Letterbox* kino chiziqlari paydo bo'ladi.
4. **4-Bosqich — Jangovar Zarba (Attack):** Hujumchi o'z sinfiga xos bo'lgan maxsus qurol yoki sehr zarbasini amalga oshiradi.
5. **5-Bosqich — Tosh Parchalanishi (Physics Destruction):** Mag'lub bo'lgan haykal **36 ta uchburchak va ko'pburchakli 3D tosh bo'laklariga** (`THREE.DodecahedronGeometry`) bo'linib ketadi. Har bir bo'lak gravitatsiya, burchak tezligi va taxtaga urilib sakrash fizikasi bilan atrofga sochiladi, uchqunlar chiqadi va kamera titraydi.
6. **6-Bosqich — O'yinga Qaytish (Return to Gameplay):** G'olib jangchi egallangan katak markaziga qadam qo'yadi, kamera silliq tarzda o'yinchining strategik ko'rinishiga qaytadi va navbat keyingi yurishga o'tadi.

> **💡 Eslatma:** Agar tezkor o'yinni xohlasangiz, jang paytida ekrandagi **`Skip Clash ⏭`** tugmasini (yoki `Space` klavishini) bosishingiz, yoxud pastki paneldagi **`Fast Combat`** belgisini yoqib qo'yishingiz mumkin.

## 🎬 Ochilish (Intro) va Mot (Checkmate) Sahnalari

### 1. 12 Soniyalik Ochilish Kinematikasi (Opening Cinematic)
O'yin ilk bor ishga tushganda real vaqtda 3D dvigatel yordamida 4 qismli kirish sahnasi namoyish etiladi:
- **0–3 soniya (`I. The Subterranean Gothic Chamber`):** Tumanli yerosti qasri va miltillovchi mash'alalar ko'rinadi.
- **3–6 soniya (`II. Passage Through the Pillars`):** Kamera ulkan gotik ustunlar orasidan suzib o'tib, markaziy shaxmat taxtasiga yaqinlashadi.
- **6–9 soniya (`III. Awakening of the Stone Warriors`):** 32 ta tosh jangchi uyg'onadi, ko'zlaridagi runalar chaqnaydi.
- **9–12 soniya (`IV. The Trial Begins`):** Kamera yuqoriga ko'tarilib, butun jang maydonini va **"THE ENCHANTED CHESS"** asosiy menyusini ochib beradi.

### 2. Mot va G'alaba Sahnasi (Checkmate Cinematic)
O'yin qonuniy **Mot (Checkmate)** bilan yakunlanganda:
- Mag'lub bo'lgan **Shoh** hech qachon oddiy sipoh kabi sindirilmaydi.
- Kamera yutqazgan Shohga qaratiladi va qizil projektor nuri tushadi.
- Mag'lub Shoh sekin **tiz cho'kadi** va ikki qo'lli qirollik qilichini yerga tushiradi.
- G'olib armiyaning barcha tirik qolgan jangchilari qurollarini osmonga ko'tarib tantana holatiga kiradi va tantanali fanfara yangraydi.

## 🎮 O'yin Rejimlari va Boshqaruv Qo'llanmasi

### O'yin Rejimlari
- **PLAY VS AI (Sun'iy Intellektga Qarshi):**
  - **Easy (Novice Stone):** Yangi o'rganuvchilar uchun qulay, taktik va tasodifiy yurishlar uyg'unligi.
  - **Medium (Castle Tactician):** 2 qadam chuqurlikdagi *Minimax + Pozitsion jadvallar* asosida o'ynaydigan o'rta darajali raqib.
  - **Hard (Grandmaster Archmage):** 3 qadam chuqurlikdagi *Alpha-Beta Pruning* va hujumlarni ustuvor saralash algoritmi bilan jihozlangan kuchli raqib.
  - **Armiya Tanlovi:** Oq (*Alabaster Stone*) yoki Qora (*Obsidian Marble*) tosh qo'shinni tanlab o'ynash mumkin.
- **TWO PLAYERS (Ikki O'yinchi):** Bitta qurilmada do'stingiz bilan navbatma-navbat o'ynash rejimi. Har yurishdan so'ng kamerani avtomatik ravishda navbatdagi o'yinchi tomonga aylantirish (`Auto-Rotate Camera`) funksiyasi mavjud.
- **Vaqt Nazorati (Time Control):** `10 Min Rapid`, `5 Min Blitz`, `15 Min Classical` yoki vaqt cheklovisiz `Untimed Immortal` rejimlari.

### Sichqoncha, Sensorli Ekran va Klaviatura Boshqaruvi

| Amal | Sichqoncha / Sensorli Ekran | Klaviatura Tugmasi |
| :--- | :--- | :---: |
| **Sipohni tanlash va yurish** | Sipoh ustiga bosing $\rightarrow$ yongan katakka bosing | — |
| **Kamerani aylantirish (Orbit)** | Bo'sh joyda chap tugmani yoki istalgan joyda o'ng tugmani bosib suring | Pastki paneldagi `⟲` / `⟳` |
| **Yaqinlashtirish / Uzoqlashtirish** | Sichqoncha g'ildiragini aylantiring (Scroll) | Pastki paneldagi `＋` / `－` |
| **Kamera rakursini almashtirish** | Yuqori paneldagi `🎥 Commander View` tugmasi | `C` |
| **Taxtani 180° aylantirish (Flip)** | Yuqori paneldagi `🔄 Flip` tugmasi | `F` |
| **Yurishni orqaga qaytarish (Undo)** | Yuqori paneldagi `↩ Undo` tugmasi | `Z` |
| **Ovozni o'chirish / yoqish (Mute)** | Yuqori paneldagi `🔊` tugmasi | `M` |
| **Intro yoki Jang sahnasini o'tkazib yuborish** | `Skip Intro ⏭` / `Skip Clash ⏭` tugmasi | `Space` |

## 🛠️ Texnologik Stek va Arxitektura

Loyiha zamonaviy veb-grafika va o'yin muhandisligi standartlari asosida qurilgan:

| Qatlam | Texnologiya | Vazifasi |
| :--- | :--- | :--- |
| **3D Render va Sahna** | `Three.js (r128)` WebGL | Gotik qasr geometriyasi, PBR materiallar, dinamik chiroqlar, soyalar (`PCFSoftShadowMap`) va `ACESFilmicToneMapping` |
| **Kinematik Animatsiyalar** | `GSAP 3.12` | Sipohlarning silliq burilishi, sakrashi, qurol zarbalari va kamera harakat trayektoriyalari |
| **Shaxmat Qoidalari Dvigateli** | `chess.js (0.10.3)` | Barcha qonuniy yurishlar, Rokirovka, En Passant, Piyoda o'zgarishi, Shoh/Mot/Pat va 3 marta takrorlanish nazorati |
| **Sun'iy Intellekt (AI)** | `Minimax + Alpha-Beta` | Sipohlar qiymati (`P=100, N=320, B=330, R=500, Q=900, K=20000`) va pozitsion katak jadvallari (`PST`) asosida baholash |
| **Audio Sintezator** | `Web Audio API` | Ossillyatorlar (`sine`, `triangle`, `sawtooth`, `square`) va shovqin buferlari (`BiquadFilter`) orqali real vaqtda ovoz generatsiyasi |
| **Foydalanuvchi Interfeysi (HUD)** | `Tailwind CSS 3.4` + `Cinzel` | Obsidian oyna effektli (`backdrop-filter: blur`) menyular, Battle Chronicle yurishlar tarixi va Warrior Inspector |

## 📂 Loyiha Fayllari Tuzilmasi

Loyiha ikki xil shaklda taqdim etilgan: darhol brauzerda ochib o'ynash mumkin bo'lgan **yagona mustaqil HTML fayl** (`enchanted_wizard_chess.html`) hamda kengaytirish uchun mo'ljallangan **modulli Vite + TypeScript loyiha arxivi** (`enchanted-wizard-chess-project.zip`).

```text
enchanted-wizard-chess-project/
├── index.html                  # To'liq ishlaydigan 3D Wizard Chess ilovasi
├── package.json                # React, Three.js, R3F, GSAP, Chess.js paketlar ro'yxati
├── README.md                   # Loyiha bo'yicha to'liq qo'llanma va hujjat
├── assets/
│   └── screenshots/
│       └── wizard-chess-banner.png  # O'yinning kinematik banner tasviri
└── src/
    ├── systems/                # Shaxmat mantiqi, AI, Audio va Kamera tizimlari
    └── components/             # 3D Sahna, Sipohlar va HUD interfeys qismlari
```

## 🚀 O'rnatish va Ishga Tushirish Bo'yicha Qo'llanma

### 1-Usul: Hech qanday o'rnatishlarsiz to'g'ridan-to'g'ri ishga tushirish (Tavsiya etiladi)
`enchanted_wizard_chess.html` (yoki arxiv ichidagi `index.html`) faylini istalgan zamonaviy brauzerda (**Google Chrome, Edge, Firefox, Safari**) ikki marta bosib oching. Barcha 3D modellar, teksturalar va ovozlar protsessual ravishda kodning o'zida yaratilgani sababli lokal server talab qilinmaydi.

### 2-Usul: Lokal Server yoki Vite Muhitida Ishga Tushirish
Agar loyihani dasturchi sifatida tahrirlamoqchi yoki kengaytirmoqchi bo'lsangiz:

```bash
# 1. Loyiha arxivini oching va papkaga kiring
unzip enchanted-wizard-chess-project.zip -d enchanted-wizard-chess
cd enchanted-wizard-chess

# 2. Paketlarni o'rnating (Node.js 18+ talab etiladi)
npm install

# 3. Development serverni ishga tushiring
npm run dev
```

Shuningdek, Python o'rnatilgan bo'lsa, oddiy HTTP server orqali ham ochishingiz mumkin:

```bash
python3 -m http.server 8080
# Brauzerda: http://localhost:8080
```

## ⚙️ Grafik Sifat va Moslashuvchanlik Sozlamalari (`Chamber Settings`)

Turli quvvatdagi kompyuterlar va mobil qurilmalarda barqaror **60 FPS** ishlashini ta'minlash uchun o'yin ichidagi **⚙ Settings** oynasida quyidagi sozlamalar mavjud:
- **Ultra:** Yumshoq 2048×2048 soyalar, oy nuri ustunlari, uchuvchi chang zarralari va 36 bo'lakli to'liq tosh parchalanish fizikasi.
- **High:** Dinamik mash'alalar va soyalar yoqilgan muvozanatli rejim.
- **Performance (60 FPS Optimized):** Kuchsizroq GPU va mobil qurilmalar uchun soyalar hamda og'ir zarralar o'chirilgan tezkor rejim.
- **Reduced Motion & Screen Shake:** Ko'rish qulayligi uchun kamera silkinishini o'chirish va parchalarni kamaytirish imkoniyati.
