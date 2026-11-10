# 11 — Patch/Update Records (Yama ve Güncelleme Kayıtları)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Varsayımsal paletleme hücresi.  
**Durum:** Örnek karar ve kayıt şablonu; gerçek cihaza yama uygulanmamıştır.

## Amaç

Bir güvenlik güncellemesi her zaman hemen yüklenmez. Endüstriyel sistemlerde güncelleme üretimi durdurabilir veya emniyetle ilgili işlevleri etkileyebilir. Bu nedenle **önce uygunluk ve risk değerlendirmesi, sonra kontrollü test, ardından izinli kurulum** gerekir.

## Örnek güncelleme karar kayıtları

| ID | Hedef | Tetikleyici | Önerilen karar | Durum |
|---|---|---|---|---|
| P-01 | SW-01 robot kontrol yazılımı | Üreticiden güvenlik duyurusu gelmesi | Etkilenen sürümü doğrula; emniyet etkisini değerlendir, test planla | Planlandı; duyuru/sürüm doğrulanmadı |
| P-02 | SW-05 bakım PC'si | İşletim sistemi güvenlik güncellemesi | Yedek al, bakım penceresinde test ederek uygula | Planlandı; kurulum yapılmadı |
| P-03 | SW-06 VPN / geçit yazılımı | Erişim yazılımında zafiyet bildirimi | Erişimi sınırla, sürümü denetle, uygun güncellemeyi test et | Planlandı; gerçek ürün bilinmiyor |

*Tablodaki P-01–P-03 gerçek yapılmış güncellemeler değil, örnek takip kayıtlarıdır.*

## Uygulamadan önce kontrol listesi

1. **Etkilenme kontrolü:** Yazılım gerçekten kurulu mu, sürümü zafiyet kapsamına giriyor mu? (`08` ve `09`)
2. **Risk:** Güvenlik açığı ve üretim/emniyet etkisi nedir? (`04` ve `10`)
3. **Yedek:** Robot programları, PLC/HMI yapılandırması ve gerekli ayarlar korundu mu? (`12`)
4. **Onay:** Bakım penceresi ve sorumlu kişi belli mi? (`07` ve `14`)
5. **Test:** Güncelleme öncesi ve sonrası fonksiyon kontrolleri planlandı mı? (`15`)
6. **Geri dönüş:** Başarısızlık durumunda üreticinin onayladığı güvenli geri alma yöntemi var mı?

## Yama yüklenemiyorsa

Uyumlu güncelleme yoksa geçici olarak **uzaktan erişimi kapatma, ilgili bağlantıyı sınırlandırma ve log takibini artırma** gibi telafi edici önlemler değerlendirilebilir. Bu önlemler robotun emniyet fonksiyonlarının yerine geçmez.

**Sonuç:** Henüz gerçek bir sürüm, tarih, uygulama kaydı veya test sonucu bulunmuyor. Bu doküman, güncelleme yapılırken tutulacak kanıtın **nasıl hazırlanacağını** gösterir.

**Ders dayanağı:** `Sunum.pdf` LAB 5; `2.1. lab_foyleri_genel.pdf` sayfa 6.
