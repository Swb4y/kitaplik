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

- *Canlı senkronu aç* denildiğinde uygulama rastgele isimli bir "oda" (ntfy.sh konusu) üretir — kayıt, hesap ya da sunucu kurulumu yok.
- Liste, odaya tek bir mesaj olarak yayınlanır (gerektiğinde gzip'lenip base64 ile). Karşı taraf `EventSource` (SSE) ile aynı odayı dinlediği için değişiklik **anında** düşer; ayrıca emniyet payı olarak arada bir yoklama yapılır (akış açıkken 60 sn, sekme arkadayken 90 sn, akış yoksa 5 sn).
- Çakışma çözümü kitap bazında **en son güncellenen kazanır** (`u` alanı). Silmeler mezar taşı (`d:1`) olarak taşındığı için karşı tarafta da silinir.
- Depo sırası `PROVIDER_ORDER` ile belirlenir: `ntfy` (öntanımlı, ön uçuş/CORS gerektirmez), sonra `jsonblob`, sonra `kvdb`. İlk çalışan seçilir; hepsi başarısız olursa hata nedenleri ekranda yazılır.
- **Bağlantıyı sına** düğmesi her deponun bu cihazdan çalışıp çalışmadığını tek tek dener ve sonucu listeler — hata ayıklamanın en kısa yolu.
- Her telefonda yerel kopya (LocalStorage) her zaman durur. Oda geçmişi ntfy.sh'te ~12 saat tutulur; uygulama her açılışta kendi listesini yeniden yayınladığı için geçmiş düşse de veri kaybolmaz, iki taraf birleşerek yakınsar.
- Odaya yalnızca eşleşme linkindeki rastgele oda adını bilen ulaşabilir. Veriler şifrelenmez; özel notları buraya yazmamak iyi olur.

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
