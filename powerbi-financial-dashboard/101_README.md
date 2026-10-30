# Power BI – Financial Dashboard

İlk Power BI çalışmam: tek tablolu bir satış verisinden KPI kartları, trend ve kırılım grafikleri olan interaktif bir dashboard.

![Dashboard](101_dashboard.png)

## Veri seti
- **Kaynak:** Microsoft Power BI örnek verisi – *Financial Sample* (`Financial Sample.xlsx`, tablo: `financials`)
- **Kapsam:** Ülke, segment, ürün ve indirim bandı bazında satış, maliyet ve kâr; Eylül 2013 – Aralık 2014 (16 ay)

## Yapılanlar
1. **Power Query:** Veri Excel'den alındı, sütun tipleri (tarih, ondalık sayı) kontrol edildi.
2. **DAX measure'ları:**
   ```dax
   Total Sales   = SUM(financials[Sales])
   Total Profit  = SUM(financials[Profit])
   Profit Margin = DIVIDE([Total Profit], [Total Sales])
   ```
   Margin, satır bazında oranların ortalaması yerine toplamlar üzerinden hesaplandı; böylece büyük satışlar doğru ağırlıkla yansıyor. `DIVIDE` sıfıra bölmede hata yerine boş değer döndürüyor.
3. **Rapor:**
   - KPI kartları: Total Sales, Total Profit, Profit Margin
   - Aylık satış trendi (line chart)
   - Ülkelere göre kâr (bar chart)
   - Segment filtresi (dropdown slicer)
   - Aylık satış ve geçen yılla karşılaştırma tablosu (Year Month, Total Sales, Sales LY, Sales YoY %)
4. **Calendar (tarih) tablosu:** Otomatik tarih hiyerarşisi yerine DAX ile ayrı bir tarih tablosu oluşturuldu ve *Mark as date table* ile işaretlendi.
   ```dax
   Calendar =
   ADDCOLUMNS (
       CALENDAR ( DATE ( 2013, 1, 1 ), DATE ( 2014, 12, 31 ) ),
       "Year", YEAR ( [Date] ),
       "Month Number", MONTH ( [Date] ),
       "Month", FORMAT ( [Date], "MMM" ),
       "Year Month", FORMAT ( [Date], "YYYY-MM" )
   )
   ```
   Yıllar tam alındı (1 Ocak – 31 Aralık), çünkü time intelligence fonksiyonları kesintisiz, tam yıllık bir takvim ister. `Month` sütunu `Month Number`'a göre sıralandı.
5. **İlişki (relationship):** `Calendar[Date]` → `financials[Date]`, one-to-many (1:\*), tek yönlü filtre. Calendar'da her tarih bir kez geçer; financials'ta aynı tarihte birden fazla satış olabilir.
6. **Time intelligence:**
   ```dax
   Sales LY    = CALCULATE ( [Total Sales], SAMEPERIODLASTYEAR ( 'Calendar'[Date] ) )
   Sales YoY % = DIVIDE ( [Total Sales] - [Sales LY], [Sales LY] )
   ```
   `CALCULATE`, tarih filtresini bir yıl geriye kaydırarak geçen yılın aynı dönemini hesaplıyor.

## Genel sonuçlar (filtresiz)
| KPI | Değer |
|---|---|
| Total Sales | 118.73M |
| Total Profit | 16.89M |
| Profit Margin | %14.23 |

**Not:** 2013 yılında yalnızca 4 ay (Eylül–Aralık) var. Bu yüzden 2013 ile 2014'ü yıl bazında karşılaştırmak yanıltıcı olur. Eksende sadece ay adı kullanıldığında da iki yılın aynı ayları üst üste toplanıyor; trend bu nedenle yıl + ay seviyesinde gösterildi.

## Geçen yılla karşılaştırma (YoY)
| Ay | Total Sales | Sales LY | YoY % |
|---|---|---|---|
| 2014-09 | 6,398,697 | 4,484,000 | %42.70 |
| 2014-10 | 12,375,820 | 9,295,611 | %33.14 |
| 2014-11 | 5,384,214 | 7,267,203 | %-25.91 |
| 2014-12 | 11,998,788 | 5,368,441 | %123.51 |

- `Sales LY` yalnızca Eylül–Aralık 2014'te dolu, çünkü bir yıl öncesinde yalnızca Eylül–Aralık 2013 verisi var.
- Tablonun toplam satırı kapatıldı: toplamda `Total Sales` 16 ayı, `Sales LY` ise yalnızca 4 ayı kapsıyor, bu yüzden toplam YoY (%349) anlamsız bir sayı veriyordu.

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `101_financial_dashboard.pbix` | Power BI Desktop dosyası |
| `101_dashboard.png` | Dashboard ekran görüntüsü |
| `101_README.md` | Bu dosya |

**Kullanılan araçlar:** Power BI Desktop, Power Query, DAX
