# LAB 3 - Tehdit ve Risk Analizi (Risk Register)

**Ders:** YMH459 - Yazılım Mühendisliğinde Güncel Konular  
**Makine:** FANUC CRX-10iA işbirlikçi robot  
**Çıktı:** Risk Register (Risk Kayıt Tablosu)

## Amaç

LAB 1'de robotun çalışanı nasıl yaralayabileceğini, LAB 2'de de olası erişim noktalarını inceledim. Şimdi **hangi erişim sorunu nasıl fiziksel bir kazaya dönüşebilir?** sorusuna cevap arıyorum.

Bu çalışmada robotun paketleme hattında kutu taşıdığını varsayıyorum. Aşağıdaki bağlantı sorunları **gerçek FANUC güvenlik açıkları değil**, dersteki yöntemi uygulamak için kurduğum örneklerdir.

## 1. İncelediğim beş giriş noktası

| Kod | Giriş noktası | Durum |
|---|---|---|
| **K-01** | Robotun dokunmatik programlama arayüzü (Z4) | Arayüz var, yetki ayrıntıları bilinmiyor |
| **K-02** | Örnek hat HMI'si ve operatör hesabı (Z3) | Varsayım |
| **K-03** | Örnek servis/mühendislik bilgisayarı (Z3 → Z4) | Varsayım |
| **K-04** | Varsa uzaktan bakım bağlantısı (C2, Z2) | Varsayım |
| **K-05** | Hat kontrolünden robota komut geçişi (C4, Z3 → Z4) | Varsayım |

Gerçekte açık port, zayıf parola veya dış bağlantı bulunduğunu doğrulamış değilim.

## 2. Risk puanı nasıl hesaplanıyor?

Hocanın LAB 3 yönteminde **Skor = L × S × E**:

- **L (1-3):** Erişim yolunun istismar edilmesi ne kadar kolay?
- **S (1-3):** Ortaya çıkabilecek fiziksel zarar ne kadar ağır?
- **E (1-3):** Erişim yolu dışarıya ne kadar açık?

**1-3 düşük, 4-8 orta, 9-17 yüksek, 18-27 kritik.** Fiziksel sonuç ağır yaralanmaysa **S = 3** olur; toplam puan düşük olsa da **S3** olarak ayrıca takip edilir.

## 3. Üç örnek tehdit senaryosu

### R-01 - İçeriden yetkisiz değişiklik

- **Kim?** Yetkisini aşan bir çalışan.
- **Nereden?** Varsayımsal hat HMI'si (**K-02**, Z3).
- **Ne yapıyor?** Gereğinden fazla yetkisi olduğu için hareket veya yeniden başlatma ayarını değiştiriyor.
- **Nasıl sonuçlanıyor?** Değişiklik **K-05** üzerinden robot kontrolüne ulaşır ve bağımsız emniyet koruması yetersiz kalırsa robot tehlikeli şekilde hareket edebilir.
- **Fiziksel sonuç:** Çalışan robot ile sabit yüzey arasında sıkışarak ağır yaralanabilir.

**Puan:** L=2 (erişim için hesap gerekir ama yetkiler zayıf varsayıldı), S=3 (ağır yaralanma), E=1 (yerel operatör paneli). **2 × 3 × 1 = 6, Orta, S3.**

**Önlem:** Operatöre yalnız gerekli yetkilerin verilmesi; program değişikliğinin onaylanması ve güvenli yeniden başlatmanın kontrol edilmesi.

### R-02 - Uzaktan bakım hesabının kötüye kullanılması

- **Kim?** Fırsatçı dış saldırgan.
- **Nereden?** Varsayımsal uzak bakım geçidi (**K-04**, Z2).
- **Ne yapıyor?** Ele geçirilmiş veya paylaşılan bakım hesabıyla gereğinden fazla yetki elde ediyor.
- **Nasıl sonuçlanıyor?** Bakım bağlantısından hat kontrolüne, oradan robot ayarlarına ulaşabildiği **ve** bağımsız koruma yetersiz kaldığı durumda tehlikeli hareket oluşabilir.
- **Fiziksel sonuç:** Robotun hareketi veya taşıdığı yük nedeniyle çalışan ağır yaralanabilir.

