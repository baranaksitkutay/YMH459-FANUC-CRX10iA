# 07 — User/Role Matrix (Kullanıcı ve Yetki Matrisi)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Konveyörden kutu alıp palete yerleştiren varsayımsal robot hücresi.  
**Kapsam:** Kör analiz; gerçek FANUC kullanıcı hesapları ve fabrika yetkileri bilinmiyor.

## Amaç

Her kullanıcının yalnızca işi için gereken işlemleri yapabilmesini sağlamak. Örneğin **operatör** hattı başlatabilir ancak **robot programını veya emniyet ayarlarını değiştiremez**. Böylece yanlışlıkla veya yetkisiz işlem yapılması zorlaşır.

## Önerilen kullanıcı ve yetki matrisi

**G:** Görüntüleme · **İ:** İşlem yapma · **O:** Onaylama · **—:** Yetki yok  
**İ\*:** Sadece izin ve kontrol altında işlem yapılabilir.

| Rol | Hattı izleme (A08) | Üretimi başlatma/durdurma | Robot programı (A02/A03) | Emniyet ayarları (A09) | Uzaktan bakım |
|---|---|---|---|---|---|
| **Operatör** | G | İ | — | — | — |
| **Robot programcısı** | G | İ (kontrollü test) | İ* | — | — |
| **Bakım teknisyeni** | G | — | İ* (bakım) | — | İ* |
| **Emniyet sorumlusu** | G | — | O (emniyet etkisi) | O / yerel doğrulama | — |
| **IT/OT yöneticisi** | — | — | — | — | İ (hesap ve bağlantı yönetimi) |
| **Üretim sorumlusu** | G | O (üretime dönüş) | O (iş onayı) | — | O (bakım izni) |

*Tablo, önerdiğimiz görev dağılımıdır; cihazda bu rollerin hazır tanımlı olduğunu iddia etmiyoruz. Emniyet ayarları üzerinde değişiklik gerekiyorsa ayrı değişiklik onayı, yetkili uygulayıcı ve yerel doğrulama gerekir; yalnızca bu tablo değişiklik yapma izni vermez.*

## Erişim kuralları

1. **Kişisel hesap:** Ortak `admin` hesabı kullanılmaz; her işlem kimin yaptığı belli olacak şekilde kaydedilir.
2. **En az yetki:** Operatör yalnızca HMI (A08) üzerinden günlük üretim işlemlerini yapar. FANUC programlama paneli (A03) ayrı ve daha yetkili bir arayüzdür.
3. **Uzaktan bakım:** Teknisyen, `06-Remote-Access-Procedure` içindeki **VPN + MFA → DMZ → bakım PC → robot kontrolörü** yolunu yalnızca onaylı süre boyunca kullanır.
4. **Emniyet ayrılığı:** SF-01 acil durdurma, SF-02 koruyucu duruş ve SF-03 güvenli yeniden başlatma, sıradan operatör veya uzak bakım yetkisiyle devre dışı bırakılamaz.
5. **Yetki iptali:** Bakım bitince geçici erişim kapatılır; görevden ayrılan kişilerin hesapları iptal edilir.

## Kısa örnek

Bir teknisyen robot programını güncellemek isterse **üretim sorumlusu işi onaylar**, **IT/OT yöneticisi süreli bağlantıyı açar**, **teknisyen izinli işlemi yapar**. Değişiklikten sonra gerekli yerel kontroller yapılır ve erişim kapatılır. **Hiçbir rol tek başına hem sınırsız erişim hem denetimsiz emniyet değişikliği yetkisine sahip olmamalıdır.**

**Sonuç:** Bu matriste amaç, robotu kullanan kişiyle robotun ayarlarını değiştirebilen kişiyi ayırmaktır. Gerçek hesap adları, parolalar ve cihazın erişim mekanizması doğrulanmamıştır.

**Ders dayanağı:** `Sunum.pdf` içindeki **EP 07 — User/Role Matrix** ve RACI sorumluluk yaklaşımı; önceki `02-Network-Architecture`, `03-Safety-Functions` ve `06-Remote-Access-Procedure` bölümleri.
