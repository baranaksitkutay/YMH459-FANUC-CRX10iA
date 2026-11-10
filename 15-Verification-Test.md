# 15 — Verification/Test (Doğrulama ve Test)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Konveyörlü varsayımsal paletleme hücresi.  
**Durum:** **Test planı**; gerçek robotta test yapılmamıştır.

## Amaç

Önceki klasörlerde birçok kontrol **önerdik**: VPN/MFA, kullanıcı yetkileri, emniyet fonksiyonları ve yedekleme gibi. Bu bölümün sorusu şudur: **"Önerdiğimiz önlemlerin çalıştığını nasıl kanıtlarız?"**

## Önerilen doğrulama planı

| Test | Kontrol edilecek konu | Beklenen sonuç | Durum |
|---|---|---|---|
| **T-01** | Operatör hesabıyla robot programı değiştirme denemesi | Yetkisiz değişiklik reddedilir. | Planlandı |
| **T-02** | Onaysız uzak bakım bağlantısı | VPN/MFA ve izin olmadan erişim verilmez. | Planlandı |
| **T-03** | Bakım oturumu sonu | Oturum kaydı oluşur, geçici yetki kapanır. | Planlandı |
| **T-04** | Acil durdurma — SF-01 | Tehlikeli robot hareketi tanımlı güvenli biçimde durur. | Planlandı |
| **T-05** | Koruyucu cihaz — SF-02 | Tehlikeli hareket uygun koruyucu duruşa geçer. | Planlandı |
| **T-06** | Yeniden başlatma — SF-03 | Tehlike giderilmeden ve gerekli onay alınmadan robot başlamaz. | Planlandı |
| **T-07** | Yedek geri yükleme | Yetkili geri yükleme sonrasında işlevler ve emniyet tekrar doğrulanır. | Planlandı |
| **T-08** | PLC–robot iletişim kesintisi | Hata algılanır; kontrol sistemi tanımlı güvenli davranışı gösterir. | Planlandı |

**Dikkat:** Bu tablo bir **laboratuvar test sonucu değildir**. Cihazın emniyet işlevlerine müdahale edilerek deneme yapılması risklidir; gerçek testler yetkili personel, uygun risk değerlendirmesi ve üreticinin prosedürleriyle yapılmalıdır. Özellikle SF-01–03 testlerinde yalnız "durdu" demek yeterli değildir; gerçek güvenli duruş koşulları ve gerekiyorsa durma mesafesi/süresi de doğrulanmalıdır.

## Test tutanağında hangi alanlar olmalı?

| Alan | Örnek açıklama |
|---|---|
| Test ID | T-04 |
| Gereksinim | SF-01 — Acil durdurma |
| Ön koşul | Güvenli test ortamı ve yetkili ekip |
| Beklenen sonuç | Tehlikeli hareketin güvenli biçimde durması |
| Gerçek sonuç | **Test edilmedi** |
| Kanıt | Henüz yok — ileride ölçüm/tutanak |
| Onay | Emniyet sorumlusu tarafından doğrulanmalı |

## Risklerle eşleştirme

- **R-01 / V-02:** T-01 ve T-06, yetkisiz komut ve kontrolsüz yeniden başlatma riskini ele alır.
- **R-02 / V-01:** T-02 ve T-03, uzaktan bakım erişiminin kısıtlanmasını değerlendirir.
- **R-03 / V-03:** Güncelleme veya program değişikliğinden sonra T-04–T-08 gibi ilgili kontroller tekrar planlanır.

**Sonuç:** Bu dosya tasarlanan güvenlik önlemlerinin **doğrulama planıdır**, uygulanmış testlerin kanıtı değildir. Tamamlandı sayılabilmesi için gerçek sonuçların, kanıtların ve yetkili onayların eklenmesi gerekir.

**Ders dayanağı:** `Sunum.pdf` — Evidence Pack 15; LAB 1 ve LAB 4'ün emniyet bağımsızlığı ilkeleri.
