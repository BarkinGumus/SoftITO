# Kobe Etkisi: NBA Yıldızları Bebek İsimlerini Değiştiriyor mu?

SoftITO Veri Analitiği eğitimi, ikinci proje.

## Soru

Bir NBA oyuncusu draft edildiğinde, şampiyon olduğunda, MVP seçildiğinde ya da hayatını kaybettiğinde, ABD'de o oyuncunun ismini alan bebek sayısı artıyor mu?

## Veri

- **Bebek isimleri:** ABD Sosyal Güvenlik Kurumu (SSA), *Baby Names from Social Security Card Applications – National Data*, 1880–2024. Ham `yob*.txt` dosyaları [dxdc/babynames](https://github.com/dxdc/babynames) aynasından alındı ve `data/names_all.csv.gz` olarak birleştirildi (2.149.477 satır). Gizlilik nedeniyle 5'ten az kullanılan isimler veride yok.
- **NBA olayları:** 17 oyuncu için 29 olay (draft, şampiyonluk, MVP, vefat). Elle derlendi, kaynak Basketball-Reference.

## Yöntem

1. İsim sayılarını o yılın toplam erkek doğumlarına bölerek **milyonda pay** hesapladım.
2. İsim eğrilerini olay yıllarıyla birlikte çizdim (EDA).
3. **Event study (olay çalışması):** Her olay için olaydan önceki 2 yılın ortalama payını (E-2, E-1), olay yılı ve sonraki yılın ortalama payıyla (E, E+1) karşılaştırdım.
4. **Placebo testi:** Aynı hesabı 1985–2023 arasında NBA'le ilgisi olmayan isimler için de yaptım (367.599 isim-yıl gözlemi). Her olayın artışını, önceki dönemde benzer büyüklükte olan (bebek sayısı yarısı ile iki katı arası) isimlerin dağılımında bir yüzdeliğe yerleştirdim.
5. Karıştırıcı faktörleri (confounder) ayrıca inceledim.

## Bulgular

- **Kobe Etkisi gerçek.**
  - Kobe ismi, Kobe Bryant'ın draft edildiği dönemde yılda 9 bebekten (1995) 1.552'ye (2001) çıktı.
  - Ocak 2020'deki vefatından sonra tek yılda 506'dan 1.515'e yükseldi, yani 3 katına çıktı. Bu artış placebo dağılımında 99.7. yüzdelikte.
- **En güçlü etkiyi "ilk görünme" yaratıyor.** 8 draft olayının medyan yüzdeliği 99.8.
  - Kobe, Shaquille, LeBron, Kyrie ve Iverson'ın draft yıllarındaki artışlar, aynı büyüklükteki isimlerin %99'undan daha fazla.
- **Şampiyonluklar her zaman isim kazandırmıyor.** 16 şampiyonluğun sadece %31'i 95. yüzdeliği geçiyor.
  - "Lebron" ismi, LeBron James'in 2012 ve 2016 şampiyonluklarından sonra azaldı.
- **Bazı isimler oyuncuyla birlikte doğdu.** "Giannis" (ilk kez 2014) ve "Kawhi" (ilk kez 2013), oyuncular ünlü olana kadar SSA verisinde hiç yok.

| Olay türü | Olay sayısı | Medyan artış (kat) | Medyan yüzdelik | 95. yüzdelik üstü |
|---|---|---|---|---|
| Draft | 8 | 5.5 | 99.8 | %75 |
| MVP | 4 | 2.1 | 96.4 | %50 |
| Vefat | 1 | 2.8 | 99.7 | %100 |
| Şampiyonluk | 16 | 1.2 | 84.5 | %31 |

## Sınırlamalar

- **Bu gözlemsel bir analiz.** Zamanlamanın tutması, nedenselliği kanıtlamıyor. Örneğin:
  - **Zion:** İsmin asıl sıçraması, Zion Williamson doğmadan önce 1999'da.
  - **Hakeem:** İsmin sıçrama yılları, Olajuwon'un şampiyonluk yıllarına denk gelmiyor.
- **Placebo testi isim büyüklüğünü kontrol ediyor, önceden var olan trendi kontrol etmiyor.** Luka, Tatum ve Kyrie isimleri olaydan önce de yükseliyordu.
- **Veri yıllık ve sadece ABD'yi kapsıyor.** Olay sayısı az (29), bu yüzden olay türü özetleri kesin sonuç değil, eğilim olarak okunmalı.

## Dosyalar

- `101_kobe_etkisi.ipynb`: analiz notebook'u (çıktılarıyla)
- `data/names_all.csv.gz`: birleştirilmiş SSA isim verisi
- `images/`: notebook'un ürettiği grafikler

## Kullanılan araçlar

pandas, NumPy, matplotlib
