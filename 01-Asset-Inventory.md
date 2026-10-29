# 01 — Asset Inventory (Varlık Envanteri)

**Makine:** FANUC CRX-10iA işbirlikçi robot  
**Senaryo:** Robotun kutuları konveyörden alıp palete yerleştirdiği örnek bir üretim hücresi.  
**Çalışma:** Kör analiz — gerçek fabrika kurulumu değildir.

## Varlık listesi

| ID | Varlık | Görevi / önemi | Bilgi durumu |
|---|---|---|---|
| A01 | FANUC CRX-10iA robot kolu | Kutuları taşır; hareketi insan emniyetini etkiler. | Model doğrulanmış |
| A02 | R-30iB Plus robot kontrolörü | Robot hareket ve görev programlarını kontrol eder. | Ürün bilgisi |
| A03 | Dokunmatik programlama paneli | Robotun programlanması ve yerel yönetimi için arayüzdür. | Ürün bilgisi |
| A04 | Kutu tutucu (gripper) | Kutuyu kavrayıp bırakır. | Varsayım |
| A05 | Konveyör | Kutuları robotun alma noktasına getirir. | Varsayım |
| A06 | Ürün algılama sensörü | Kutunun hazır olduğunu algılar. | Varsayım |
| A07 | Üretim PLC'si | Konveyör ve hücre sırasını yönetir. | Varsayım |
| A08 | Operatör paneli (HMI) | Çalışma durumunu gösterir, izinli komutları alır. | Varsayım |
| A09 | Emniyet donanımı / fonksiyonları | Tehlikeli durumda koruyucu duruşu sağlar. | Ayrıntısı bilinmiyor |
| A10 | Bakım bilgisayarı | Yetkili bakım ve program değişikliği için kullanılır. | Varsayım |
| A11 | Ağ cihazları ve erişim geçidi | Hücreyi diğer ağlara kontrollü bağlar; uzaktan erişim varsa sınırlar. | Varsayım |

## Kısa değerlendirme

Öncelikle robot kolu, kontrolörü ve emniyetle ilgili işlevler korunmalıdır; çünkü bu bileşenlerin hatalı çalışması fiziksel yaralanmaya neden olabilir. Operatör paneli ve bakım erişimi de yetkisiz değişikliklere karşı önemlidir.

**Not:** FANUC'un gerçek bir kurulumundaki ağ cihazları, harici Safety PLC varlığı, kullanıcı hesapları ve yazılım sürümleri bilinmemektedir. Bunlar burada gerçek bulgu gibi sunulmamıştır. Ayrıntılı ağ çizimi **02-Network-Architecture**, emniyet analizi **03-Safety-Functions**, kullanıcı yetkileri ise **07-User-Role-Matrix** altında ele alınacaktır.

**Dayanak:** YMH459 dersinin *Sunum.pdf* ve *2.1. lab_foyleri_genel.pdf* LAB 2 örnekleri; FANUC CRX-10iA kamuya açık ürün bilgileri.
