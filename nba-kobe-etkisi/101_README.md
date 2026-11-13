# Kobe Etkisi: NBA Yıldızları Bebek İsimlerini Değiştiriyor mu?

SoftITO Veri Analitiği eğitimi, ikinci proje.

## Soru

Bir NBA oyuncusu draft edildiğinde, şampiyon olduğunda, MVP seçildiğinde ya da hayatını kaybettiğinde, ABD'de o oyuncunun ismini alan bebek sayısı artıyor mu?

## Veri

- **Bebek isimleri:** ABD Sosyal Güvenlik Kurumu (SSA), *Baby Names from Social Security Card Applications – National Data*, 1880–2024. Ham `yob*.txt` dosyaları [dxdc/babynames](https://github.com/dxdc/babynames) aynasından alındı ve `data/names_all.csv.gz` olarak birleştirildi (2.149.477 satır). Gizlilik nedeniyle 5'ten az kullanılan isimler veride yok.
- **NBA olayları:** 25 oyuncu için 47 olay (draft, şampiyonluk, MVP, vefat, emeklilik, isim değişikliği). Aralarında Michael Jordan, Magic Johnson, Larry Bird, Kareem Abdul-Jabbar ve Isiah Thomas gibi megastarlar da var. Elle derlendi, kaynak Basketball-Reference.

## Yöntem

1. İsim sayılarını o yılın toplam erkek doğumlarına bölerek **milyonda pay** hesapladım.
2. İsim eğrilerini olay yıllarıyla birlikte çizdim (EDA).
3. **Event study (olay çalışması):** Her olay için olaydan önceki 2 yılın ortalama payını (E-2, E-1), olay yılı ve sonraki yılın ortalama payıyla (E, E+1) karşılaştırdım.
4. **Placebo testi:** Aynı hesabı 1970–2023 arasında NBA'le ilgisi olmayan isimler için de yaptım (442.839 isim-yıl gözlemi). Her olayın artışını, önceki dönemde benzer büyüklükte olan (bebek sayısı yarısı ile iki katı arası) isimlerin dağılımında bir yüzdeliğe yerleştirdim.
5. Karıştırıcı faktörleri (confounder) ayrıca inceledim.

## Bulgular

- **Kobe Etkisi gerçek.**
  - Kobe ismi, Kobe Bryant'ın draft edildiği dönemde yılda 9 bebekten (1995) 1.552'ye (2001) çıktı.
  - Ocak 2020'deki vefatından sonra tek yılda 506'dan 1.515'e yükseldi, yani 3 katına çıktı. Bu artış placebo dağılımında 99.7. yüzdelikte.
- **En güçlü etkiyi "ilk görünme" yaratıyor.** 16 draft olayının medyan yüzdeliği 99.5.
  - Kobe, Shaquille, LeBron, Kyrie, Iverson, Earvin (Magic Johnson), Anfernee (Penny Hardaway) ve Amare'nin draft yıllarındaki artışlar, aynı büyüklükteki isimlerin %99'undan daha fazla.
  - Kareem: Lew Alcindor'un 1971'de adını değiştirmesinden sonra isim 12 bebekten (1970) 378'e (1972) çıktı.
- **Şampiyonluklar her zaman isim kazandırmıyor.** 21 şampiyonluğun sadece %33'ü 95. yüzdeliği geçiyor.
  - "Lebron" ismi, LeBron James'in 2012 ve 2016 şampiyonluklarından sonra azaldı.
- **Megastar olmak yaygın bir ismi değiştirmeye yetmiyor.** "Michael" ve "Larry", Michael Jordan ve Larry Bird'ün en parlak yıllarında bile düşüşteydi.
- **Bazı isimler oyuncuyla birlikte doğdu.** "Giannis" (ilk kez 2014) ve "Kawhi" (ilk kez 2013), oyuncular ünlü olana kadar SSA verisinde hiç yok.

| Olay türü | Olay sayısı | Medyan artış (kat) | Medyan yüzdelik | 95. yüzdelik üstü |
|---|---|---|---|---|
| Draft | 16 | 3.1 | 99.5 | %62.5 |
| MVP | 5 | 1.4 | 93.5 | %40 |
| Şampiyonluk | 21 | 1.2 | 87.5 | %33 |
| Vefat (Kobe) | 1 | 2.8 | 99.7 | |
| Emeklilik (Magic) | 1 | 2.3 | 98.9 | |
| İsim değişikliği (Kareem) | 1 | 39.9 | 100.0 | |

## Sınırlamalar

- **Bu gözlemsel bir analiz.** Zamanlamanın tutması, nedenselliği kanıtlamıyor. Örneğin:
  - **Zion:** İsmin asıl sıçraması, Zion Williamson doğmadan önce 1999'da.
  - **Hakeem:** İsmin sıçrama yılları, Olajuwon'un şampiyonluk yıllarına denk gelmiyor.
- **Placebo testi isim büyüklüğünü kontrol ediyor, önceden var olan trendi kontrol etmiyor.** Luka, Tatum, Kyrie ve Jordan isimleri olaydan önce de yükseliyordu.
- Dikembe ve Dwyane isimleri draft öncesinde veride hiç olmadığı için bu iki olayın yüzdeliği hesaplanamadı.
- **Veri yıllık ve sadece ABD'yi kapsıyor.** Olay türlerinin çoğunda olay sayısı az, bu yüzden özetler kesin sonuç değil, eğilim olarak okunmalı.

## Dosyalar

- `101_kobe_etkisi.ipynb`: analiz notebook'u (çıktılarıyla)
- `data/names_all.csv.gz`: birleştirilmiş SSA isim verisi
- `images/`: notebook'un ürettiği grafikler

## Makale

Bu proje hakkında yazdığım Medium yazısı: [Kobe Etkisi: NBA yıldızları bebek isimlerini değiştiriyor mu?](https://medium.com/@barkingumus56/kobe-etkisi-nba-y%C4%B1ld%C4%B1zlar%C4%B1-bebek-isimlerini-de%C4%9Fi%C5%9Ftiriyor-mu-de5f608bf349)

## Kullanılan araçlar

pandas, NumPy, matplotlib
