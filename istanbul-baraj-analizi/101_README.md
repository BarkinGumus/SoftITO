# İstanbul Barajları Doluluk Analizi

## Veri seti
- **Kaynak:** İBB Açık Veri Portalı (data.ibb.gov.tr) – İstanbul Barajları Günlük Doluluk Oranları
- **Dosya:** `istanbul-dams-daily-occupancy-rates.xlsx`
- **Kapsam:** 10 baraj, günlük doluluk oranı (0–1), 23 Ekim 2000 – 19 Şubat 2024, 8.520 satır

## Önerme
> İstanbul barajları her yıl en düşük seviyesine sonbaharda (Eylül–Aralık) iner.

## Yöntem
1. **Veri temizleme:** 1 Nisan – 8 Ağustos 2023 arasındaki 130 satırda tarih metin olarak (`1.4.2023`), oranlar ise yüzde olarak girilmişti. Tarihler `gün.ay.yıl` formatıyla çevrildi, bu satırlardaki oranlar 100'e bölündü. 1'i hafifçe aşan değerler (taşma) olduğu gibi bırakıldı.
2. **Genel doluluk:** 10 barajın ağırlıksız ortalaması.
3. **EDA:** yıllık, aylık ve baraj bazında özetler.
4. **Önerme testi:** Her tam yılın en düşük doluluk günü bulundu ve ayına bakıldı. Veri 2000 ve 2024'te eksik olduğu için bu yıllar dışarıda bırakıldı; aksi halde dip noktası sadece mevcut aylardan seçilir ve sonuç yanıltıcı olur.

## Sonuç
- Doluluk Nisan'da zirve (~%80), Ekim'de dip (~%47) yapıyor.
- 23 yılın **18'inde (%78.3)** dip Eylül–Aralık'ta.
- Ocak başı dipler (sonbahar düşüşünün devamı) dahil edildiğinde **22/23 (%95.7)**. Tek istisna 2002.
- **Önerme büyük ölçüde destekleniyor.**

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `istanbul-dams-daily-occupancy-rates.xlsx` | Ham veri seti |
| `101_istanbul_baraj_analizi.ipynb` | Temizleme, EDA ve önerme testi |
| `101_README.md` | Bu dosya |

**Kullanılan kütüphaneler:** Python, Pandas, NumPy
