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

## Ortak liste (canlı senkron) nasıl çalışıyor?

- *Yeni ortak liste başlat* kısa bir kod üretir (örn. `mavi-sumbul-2593`). Eşiniz aynı kodu yazınca ya da gönderilen eşleşme linkine dokununca aynı listeye bağlanır. Hesap, şifre, kurulum yok.
- Oda adı kodun **SHA-256 özetinden** türetilir, yani kod hiçbir zaman adres olarak görünmez. Kodu bilmeyen odayı bulamaz.
- Liste, odaya tek mesaj olarak yayınlanır (gerekirse gzip + base64). Karşı taraf `EventSource` (SSE) ile aynı odayı dinlediği için değişiklik **anında** düşer; emniyet payı olarak arada yoklama da yapılır (akış açıkken 60 sn, sekme arkadayken 90 sn, akış yoksa 5 sn).
- Çakışma çözümü kitap bazında **en son güncellenen kazanır** (`u` = epoch ms). Silmeler mezar taşı (`d:1`) olarak taşındığı için karşı tarafta da silinir. `u` alanı `ts()` ile okunur — `num()` sayfa sayısını 20000'e kırptığı için zaman damgasına uygulanamaz.
- Depo sırası: `ntfy` (öntanımlı; oda adı istemcide üretilir, `text/plain` POST olduğu için CORS ön uçuşu gerekmez), sonra `jsonblob`, sonra `kvdb`. ntfy dışındaki depolar kendi kimliklerini üretir, orada kod yerine eşleşme linki kullanılır.
- **Bağlantıyı sına** düğmesi her depoyu tek tek dener (yaz → oku) ve sonucu ✅/❌ olarak listeler.
- Her telefonda LocalStorage'da çevrimdışı bir kopya durur. ntfy.sh oda geçmişini ~12 saat tutar; uygulama her açılışta kendi listesini yeniden yayınladığı ve geçmişteki tüm anlık görüntüler birleştirildiği için geçmiş düşse de veri kaybolmaz.

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
