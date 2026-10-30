# Pandas Ödevleri (01 & 02)

SoftITO eğitimi kapsamında verilen iki pandas ödevi: veriyi içe aktarma, ilk inceleme ve temel analiz/görselleştirme.

## Veri setleri
| Dosya | Açıklama |
|---|---|
| `bestsellers.csv` | Amazon çok satan kitaplar (550 satır): ad, yazar, puan, yorum sayısı, fiyat, yıl, tür |
| `mount_everest_deaths.csv` | Everest'te hayatını kaybedenler (1922–2021): tarih, yaş, ekspedisyon, uyruk, ölüm nedeni, konum |
| `movie_titles.tsv` | Film listesi; tab ile ayrılmış, başlık satırı yok |

## Pandas 01 — Veri içe aktarma ve ilk inceleme
- `bestsellers`: boyut, `head`/`tail`, eksik değerler, veri tipleri
- `mount_everest_deaths`: mevcut sütunu index olarak kullanma (`index_col`), null analizi
- `movie_titles.tsv`: `sep='\t'` ile okuma, `header=None` + `names` ile sütun adlarını verme

## Pandas 02 — Temel analiz ve görselleştirme (`bestsellers`)
- Series seçimi, unique değerler, ortalama ve en yüksek fiyatlar
- En sık geçen kitaplar ve yazar–puan kombinasyonları (`value_counts`)
- Grafikler: tür dağılımı (pie), en üretken 10 yazar (bar), puan dağılımı (histogram)

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `101_Pandas_01.ipynb` | Pandas 01 çözümleri |
| `101_Pandas_02.ipynb` | Pandas 02 çözümleri |
| `101_README.md` | Bu dosya |

**Kullanılan kütüphaneler:** Python, Pandas, Matplotlib
