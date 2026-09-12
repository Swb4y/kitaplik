# English Quest — Sıfırdan İngilizce 🦉

English Quest, **hiç İngilizce bilmeyenler** için tasarlanmış, tamamı Türkçe arayüzlü, oyunlaştırılmış bir İngilizce öğrenme uygulamasıdır. Vite, React, TypeScript ve Tailwind CSS ile geliştirilmiştir.

Kayıt yok, ceza yok, stres yok: kendi hızında ilerlersin, ilerlemen cihazında saklanır ve uygulama çevrimdışı da çalışır (PWA).

## Özellikler

- 🇹🇷 **Tamamı Türkçe arayüz** — hiç İngilizce bilmeden rahatça kullanılır
- 🐣 **Sıfırdan başlayan müfredat** — 12 ünite, 96 temel kelime, 48 kalıp cümle
- 🔊 **Sesli telaffuz** — her kelime ve örnek cümle tarayıcının ses motoruyla dinlenebilir (Web Speech API)
- 📖 **Kelime kartları** — emoji, Türkçe anlam, Türkçe harflerle okunuş ve örnek cümle
- 🎯 **5 farklı alıştırma türü**:
  - Çoktan seçmeli (İngilizce → Türkçe)
  - Çoktan seçmeli (Türkçe → İngilizce)
  - Dinleme (duyduğun kelimeyi bul)
  - Eşleştirme (İngilizce–Türkçe çiftleri)
  - Cümle kurma (karışık kelimelerden cümle diz)
- 🎮 **Oyunlaştırma** — XP, seviye, günlük seri, 6 rozet, konfetili kutlamalar
- 🔁 **Tekrar modu** — öğrendiğin kelimelerden karışık hızlı tekrar turları
- 📔 **Kelime defteri** — öğrendiğin tüm kelimeler telaffuzlarıyla tek listede
- 🗺️ **Ünite haritası** — her ünite bitince yenisi açılır
- 📱 **Mobil öncelikli tasarım** — gradyanlar, animasyonlar, PWA desteği

## Üniteler

1. 👋 Selamlaşma
2. 🔢 Sayılar
3. 🎨 Renkler
4. 👨‍👩‍👧 Aile
5. 🍎 Yiyecek ve İçecek
6. 🐶 Hayvanlar
7. 📅 Günler
8. 🧍 Vücudumuz
9. 🏠 Evimiz
10. 👕 Kıyafetler
11. ☀️ Hava Durumu
12. 🏙️ Şehirde

## Teknolojiler

- Vite + React + TypeScript
- Tailwind CSS
- Web Speech API (telaffuz)
- LocalStorage (ilerleme kaydı)
- PWA (manifest + service worker)

## Geliştirme

Bağımlılıkları kur:

```bash
npm install
```

Geliştirme sunucusunu başlat:

```bash
npm run dev
```

Üretim derlemesi:

```bash
npm run build
```

Derlemeyi önizle:

```bash
npm run preview
```

## Yayınlama

### GitHub Pages (docs/ klasörü)

```bash
npm run build:pages
```

Bu komut uygulamayı `docs/` klasörüne derler. Repo ayarlarından **Settings → Pages → Deploy from a branch → /docs** seçiliyse uygulama otomatik yayınlanır.

### Vercel / Netlify

- Build komutu: `npm run build`
- Çıktı klasörü: `dist`

## Notlar

- Arka uç (backend) gerektirmez, tamamen tarayıcıda çalışır.
- Ders içerikleri `src/data/units.ts` dosyasındadır; yeni ünite eklemek için bu dosyaya ekleme yapmak yeterlidir.
- İlerleme yalnızca kullanılan cihazda, LocalStorage'da saklanır.
- Telaffuz için tarayıcının Web Speech API desteği kullanılır (tüm modern tarayıcılarda mevcuttur).

---

## 📚 Kitaplık — ortak okuma günlüğü

Bu repoda, English Quest'ten bağımsız çalışan ikinci bir mini uygulama var: **Kitaplık**. İki kişinin (ör. bir çiftin) hangi kitabı bitirdiğini, hangisini okuduğunu ve sırada ne olduğunu takip etmesi için tasarlandı.

- **Adres:** `docs/kitaplik/` → yayında `https://swb4y.github.io/english-quest/kitaplik/`
- **Kayıt/giriş yok:** linki açan herkes doğrudan kullanır
- **Veri:** yalnızca kullanılan cihazın LocalStorage'ında saklanır (sunucu yok)
- **Eşleşme:** “Listeyi gönder” butonu, tüm kayıtları bağlantının içine gömerek paylaşır; karşı taraf linki açınca “Listeye ekle” diyerek kendi listesiyle birleştirir (aynı kayıt iki tarafta varsa en son güncellenen kazanır)
- **PWA:** manifest + service worker; Safari'de *Paylaş → Ana Ekrana Ekle* ile uygulama gibi açılır ve çevrimdışı çalışır
- **Tek dosya:** `docs/kitaplik/index.html` (derleme adımı yok, bağımlılık yok)

Kitap kaydında tutulanlar: ad, yazar, durum (Sırada / Okuyorum / Bitirdim / Bıraktım), sayfa sayısı ve kaçıncı sayfada olunduğu, 5 üzerinden puan, başlama ve bitirme tarihi, not ve okuyan kişi.

> Dikkat: `npm run build:pages` komutu `docs/` klasörünü **tamamen temizleyerek** yeniden derler (`--emptyOutDir`). English Quest'i yeniden derlemeden önce `docs/kitaplik/` klasörünü yedekleyin.
