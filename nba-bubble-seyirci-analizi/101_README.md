# Seyirci Gerçekten Maç Kazandırır mı? NBA Bubble ve Ev Sahibi Avantajı

SoftITO Veri Analitiği eğitimi bitirme projesi, Bölüm A. *(Çalışma devam ediyor: Power BI dashboard eklenecek.)*

## Soru

NBA'de ev sahibi avantajının ne kadarı seyirciden geliyor?

2020 NBA Bubble'ı bu soru için bir doğal deney sunuyor: 30 Temmuz – 11 Ekim 2020 arasında maçlar seyircisiz ve tarafsız sahada oynandı.

## Veri

[NBA games data (Kaggle, nathanlauga)](https://www.kaggle.com/datasets/nathanlauga/nba-games) veri setindeki `games.csv` dosyası. Ekim 2003 – Aralık 2022 arası 26.651 maç içeriyor.

`games.csv` dosyasını indirip bu klasöre koyduktan sonra notebook baştan sona çalıştırılabilir.

## Yöntem

1. **Veri temizliği**
   - Tekrar eden kayıtlar silindi; aynı ID'ye sahip 2 maçta istatistik düzeltmesi vardı.
   - Hazırlık maçları çıkarıldı.
   - Veri tipleri küçültüldü: bellek 5.7 MB'tan 1.95 MB'a indi.
2. **EDA**
   - Sezonlara göre ev sahibi kazanma oranı ve sayı farkı, %95 güven aralıklarıyla.
3. **Hipotez testi**
   - Soru: 2019-20 sezonundaki düşüş COVID'le mi ilgili? 2019-20'nin her ayı, önceki sezonların aynı ayıyla karşılaştırıldı.
4. **Model**
   - Sadece maç öncesinde bilinen özellikler kullanıldı: son 10 maçtaki form ve dinlenme günü. Böylece veri sızıntısı (data leakage) önlendi.
   - **Tahmin:** Logistic Regression. Train 2003–2016, test 2017–2022 (zamana göre bölme).
   - **Açıklama:** statsmodels Logit ile seyircisiz dönemin etkisi ölçüldü. Takım formu, dinlenme, maç türü ve uzun vadeli trend kontrol edildi.

## Bulgular

- **Ev sahibi avantajı 20 yılda eriyor.**
  - 2003–2012 arasında ev sahibi maçların yaklaşık %60–61'ini kazanıyordu, 2021-22'de bu oran %54.8.
  - Düşüş COVID'den önce başlamış.
  - Seyirci 2021-22'de geri döndü ama avantaj geri dönmedi.
- **Bubble'da ev sahibi kazanma oranı %52.3.** Ancak Bubble'da sadece 172 maç var. Ev sahibinin ortalama sayı farkı +1.35 ± 2.0; bu aralık sıfırı içeriyor, yani Bubble verisi tek başına kesin bir sonuç vermiyor.
- **Model, baseline'ı yaklaşık 5 puan geçiyor.**

  | | Accuracy | AUC |
  |---|---|---|
  | Baseline (her zaman ev sahibi) | 0.568 | 0.500 |
  | Logistic Regression | 0.619 | 0.659 |

- **Seyircinin etkisi küçük ama anlamlı.**
  - Diğer faktörler kontrol edildikten sonra seyircisizlik, ev sahibinin kazanma ihtimalini düşürüyor.
  - Eşit güçte iki takım için (2020 sezonu): seyirciyle %57.7, seyircisiz %54.4. Fark yaklaşık 3.3 puan.
  - Katsayı: −0.134, %95 güven aralığı [−0.260, −0.009], p = 0.036.
  - Etkinin büyüklüğü belirsiz, çünkü güven aralığının üst ucu sıfıra çok yakın.
- **Seyirci, avantajın tamamını açıklamıyor.** Uzun vadeli trend, ev sahibi avantajını seyircisizlikten daha fazla düşürmüş.

## Sınırlamalar

- Bu bir gözlemsel çalışma. Bulgular nedensellik değil, kontrol edilmiş ilişki gösteriyor.
- `no_crowd` bayrağı yaklaşık bir değer: 2020-21 sezonunun sonlarında bazı salonlar sınırlı sayıda seyirci aldı.

## Dosyalar

- `101_bubble_seyirci.ipynb`: analiz notebook'u
- `home_win_rate_by_season.png`: sezonlara göre ev sahibi kazanma oranı grafiği

## Kullanılan araçlar

pandas, NumPy, matplotlib, scikit-learn, statsmodels
