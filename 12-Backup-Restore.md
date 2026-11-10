# 12 — Backup & Restore (Yedekleme ve Geri Yükleme)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Konveyörlü varsayımsal paletleme hücresi.  
**Durum:** Önerilen yedekleme planı; gerçek yedek alınmamıştır.

## Amaç

Robotun programı bozulursa veya yanlış bir değişiklik yapılırsa **önceki güvenilir duruma dönebilmek**. Yedekleme, hem üretimin devamlılığı hem de emniyet açısından önemlidir.

## Neler yedeklenmeli?

| İçerik | İlgili varlık | Önerilen zaman | Sorumlu |
|---|---|---|---|
| Robotun görev programı ve gerekli yapılandırması | A02 / SW-02 | Her onaylı değişiklikten önce ve sonra | Robot programcısı |
| PLC uygulaması ve parametreleri | A07 / SW-03 | Her sürüm değişikliğinde | Otomasyon sorumlusu |
| HMI ekranları ve izinli ayarlar | A08 / SW-04 | Her onaylı değişiklikte | Otomasyon sorumlusu |
| Erişim geçidi / güvenlik duvarı yapılandırması | A11 / SW-06 | Ağ kuralı değiştiğinde | IT/OT yöneticisi |
| Emniyetle ilişkili ayarlar ve onay kayıtları | A09 / A02 | Yetkili değişiklik öncesi/sonrası | Emniyet sorumlusu |

**Not:** Gerçek yedekleme yöntemleri ve desteklenen dosya türleri kurulu kontrolör/yazılım sürümüne bağlıdır; bu çalışmada doğrulanmamıştır.

## Önerilen koruma ve geri yükleme akışı

1. Yedek, yetkili kişi tarafından alınır; **tarih, sürüm ve sorumlu kişi** kaydedilir.
2. Bir kopya erişimi kısıtlanmış alanda, ikinci kopya sistemden ayrı tutulur; bütünlük kontrolü yapılır.
3. Geri yükleme gerekiyorsa olayın nedeni değerlendirilir, **güvenilir yedek** seçilir.
4. Üretim uygun biçimde durdurulur; yalnız yetkili kişi geri yükleme işlemini yürütür.
5. PLC–robot iletişimi, SF-01/02/03 emniyet işlevleri ve yeniden başlatma koşulları **yerel olarak doğrulanmadan üretime dönülmez**.

## Örnek kayıt

`B-01 | Robot görev programı | Son onaylı sürüm | Sorumlu: Robot programcısı | Durum: Planlandı / gerçek yedek yok`

**Sonuç:** Yedek almak kadar **geri yüklemenin işe yaradığını test etmek** de gerekir. Bu deney henüz yapılmadığından kayıtlar doğrulanmış kanıt sayılmaz. Test yaklaşımı `15-Verification-Test.md` bölümünde ele alınacaktır.

**Ders dayanağı:** `Sunum.pdf` — Evidence Pack 12; LAB 4'ün emniyet bağımsızlığı yaklaşımı.
