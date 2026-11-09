# Pandas Ödevleri (01, 02 & 03)

SoftITO eğitimi kapsamında verilen pandas ödevleri: veriyi içe aktarma, ilk inceleme ve temel analiz/görselleştirme.

## Veri setleri
| Dosya | Açıklama |
|---|---|
| `bestsellers.csv` | Amazon çok satan kitaplar (550 satır): ad, yazar, puan, yorum sayısı, fiyat, yıl, tür |
| `mount_everest_deaths.csv` | Everest'te hayatını kaybedenler (1922–2021): tarih, yaş, ekspedisyon, uyruk, ölüm nedeni, konum |
| `movie_titles.tsv` | Film listesi; tab ile ayrılmış, başlık satırı yok |
| `degerlendirme_veri.xlsx` | 50 öğrencinin 13 günlük sınav notları (0-100) ve günlük değerlendirme puanları (0-10), A/B/C grupları |

## Pandas 01 — Veri içe aktarma ve ilk inceleme
- `bestsellers`: boyut, `head`/`tail`, eksik değerler, veri tipleri
- `mount_everest_deaths`: mevcut sütunu index olarak kullanma (`index_col`), null analizi
- `movie_titles.tsv`: `sep='\t'` ile okuma, `header=None` + `names` ile sütun adlarını verme

## Pandas 02 — Temel analiz ve görselleştirme (`bestsellers`)
- Series seçimi, unique değerler, ortalama ve en yüksek fiyatlar
- En sık geçen kitaplar ve yazar–puan kombinasyonları (`value_counts`)
- Grafikler: tür dağılımı (pie), en üretken 10 yazar (bar), puan dağılımı (histogram)

## Pandas 03 — Kodlama Değerlendirmesi: öğrenci başarı analizi (`degerlendirme_veri.xlsx`)
- Üç sayfanın `merge` ile birleştirilmesi ve veri kalitesi kontrolü
- Min-Max normalizasyonu ve başarı ölçüsü: `Not_norm * 0.7 + Puan_norm * 0.3`
- En başarılı N öğrenci ve en başarılı grup, gruplar için tarih aralığına göre başarı grafiği
- Günlük sınav ortalamasının değişimi; ortalama, medyan, mod, standart sapma ve görselleştirme
- Ek sorular: sınav notu ile değerlendirme puanı ilişkisi (korelasyon), dönem içinde en çok gelişen öğrenciler

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `101_Pandas_01.ipynb` | Pandas 01 çözümleri |
| `101_Pandas_02.ipynb` | Pandas 02 çözümleri |
| `101_Pandas_03.ipynb` | Pandas 03 – Kodlama değerlendirmesi |
| `101_README.md` | Bu dosya |

**Kullanılan kütüphaneler:** Python, Pandas, NumPy, Matplotlib, Seaborn
