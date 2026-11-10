# 13 — Incident Response (Siber Olay Müdahalesi)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Varsayımsal paletleme hücresi.  
**Durum:** Masa başı olay müdahale senaryosu; gerçek bir olay yaşanmamıştır.

## Örnek olay

Saat **10.15'te**, uzaktan bakım hesabında beklenmeyen bir oturum tespit edildiği varsayılsın. Robot kontrolörüne erişilip erişilmediği ve programın değişip değişmediği bilinmiyor. Bu durum `04-Cyber-Risk-Assessment.md` içindeki **R-02** senaryosuyla ilişkilidir.

**Öncelik:** Önce çalışanların fiziksel emniyeti, sonra olayın sınırlandırılması ve kanıtların korunmasıdır. Belirsiz durumda robotun güvenli biçimde durdurulması ve üretime dönüşün yerel yetkilendirmeyle yapılması gerekir.

## Önerilen müdahale planı

| Zaman / aşama | Yapılacaklar | Sorumlu |
|---|---|---|
| **İlk 15 dakika** | Üretim ve emniyet sorumlularını bilgilendir; robotun güvenli durumunu kontrol et; şüpheli uzak bağlantıyı sınırlandır. | Üretim + emniyet + IT/OT |
| **İlk 2 saat** | Oturum loglarını, kullanıcı ve cihaz saatlerini, program sürümlerini koru; şüpheli hesabı askıya al; değişiklik olup olmadığını incele. | IT/OT + bakım |
| **Aynı gün** | Olayın giriş yolunu ve olası fiziksel etkisini araştır; `R-02` riskini yeniden değerlendir. | IT/OT + emniyet |
| **İyileştirme** | Güvenilir yedekleri ve onaylı programı karşılaştır; gerekli düzeltmeleri yetkili onayla uygula. | Robot programcısı + bakım |
| **Üretime dönüş** | SF-01, SF-02, SF-03 ve robot–PLC haberleşmesi doğrulanınca üretim sorumlusundan izin al. | Emniyet + üretim |

## Kanıt listesi

- VPN/DMZ erişim ve oturum kayıtları (A11)
- Bakım bilgisayarının ilgili kayıtları (A10)
- Robot görev programının değişiklik ve yedek bilgileri (A02)
- Olayı fark eden kişinin saati ve açıklaması
- Alınan kararlar, sorumlular ve üretime dönüş onayı

**Önemli:** Kanıtları korumadan cihazları rastgele sıfırlamak incelemeyi zorlaştırabilir. Bununla birlikte fiziksel tehlike varsa **kanıt toplamak için güvenli durdurma geciktirilmez**.

## Bildirim ve kapanış

Dersin LAB 6 örneğindeki **24 saat / 72 saat / 14 gün** zaman çizelgesi bir **eğitim senaryosu** olarak dikkate alınabilir. Gerçek bir işletmede hangi yasal bildirimin zorunlu olduğu; olayın, ürünün ve sorumlu kuruluşun kapsamına göre ayrıca değerlendirilir.

**Sonuç:** Olay kapatılmadan önce neden, etki, alınan önlem ve tekrarını önleme planı kayıt altına alınır. Bu dosya gerçek bir müdahale tutanağı değildir.

**Ders dayanağı:** `Sunum.pdf` LAB 6 ve Evidence Pack 13; `2.1. lab_foyleri_genel.pdf` sayfa 7.
