# Shajara — Telegram Mini App

Oilalar o'z shajarasini (ota-ona, bobo-buvi, farzandlar...) tuzib, butun daraxtni bitta ekranda ko'radigan Telegram mini ilovasi. Hozirgi bosqich — MVP: bitta statik `index.html`, ma'lumotlar qurilmaning o'zida (localStorage) saqlanadi, backend hali yo'q.

## Tuzilma

| Fayl | Vazifasi |
|---|---|
| `index.html` | Butun ilova: UI, SVG daraxt, pan/zoom, qarindoshlik nomlari, Telegram WebApp integratsiyasi |

Telegram integratsiyasi (`telegram-web-app.js`) himoyalangan: ilova oddiy brauzerda ham, Telegram ichida ham ishlaydi. Telegram ichida qo'shimcha:

- `expand()` — to'liq ekran
- `disableVerticalSwipes()` — daraxtni surganda ilova yopilib ketmaydi
- Telegram temasi (light/dark) ilova temasiga ulanadi
- **Back** tugmasi ochiq oynalarni (varaq/modal) yopadi
- Foydalanuvchining Telegram ismi onboardingga oldindan yoziladi

## Onlayn rejim

`index.html` dagi `API_DEFAULT` ga [shajara_api](https://github.com/JumayevIU/shajara_api) backendining HTTPS manzili yozilsa, ilova umumiy baza bilan ishlaydi: daraxt yaratish, taklif havolasi orqali qo'shilish, "Bu — men" belgilash. `API_DEFAULT` bo'sh qolsa — avvalgidek faqat qurilmaning o'zida (localStorage) saqlaydigan rejim.

Lokal sinov (Telegramsiz): `index.html?api=http://127.0.0.1:8000&dev=1:Ilhom` — `dev` parametri backendning lokal rejimidagi soxta foydalanuvchi.

## Lokal ishga tushirish

```bash
cd ~/Documents/projects/shajara
python3 -m http.server 8080
```

So'ng brauzerda: `http://localhost:8080`

## Botni yaratish (BotFather, ~5 daqiqa)

1. Telegramda **@BotFather** ni oching → `/newbot`
   - Nom: `Shajara`
   - Username: masalan `shajara_oila_bot` (bo'sh bo'lgani, `bot` bilan tugashi shart)
   - Qaytgan **token**ni saqlab qo'ying (hozircha kerak emas, backend bosqichida kerak bo'ladi)
2. `/newapp` → botingizni tanlang
   - Title: `Shajara`
   - Description: `Oilangiz shajarasini tuzing va butun daraxtni ko'ring`
   - Photo: 640×360 px rasm (keyin almashtirsa bo'ladi)
   - Demo GIF: *Skip*
   - **Web App URL**: hosting manzili (HTTPS shart)
   - Short name: `shajara`
   - Natija: `t.me/<bot_username>/shajara` — to'g'ridan-to'g'ri ochiladigan havola
3. Qo'shimcha (ixtiyoriy): `/mybots` → botni tanlang → **Bot Settings → Menu Button** → shu URL ni qo'ying — bot chatidagi pastki tugma ham ilovani ochadi.

> Mini app uchun server shart emas: BotFather'dagi URL to'g'ridan-to'g'ri statik sahifani ochadi. Bot tokeni faqat keyingi bosqichda (backend, xabarlar) ishlatiladi.

## Yo'l xaritasi

- [x] MVP prototip: daraxt kiritish va ko'rish (mock/local)
- [x] Telegram WebApp integratsiyasi
- [x] Hosting (GitHub Pages) + BotFather'da ro'yxatdan o'tkazish
- [x] Backend (Laravel): umumiy baza, Telegram auth — [shajara_api](https://github.com/JumayevIU/shajara_api)
- [x] Taklif havolasi va "Bu — men" belgilash
- [ ] Backendni HTTPS hostingga joylash va `API_DEFAULT` ni to'ldirish
- [ ] Shajara posterini PDF eksport (premium g'oya)
