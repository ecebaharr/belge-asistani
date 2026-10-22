# Pro Git Asistanı

Türkçe soru soran, **İngilizce** *Pro Git* kitabından cevap bulan bir soru-cevap asistanı (RAG).
Soru Türkçe sorulur; asistan soruyu İngilizceye çevirip kitapta arar, **yalnızca bulduğu parçalara dayanarak** Türkçe cevap verir ve **kaynak sayfayı** gösterir. Kitapta cevap yoksa uydurmak yerine "bulamadım" der.

## Neler var?
- **Türkçe → İngilizce çapraz dilli arama:** soru çevrilir, hem BM25 hem embedding ile aranır, cross-encoder ile yeniden sıralanır.
- **Yapıya duyarlı parçalama:** yazı tipinden başlık ve kod blokları algılanır, kodlar bölünmez.
- **Kaynaklı cevap:** her bilgi `[kimlik]` ile işaretlenir, uydurma kaynaklar uyarı alır; kaynak kartında sayfa önizlemesi ve sarı vurgu.
- **İsteğe bağlı cevap doğrulama**, takip soruları, bölüm özeti, terim sözlüğü, quiz, sohbeti indirme.
- **Ölçüm bölümü:** Hit@K, MRR, çeviri deneyi, kapsam dışı test, Haiku ↔ Sonnet karşılaştırması.

## Kurulum
1. Python 3.10+ ve bir [Anthropic API anahtarı](https://console.anthropic.com) gerekir (anahtar yoksa "yalnızca arama" modu çalışır).
2. Kütüphaneler:
   ```
   pip install chromadb sentence-transformers rank_bm25 pypdf anthropic "gradio>=5" snowballstemmer pypdfium2
   ```
3. Kitabı [git-scm.com/book](https://git-scm.com/book) adresinden PDF olarak indirip `Day5/veri/progit.pdf` yoluna koyun.
4. API anahtarını **koda yazmayın**; ortam değişkeni olarak verin (PowerShell):
   ```
   $env:ANTHROPIC_API_KEY = "anahtarınız"
   ```
   Verilmezse not defteri çalışırken gizli giriş ister.

## Çalıştırma
`progit_asistani.ipynb` dosyasını VS Code'da açın, hücreleri yukarıdan aşağıya çalıştırın. Son hücre Gradio arayüzünü `http://127.0.0.1:7860` adresinde açar.
İlk çalıştırma modelleri indirir ve indeksi kurar (birkaç dakika); sonrası önbellekten hızlı gelir.

## Sınırlılıklar
- Testler **kuralları** denetler (kaynak var mı, uydurma kaynak yok mu); cevabın içerik doğruluğunu otomatik ölçmez.
- Ölçüm seti küçüktür (16 soru), sonuçlar yön göstergesidir.
- Taranmış (yalnızca resim) PDF'lerde metin okunamaz; OCR gerekir.

## Lisans / Kaynak
*Pro Git* — Scott Chacon, Ben Straub — Creative Commons BY-NC-SA 3.0. Kitap bu depoya dahil değildir.
