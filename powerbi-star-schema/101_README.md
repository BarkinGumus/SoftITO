# Power BI – Star Schema vs Snowflake Modelleme

İşletme anketi (establishment survey) verisi üzerinde boyutsal modelleme çalışması: aynı rapor hem **star schema** hem **snowflake** yapısıyla kurulup karşılaştırıldı.

## Veri modeli
- **Fact tablosu:** `Establishment_Survey` (çalışan sayısı)
- **Star schema boyutları:** `Industry` (sektör hiyerarşisi tek tabloda), `Time`, `EstablishmentAge`
- **Snowflake boyutları:** sektör hiyerarşisi ayrı tablolara bölündü: `Sector` → `Subsector` → `Industry_group` → `NAICS_code`

## Rapor
- **Sayfa 1:** Alt sektörlere göre toplam çalışan sayısı (bar chart); on yıl, işletme yaşı ve sektör grubu filtreleri (slicer)
- **Sayfa 2:** Aynı metriğin star (`Industry`) ve snowflake (`Subsector`) modeliyle çizilmiş iki line chart'ı yan yana; iki yaklaşımın aynı sonucu verdiğini göstermek için

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `101_star_schema.pbix` | Power BI Desktop dosyası |
| `101_README.md` | Bu dosya |

**Kullanılan araçlar:** Power BI Desktop, Power Query, boyutsal modelleme
