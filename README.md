# Kitaplık 📚

**Kitaplık**, iki kişinin (ör. bir çiftin) kitaplarını birlikte takip etmesi için yapılmış küçük bir web uygulamasıdır. Hangi kitabı bitirdiniz, hangisini okuyorsunuz, sırada ne var — hepsi tek listede, iki telefonda canlı olarak.

👉 **Yayındaki adres:** https://swb4y.github.io/kitaplik/

Kayıt yok, giriş yok, sunucu yok. Linki açan doğrudan kullanmaya başlar.

## Özellikler

- 🔄 **Canlı senkron** — iki telefon aynı listeyi paylaşır; biri kitap eklediğinde diğerinde birkaç saniye içinde görünür. Kurulum, hesap ya da şifre gerekmez: *Ayarlar → Canlı senkronu aç* → *Eşleşme linkini gönder*.
- 📖 **Kitap kaydı** — ad, yazar, durum, sayfa sayısı, kaçıncı sayfada olduğunuz, 5 üzerinden puan, başlama ve bitirme tarihi, not, okuyan kişi
- 🏷️ **Dört durum** — Sırada · Okuyorum · Bitirdim · Bıraktım (satırın solundaki kitap sırtı çizgisi durumu gösterir)
- 📊 **Özet** — bitirilen kitap sayısı, okunan toplam sayfa, ortalama puan
- 🔎 **Filtreler** — durum sekmeleri, kitap/yazar arama, okuyan kişiye göre süzme
- 🔗 **Link ile paylaşma** — senkron kapalıyken de tüm liste bir bağlantının içinde gönderilip karşı tarafta birleştirilebilir
- 📱 **Ana ekrana eklenebilir** — Safari'de *Paylaş → Ana Ekrana Ekle*; uygulama gibi açılır, çevrimdışı çalışır (PWA)
- 🌸 **Mor çiçekli tema** — açık ve koyu modda çalışan bahçe temalı arayüz, kitap bitince taç yaprağı kutlaması

## Canlı senkron nasıl çalışıyor?

- *Canlı senkronu aç* denildiğinde uygulama, hesap gerektirmeyen ücretsiz bir bulut depoda (önce `kvdb.io`, olmazsa `jsonblob.com`) rastgele kimlikli bir "oda" açar ve listeyi oraya yazar.
- Her telefon odayı 5 saniyede bir okur (sekme arkadayken 45 saniye), gelen kayıtları işler ve kendi değişikliklerini yazar.
- Çakışma çözümü kitap bazında **en son güncellenen kazanır** (`u` alanı). Silmeler mezar taşı (`d:1`) olarak yazıldığı için karşı tarafta da silinir.
- Her telefonda yerel bir kopya (LocalStorage) her zaman durur; internet ya da servis kesilse bile kayıtlar kaybolmaz, bağlantı gelince kendiliğinden eşitlenir.
- Odaya yalnızca eşleşme linkindeki rastgele oda kodunu bilen ulaşabilir. Veriler şifrelenmediği için özel notları buraya yazmamak iyi olur.

## Teknik

Tek dosyalık, bağımlılıksız bir uygulama. Derleme adımı yoktur.

```
docs/
├── index.html            # uygulamanın tamamı (HTML + CSS + JS)
├── manifest.webmanifest  # PWA künyesi
├── sw.js                 # çevrimdışı önbellek
└── icon*.png / icon.svg  # uygulama ikonları
```

## Geliştirme

Depoyu klonlayıp `docs/index.html` dosyasını doğrudan tarayıcıda açmak yeterlidir. Service worker'ın da çalışması için yerel bir sunucu kullanın:

```bash
npx http-server docs -p 8080
```

## Yayınlama

GitHub Pages, `main` dalının `docs/` klasöründen yayın yapar (**Settings → Pages → Deploy from a branch → main / docs**). `docs/` içindeki dosyaları değiştirip `main`'e push etmek yeterlidir; birkaç dakika içinde yayına girer.

Tüm dosya yolları görelidir; uygulama depo adı değişse de (adres `…github.io/yeni-ad/` olur) çalışmaya devam eder.
