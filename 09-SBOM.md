# 09 — SBOM (Yazılım Bileşen Listesi)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Varsayımsal paletleme hücresi.  
**Durum:** Örnek SBOM taslağı; üreticinin gerçek SBOM'u elde edilmemiştir.

## SBOM nedir?

**Software Bill of Materials (SBOM)**, bir yazılımın hangi alt bileşenlerden oluştuğunu gösteren listedir. Bir güvenlik açığı duyurulduğunda önce **o bileşen bizim sistemimizde var mı?** diye bakarız.

`08-Software-Firmware-Inventory.md` tüm yazılım ürünlerini listeler. **SBOM ise bir ürünün içindeki kütüphanelere ve bağımlılıklara iner.** Bu iki envanter aynı şey değildir.

## İncelenecek örnek bileşenler

| Üst ürün | Alt bileşen / bağımlılık | Sürüm | Durum |
|---|---|---|---|
| SW-01 — Robot kontrol yazılımı | Gömülü işletim sistemi / yazılım modülleri | Bilinmiyor | Gerçek bileşen listesi mevcut değil |
| SW-03 — PLC uygulaması | PLC çalışma zamanı ve kullanılan modüller | Bilinmiyor | Varsayımsal hücre; doğrulanmalı |
| SW-04 — HMI uygulaması | Arayüz kütüphaneleri / haberleşme modülleri | Bilinmiyor | Varsayımsal hücre; doğrulanmalı |
| SW-05 — Bakım PC'si | İşletim sistemi ve bakım yazılımı bağımlılıkları | Bilinmiyor | Varsayımsal hücre; doğrulanmalı |
| SW-06 — VPN / bakım geçidi | VPN yazılımı ve ilgili bileşenler | Bilinmiyor | Önerilen mimari; doğrulanmalı |

*Tablodaki alt bileşenler, kuruldukları doğrulanmış paket adları değil, SBOM hazırlanırken araştırılacak kategorilerdir.*

## Bir CVE kaydını nasıl değerlendiririz?

Bir bileşene ait güvenlik duyurusu gördüğümüzde şu sırayı izleriz:

1. **Bileşen var mı?** Gerçek SBOM veya cihaz kayıtlarından kontrol et.
2. **Etkilenen sürüm mü?** Duyurudaki sürüm aralığıyla eşleştir.
3. **Açık kullanılabilir mi?** İlgili servis veya erişim yolu bizim mimaride ulaşılabilir mi?
4. **Emniyet etkisi var mı?** Robotun hareketine, koruyucu duruşuna veya yeniden başlatmasına etki edebilir mi?

Bu üç teknik koşul (varlık, sürüm, erişilebilirlik) doğrulanmadan **"CRX-10iA bu CVE'den etkileniyor"** denilemez.

## Eksikler ve sonuç

Üreticiye ait gerçek alt bileşenler, lisanslar, sürümler ve bağımlılık ilişkileri bilinmiyor. Bu nedenle **tam veya doğrulanmış SBOM hazırladığımızı iddia etmiyoruz.** Mevcut çalışma, nasıl bir SBOM toplanacağını ve güvenlik açığı değerlendirmesinde nasıl kullanılacağını gösteren akademik taslaktır.

**İlgili çalışma:** `10-Vulnerability-Records.md`.  
**Ders dayanağı:** `Sunum.pdf` LAB 5; `2.1. lab_foyleri_genel.pdf` LAB 5.