**Puan:** L=2 (ele geçirilebilen servis kimliği varsayımı), S=3 (ağır yaralanma), E=2 (kontrollü dış erişim). **2 × 3 × 2 = 12, Yüksek, S3.**

**Önlem:** Kişisel hesap, MFA, VPN, jump server, süreli bakım izni ve oturum kaydı. Ayrıca emniyetin bakım bağlantısından bağımsız korunması gerekir.

### R-03 - Servis bilgisayarından hatalı program yüklenmesi

- **Kim?** Tedarik zinciri üzerinden gelen tehdit.
- **Nereden?** Varsayımsal servis bilgisayarı (**K-03**, Z3 → Z4).
- **Ne yapıyor?** Kaynağı doğrulanmamış bir program veya ayar dosyası robota yükleniyor.
- **Nasıl sonuçlanıyor?** Robot beklenmedik hareket eder ve ayrı emniyet önlemleri bunu engelleyemezse çalışan tehlikeye girer.
- **Fiziksel sonuç:** Robot veya yük nedeniyle ağır yaralanma meydana gelebilir.

**Puan:** L=1 (dosyanın değiştirilmesi ve bakımda yüklenmesi gibi birden fazla koşul), S=3 (ağır yaralanma), E=1 (yerel servis erişimi). **1 × 3 × 1 = 3, Düşük, ama S3.**

**Önlem:** Dosya kaynağını kontrol etmek, değişiklikleri onaylamak, test etmek ve bakım kayıtlarını tutmak.

## 4. Risk kayıt tablosu

| Risk | Saldırgan profili | Giriş | L | S | E | Puan | Öncelik |
|---|---|---|---:|---:|---:|---:|---|
| **R-02** | Fırsatçı dış | K-04 | 2 | 3 | 2 | **12** | Yüksek - S3 |
| **R-01** | İçeriden | K-02, K-05 | 2 | 3 | 1 | **6** | Orta - S3 |
| **R-03** | Tedarik zinciri | K-03 | 1 | 3 | 1 | **3** | Düşük - S3 |

| Risk | Önerdiğim sorumlu ekip | İlk yapılacak iş |
|---|---|---|
| R-02 | OT/IT ve bakım | Uzaktan erişim yetkilerini düzenlemek |
| R-01 | Otomasyon / üretim | Kullanıcı yetkilerini sınırlandırmak |
| R-03 | Bakım / yazılım | Güncelleme ve programları test etmek |

Bu roller ve puanlar bir işletmede doğrulanmış görevler veya ölçülmüş riskler değildir; örnek çalışmaya aittir.

## 5. Föyün son iki sorusu

**En yüksek öncelikli risk hangisi?**  
**R-02**; çünkü örnek bakım yolu dış erişime de açıldığı ve ağır yaralanmaya yol açabilecek değişikliklere ulaşabildiği varsayıldığı için puanı **12** çıktı.

**S=3 olduğu hâlde düşük puanlı senaryo var mı?**  
Evet. **R-03'ün puanı 3.** Fakat sonucu ağır yaralanma olabileceği için **S3 bayrağıyla** takip edilmesi gerekiyor.

## Sonuç

LAB 3'te gördüğüm şey, her siber olayın emniyet riski olmadığı. Riskin fiziksel bir zarara nasıl yol açacağını da açıklamak gerekiyor. LAB 4'te en yüksek puanlı **R-02** için daha güvenli bir uzaktan erişim düzeni inceleyeceğim.

## Kaynaklar

- Ders materyali: *LAB3.pdf* (senaryo yöntemi, L/S/E ölçekleri, Risk Register).
- Ders materyali: *2.1. lab_foyleri_genel.pdf*, sayfa 4 (LAB 3).
- Önceki çalışmalar: `LAB1-Safety-Architecture.md`, `LAB2-Zone-Conduit.md`.
- [FANUC CRX-10iA resmî ürün sayfası](https://www.fanuc.eu/tr-tr/urun/robot/crx-10ia) (ürün özellikleri; varsayımsal risklerin kanıtı değildir).
