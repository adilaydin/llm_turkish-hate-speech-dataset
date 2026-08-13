# Türkçe Nefret Söylemi — Hedef Kategori Bazlı Yeniden Etiketlenmiş Veri Kümesi

⚠️ **İçerik uyarısı:** Bu veri kümesi nefret söylemi, saldırgan dil ve ayrımcı ifadeler içeren tweet metinleri barındırmaktadır. Yalnızca araştırma amaçlı kullanım için paylaşılmaktadır.

## Genel Bakış

Bu veri kümesi, Toraman ve ark. (2022) tarafından toplanan ve daha sonra yazarlarca "v2" sürümü olarak yayımlanan (%80 üzeri anotatör uyumlu, 60.310 Türkçe tweet) külliyatın, büyük dil modeli (Claude, Anthropic) ile uzman bilgisine dayalı bir Türkçe sözlüğü birleştiren bir zayıf-gözetim (weak supervision) hattıyla **içerik temelli hedef kategorilerine göre yeniden etiketlenmiş** hâlidir.

Orijinal veri kümesi, tweet'leri veri toplama sürecinde kullanılan anahtar-kelime alanına (`TopicID`: Din, Cinsiyet, Irk, Siyaset, Spor) göre etiketliyordu — bu, gerçek hedef kategorisinin güvenilir bir vekili değildir. Bu çalışma, aynı tweet'leri dört hedef kategoriye (ırkçılık, dini kökenli nefret, cinsiyetçilik/cinsel yönelim, diğer) göre yeniden etiketleyerek, hem eski vekil etiketi (`TopicID`) hem de yeni içerik-temelli etiketi aynı satırda bir arada sunar.

Yöntem, doğrulama ve karşılaştırmalı sonuçlar için bkz
## Dosya

| Dosya | Satır | Açıklama |
|---|---|---|
| `veriseti2_temiz_sonuc.csv` | 60.310 | Ana veri kümesi (800 satırlık altın standart alt kümesi dahil) |

## Sütunlar

| Sütun | Açıklama |
|---|---|
| `TweetID` | Twitter/X tweet kimliği |
| `TopicID` | Orijinal vekil etiket (0=Din, 1=Cinsiyet, 2=Irk, 3=Siyaset, 4=Spor) — Toraman ve ark. (2022)'den korunmuştur |
| `HateLabel` | Orijinal şiddet sınıfı (0=Normal, 1=Saldırgan, 2=Nefret) — Toraman ve ark. (2022)'den korunmuştur |
| `text` | Tweet metni |
| `irkcilik` | Irkçılık hedef kategorisi (0/1, one-hot) |
| `dini_kokenli` | Dini kökenli nefret hedef kategorisi (0/1, one-hot) |
| `cinsiyetcilik_cinsel_yonelim` | Cinsiyetçilik/cinsel yönelim hedef kategorisi (0/1, one-hot) |
| `diger` | Diğer hedef kategorisi (0/1, one-hot) |
| `process_status` | Satırın işlenme durumu: `ok` (LLM+sözlük hattından başarıyla geçti), `skipped_negative` (doğrudan nötr olarak enjekte edildi), `llm_error` (LLM hata/zaman aşımı, ham etikete geri düşürüldü), `golden` (800 satırlık insan-doğrulamalı altın standart alt kümesi) |

## Kategori Dağılımı

| process_status | Satır Sayısı | Oran |
|---|---|---|
| skipped_negative | 32.539 | %54,0 |
| ok | 24.846 | %41,2 |
| llm_error | 2.125 | %3,5 |
| golden | 800 | %1,3 |

## Etiketleme Yöntemi (özet)

1. Tweet gruplari, altın standart üzerindeki uyuşmazlık analiziyle geliştirilen bir sistem promptuyla Claude'a (Anthropic) gönderilmiştir.
2. Bağımsız bir sinyal olarak elle küratörlüğü yapılmış bir Türkçe sözlükten geçirilmiştir.
3. İki kaynağın çıktıları kural birleşimi (rule fusion) adımında tek bir etikette birleştirilmiştir.
4. Etiketleme, 800 örneklik insan-doğrulamalı altın standart kümeye karşı %78,25 doğruluk ve 0,712 Cohen's Kappa değeri elde etmiştir.

Ayrıntılı yöntem, sınırlılıklar ve aşağı-akış model karşılaştırmaları için bildiriye bakınız.

## Lisans ve Kullanım Notu

- Bu veri kümesi yalnızca **araştırma amaçlı** kullanım için paylaşılmaktadır.
- **Twitter/X kullanım koşulları** ham tweet metninin doğrudan yeniden dağıtımını kısıtlayabilir. Yayımlamadan önce güncel [X Geliştirici Sözleşmesi'ni](https://developer.x.com/en/developer-terms/agreement-and-policy) kontrol etmeniz ve gerekirse `text` sütununu kaldırıp yalnızca `TweetID` + etiketleri paylaşarak kullanıcıların kendi "rehydration" (yeniden metin çekme) betiğiyle içeriği almasını sağlamanız önerilir — Toraman ve ark.'ın kendi v1/v2 sürümleri de bu yaklaşımı benimsemiştir.
- Önerilen lisans: `CC BY-NC-SA 4.0` (orijinal Toraman v1/v2 veri kümesiyle aynı lisans ailesi) — nihai kararı siz verin.

## Atıf

Bu veri kümesini kullanırsanız lütfen hem orijinal külliyatı hem de bu çalışmayı kaynak gösterin:

```
Toraman, C., Şahinuç, F., & Yılmaz, E. H. (2022). Large-scale hate speech detection
with cross-domain transfer. Proceedings of the Thirteenth Language Resources and
Evaluation Conference (LREC 2022), 2215-2225.

[https://github.com/metunlp/hate-speech/tree/master]
```

## İletişim

Sorularınız için: [adilaydin1661@gmail.com]
