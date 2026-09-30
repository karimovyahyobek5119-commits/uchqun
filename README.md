# Uchqun — Android loyihasi

O'yin `app/src/main/assets/index.html` faylida. Android ilova uni WebView orqali ochadi, progress telefonda saqlanadi.
Paket nomi: `uz.yahyobek.uchqun` (Play Market'ga chiqqandan keyin o'zgartirib bo'lmaydi).

## 1. APK olish (telefonda sinab ko'rish uchun)

Kompyuterga Android Studio o'rnatish shart emas, GitHub o'zi yig'ib beradi.

1. GitHub'da yangi repository oching, masalan `uchqun`.
2. Shu papkadagi hamma fayllarni unga yuklang (`.github` papkasi ham bo'lishi shart).
3. Repository'da **Actions** bo'limini oching va "Build Uchqun" ishini kuting (3–6 daqiqa).
4. Tugagach, pastdagi **Artifacts** bo'limidan `uchqun-debug-apk` ni yuklab oling.
5. Zip ichidagi `app-debug.apk` ni telefonga o'tkazib o'rnating ("Noma'lum manbalar"ga ruxsat berish kerak bo'ladi).

Android Studio bo'lsa: papkani oching va ▶ Run bosing.

## 2. Play Market uchun AAB

Play Market APK emas, **AAB** (Android App Bundle) faylini qabul qiladi va u sizning kalitingiz bilan imzolangan bo'lishi kerak.

1. Kalit yarating (bir marta; faylni va parolni **hech qachon yo'qotmang**):
   ```
   keytool -genkeypair -v -keystore upload.jks -keyalg RSA -keysize 2048 -validity 10000 -alias uchqun
   ```
2. Kalitni base64 ga aylantiring:
   - Linux/Mac: `base64 -w0 upload.jks > upload.txt`
   - Windows PowerShell: `[Convert]::ToBase64String([IO.File]::ReadAllBytes("upload.jks")) > upload.txt`
3. GitHub → Settings → Secrets and variables → Actions → **New repository secret**:
   - `UPLOAD_KEYSTORE_BASE64` — upload.txt ichidagi matn
   - `UPLOAD_KEYSTORE_PASSWORD` — kalit paroli
   - `UPLOAD_KEY_ALIAS` — `uchqun`
   - `UPLOAD_KEY_PASSWORD` — kalit paroli
4. Actions'ni qayta ishga tushiring. Endi `uchqun-release-aab` ham chiqadi.
5. Har yangi versiyada `app/build.gradle` ichida `versionCode` ni 1 taga oshiring.

## 3. Play Console'da nima kerak

- Google Play Developer akkaunti (bir martalik to'lov).
- Yangi shaxsiy akkauntlar ochiq chiqarishdan oldin **yopiq test** o'tkazishi kerak: kamida 12 ta tester, 14 kun ketma-ket.
- Maxfiylik siyosati (Privacy Policy) sahifasi havolasi.
- Kontent reytingi so'rovnomasi va "Data safety" bo'limi. O'yin hech qanday ma'lumot yig'maydi, reklama yo'q.
- Maqsadli auditoriya 13 yoshdan kichiklarni ham o'z ichiga olsa, **Families** siyosati talablari amal qiladi.
- Ikon: `play-store/icon-512.png`. Yana 1024×500 banner va kamida 2 ta skrinshot kerak.

## Chiqarishdan oldin tuzatish kerak

**Do'stlar bo'limi:** hozir taklif kodi faqat shu telefonda tekshiriladi, taklif qilgan odamga sovg'a bormaydi.
Ilovada esa "siz 200 tanga + Bomba olasiz" deb yozilgan. Server (masalan, Firebase) qo'shilguncha
bu va'dani matndan olib tashlang yoki bo'limni yashiring, aks holda foydalanuvchilarni chalg'itadi.

**Shriftlar** Google Fonts'dan internet orqali yuklanadi. Internet bo'lmasa, o'yin telefonning standart shriftida ochiladi.
