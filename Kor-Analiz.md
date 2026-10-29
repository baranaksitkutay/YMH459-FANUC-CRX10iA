# FANUC CRX-10iA - Kör Analiz

**Ders:** YMH459 - Yazılım Mühendisliğinde Güncel Konular  
**Makine:** FANUC CRX-10iA İşbirlikçi Endüstriyel Robot (Cobot)  
**Çalışma:** Kamuya açık kaynaklarla ön inceleme

## 1. Bu makineyi neden inceliyorum?

CRX-10iA, üretimde malzeme taşıma, makine besleme ve paketleme gibi işlerde kullanılabilen bir robot kolu. Bu çalışmada robotun temel özelliklerini, nasıl çalıştığını ve iş güvenliği açısından nelere dikkat edilmesi gerektiğini inceliyorum.

**Kör analiz** kapsamında üreticiden özel bilgi istemeden, açık kaynaklardaki bilgileri kullanıyorum. Robotun belirli bir fabrikadaki kurulumunu görmediğim için bazı ayrıntıları kesin olarak bilemiyorum.

## 2. Temel özellikler

| Özellik | Bilgi |
|---|---|
| Üretici | FANUC (Japonya) |
| Model | CRX-10iA |
| Robot türü | İşbirlikçi robot (cobot) |
| Eksen sayısı | 6 |
| Taşıma kapasitesi | 10 kg |
| Erişim mesafesi | 1.249 mm |
| Kontrolör ailesi | R-30iB Plus |
| Programlama | Dokunmatik arayüzde sürükle-bırak |

Bu bilgiler üreticinin ürün tanıtımına dayanmaktadır. CRX-10iA ile **CRX-10iA/L** farklı modellerdir; burada CRX-10iA'yı ele alıyorum.

## 3. Nasıl çalışabilir? Örnek senaryo

Analizi somutlaştırmak için robotun bir **paketleme hattında kutuları taşıdığını varsayıyorum**:

1. Konveyör, kutuyu robotun alabileceği noktaya getirir.
2. Robot kolu, uygun bir tutucuyla kutuyu kavrar.
3. Programlanan hareketi yaparak kutuyu palete bırakır.
4. Uygun ve güvenli koşullarda aynı işlem tekrarlanır.

**Bu bir örnektir.** Konveyörün, tutucunun ve ürün sensörünün gerçek bir CRX-10iA kurulumunda hangi modelde kullanıldığını bilmiyorum. Robotun kendisi ile fabrikaya sonradan eklenen ekipmanları birbirinden ayırıyorum.

## 4. İlk emniyet değerlendirmesi

İşbirlikçi robotlar insanlarla yakın çalışabilse de her kullanım kendiliğinden güvenli sayılmaz. Çalışma alanına ve taşınan yüke göre ayrıca değerlendirme yapmak gerekir.

| Olası tehlike | Neye dikkat edilmeli? |
|---|---|
| Robot kolunun çalışana çarpması | Güvenli hareket ve duruş koşulları |
| Kol ile sabit yüzey arasında sıkışma | Çalışma alanının ve korumaların değerlendirilmesi |
| Kutunun tutucudan düşmesi | Yükün güvenli kavranması |
| Beklenmeyen yeniden başlama | Yeniden başlatma koşullarının kontrol edilmesi |

Üretici robotta **temas algılama** özelliği bulunduğunu belirtiyor. Ancak bunun tek başına bütün bir paketleme hattının güvenli olduğunu gösterdiğini söyleyemem.

## 5. Yazılım ve siber güvenlik açısından ilk sorularım

Robotun hareketleri kontrolör ve görev programlarıyla yönetiliyor. Bu yüzden şu konuların incelenmesi gerektiğini düşünüyorum:

- Robot programlarını ve ayarlarını kim değiştirebiliyor?
- Operatör ile bakım personelinin yetkileri farklı mı?
- Fabrika ağına veya uzaktan bakım sistemine bağlantı var mı?
- Yetkisiz bir değişiklik yapılırsa emniyet fonksiyonları bundan etkilenebilir mi?

Bunlar **inceleme sorularıdır**. CRX-10iA'da açık bir internet portu, zayıf parola veya doğrulanmış bir güvenlik açığı bulunduğunu iddia etmiyorum. Böyle bir sonuca varmak için gerçek kurulum ve teknik kanıt gerekir.

## 6. Bildiklerim, varsaydıklarım, bilmediklerim

| Durum | Örnek |
|---|---|
| **Kamuya açık bilgi** | 6 eksen, 10 kg taşıma kapasitesi, dokunmatik programlama |
| **Benim varsayımım** | Kutuları konveyörden alıp palete yerleştiren bir fabrika hattı |
| **Henüz bilmiyorum** | Gerçek ağ bağlantıları, yazılım sürümü, harici sensörler ve emniyet kontrolünün ayrıntıları |

## 7. Sonuç ve devam planı

İlk incelememde robotun sadece hareketlerini değil, **çalışanın tehlikeli hareketlerden nasıl korunacağını** da anlamam gerektiğini gördüm. Bu nedenle sonraki çalışmaları şu sırayla ele alıyorum:

- **LAB 1:** Emniyet mimarisi ve tehlikeli durumlar
- **LAB 2:** Olası cihazlar, ağ bölgeleri ve bağlantılar
- **LAB 3:** Tehdit senaryoları ve risk puanlaması
- **LAB 4:** Güvenli uzaktan erişim gereksinimleri

Bu dosya başlangıç incelemesidir. Ayrıntılı cevaplar ve varsayımsal teknik çizimler ilgili LAB dosyalarındadır.

## Kaynaklar

- [FANUC - CRX-10iA ürün sayfası](https://www.fanuc.eu/tr-tr/urun/robot/crx-10ia)
- [FANUC America - CRX-10iA](https://www.fanucamerica.com/products/robots/series/collaborative-robot/crx-10ia)
- Ders materyalleri: *Sunum.pdf* ve *2.1. lab_foyleri_genel.pdf*

> Bu metin eğitim amaçlı ön değerlendirmedir; gerçek bir fabrika incelemesi veya sertifikasyon raporu değildir.
