# 14 — Change Management (Değişiklik Yönetimi)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Varsayımsal paletleme hücresi.  
**Durum:** Örnek değişiklik yönetimi prosedürü; gerçek değişiklik yapılmamıştır.

## Amaç

Robot programında, PLC'de veya ağ kurallarında yapılan her değişiklik **üretimi ve çalışan emniyetini etkileyebilir**. Bu nedenle değişiklikler talep, değerlendirme, onay, uygulama ve test aşamalarından geçmelidir.

## Örnek değişiklik: CH-01

**Talep:** Robotun farklı boyutlu bir kutuyu palete yerleştirmesi için hareket programının güncellenmesi.  
**Etkilenen varlıklar:** A02 robot kontrolörü, A04 tutucu, A06 ürün sensörü, A07 PLC.  
**Olası etki:** Yanlış hareket veya tutuş; çarpma, sıkışma ya da kutu düşmesi.  
**Emniyet bağlantısı:** SF-02 koruyucu duruş ve SF-03 güvenli yeniden başlatma kontrol edilmelidir.

## Değişiklik akışı

| Aşama | Yapılacak iş | Önerilen sorumlu |
|---|---|---|
| **1. Talep** | Amaç, etkilenen cihazlar ve istenen tarih kaydedilir. | Üretim sorumlusu |
| **2. Risk incelemesi** | Hareket/yük riski, kullanıcı yetkileri ve siber etkiler değerlendirilir. | Emniyet + otomasyon |
| **3. Onay** | İş kapsamı ve bakım süresi onaylanır. | Üretim + yetkili sorumlu |
| **4. Yedekleme** | Mevcut robot programı ve gerekli ayarlar korunur. | Robot programcısı |
| **5. Kontrollü uygulama** | Değişiklik izinli bakım koşullarında yapılır; işlemler kaydedilir. | Yetkili programcı |
| **6. Doğrulama** | Hareket, PLC iletişimi ve SF-01/02/03 kontrolleri yapılır. | Emniyet + otomasyon |
| **7. Kapanış** | Test sonucu, sürüm ve üretime dönüş onayı kaydedilir. | Üretim sorumlusu |

## Kayıt ve geri dönüş

`CH-01 | Kutu boyutu için robot programı değişikliği | Risk: Hareket/yük | Durum: Örnek / uygulanmadı`

Beklenmeyen sonuçta üretime devam edilmez; `12-Backup-Restore.md` planındaki **onaylı ve güvenilir sürüme dönüş** değerlendirilir. Programın geri alınması, emniyet testlerinin atlanabileceği anlamına gelmez.

**Sonuç:** Değişiklik yönetiminin amacı işi yavaşlatmak değil, **neyin, neden, kim tarafından ve hangi kontrol sonrasında değiştiğini** gösterebilmektir. Gerçek değişiklik ve test kayıtlarımız henüz bulunmuyor.

**İlgili bölümler:** `07-User-Role-Matrix.md`, `11-Patch-Update-Records.md`, `12-Backup-Restore.md`, `15-Verification-Test.md`.  
**Ders dayanağı:** `Sunum.pdf` — Evidence Pack 14 ve RACI yaklaşımı.
