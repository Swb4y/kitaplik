# Kitaplık 📚

**Kitaplık**, iki kişinin (ör. bir çiftin) kitaplarını birlikte takip etmesi için yapılmış küçük bir web uygulamasıdır. Hangi kitabı bitirdiniz, hangisini okuyorsunuz, sırada ne var — hepsi tek listede.

👉 **Yayındaki adres:** https://swb4y.github.io/kitaplik/

Kayıt yok, giriş yok, sunucu yok. Linki açan doğrudan kullanmaya başlar.

## Özellikler

- 📖 **Kitap kaydı** — ad, yazar, durum, sayfa sayısı, kaçıncı sayfada olduğunuz, 5 üzerinden puan, başlama ve bitirme tarihi, not, okuyan kişi
- 🏷️ **Dört durum** — Sırada · Okuyorum · Bitirdim · Bıraktım (her satırın solundaki kitap sırtı çizgisi durumu gösterir)
- 📊 **Özet** — bitirilen kitap sayısı, okunan toplam sayfa, ortalama puan
- 🔎 **Filtreler** — durum sekmeleri, kitap/yazar arama, okuyan kişiye göre süzme
- 🔗 **Listeyi gönder** — tüm kayıtlarınızı bağlantının içine gömer; karşı taraf linki açınca "Listeye ekle" diyerek kendi listesiyle birleştirir. Aynı kitap iki tarafta varsa en son güncellenen kazanır.
- 📱 **Ana ekrana eklenebilir** — Safari'de *Paylaş → Ana Ekrana Ekle*; uygulama gibi açılır ve çevrimdışı çalışır (PWA)
- 🌗 **Açık ve koyu tema** — telefonun ayarına uyar

## Veriler nerede duruyor?

Yalnızca uygulamayı açtığınız cihazın tarayıcısında (LocalStorage). Hiçbir veri sunucuya gitmez, hesap gerekmez. İki telefonu eşlemenin yolu **Listeyi gönder** bağlantısıdır.

Not: Birleştirme ekleme yönünde çalışır — bir kitabı sildiğinizde bu silme karşı tarafa geçmez.

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
