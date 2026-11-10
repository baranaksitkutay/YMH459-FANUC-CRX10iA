# 08 — Software/Firmware Inventory (Yazılım ve Firmware Envanteri)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Konveyörden kutu alıp palete yerleştiren varsayımsal robot hücresi.  
**Durum:** Kör analiz; gerçek cihazlardan yazılım sürümü okunmamıştır.

## Amaç

`01-Asset-Inventory.md` bölümünde fiziksel cihazları listeledik. Burada ise **o cihazların çalışmasını sağlayan yazılımları** ele alıyoruz. *Firmware*, cihazın içinde çalışan gömülü yazılımdır. Sürüm bilgisi bilinmezse hangi güvenlik uyarısının bizi ilgilendirdiğine karar vermek zorlaşır.

## Örnek yazılım envanteri

| ID | İlgili varlık | Yazılım / firmware | Sürüm | Bilgi durumu |
|---|---|---|---|---|
| SW-01 | A02 — Robot kontrolörü | Robot kontrol yazılımı | **Bilinmiyor** | Yazılım türü beklenir, gerçek sürüm doğrulanmadı |
| SW-02 | A02 / A03 | Robotun paletleme görev programı | **Bilinmiyor** | Örnek hücre varsayımı |
| SW-03 | A07 — Üretim PLC'si | PLC uygulama programı ve firmware | **Bilinmiyor** | Varsayım |
| SW-04 | A08 — Harici HMI | Operatör ekran yazılımı | **Bilinmiyor** | Varsayım |
| SW-05 | A10 — Bakım PC'si | İşletim sistemi ve bakım araçları | **Bilinmiyor** | Varsayım |
| SW-06 | A11 — Ağ / bakım geçidi | Firewall ve VPN yazılımı | **Bilinmiyor** | Önerilen mimari varsayımı |

**Önemli:** Tablo, FANUC'un gerçek yazılım paketlerinin tam listesi değildir. Özellikle PLC, harici HMI, bakım PC'si ve VPN geçidi robotun standart parçası olarak gösterilmemektedir.

## Gerçek bir tesiste ne kaydedilirdi?

Her bileşen için **üretici, ürün adı, sürüm/build numarası, cihaz ID'si, en son güncelleme tarihi, destek durumu ve bilgi kaynağı** tutulurdu. Bu veriler yetkili cihaz ekranından veya bakım kayıtlarından doğrulanırdı. Kör analizde bunları ölçmediğimiz için sürüm numarası uydurmuyoruz.

## Güvenlik açısından değerlendirme

- **SW-01 ve SW-02:** Yetkisiz değişiklik beklenmeyen robot hareketine yol açabilir; `03-Safety-Functions.md` ile ilişkilidir.
- **SW-03 / SW-04:** Üretim komutları ve operatör yetkileri korunmalıdır.
- **SW-05 / SW-06:** Yetkisiz uzak bakım, `04-Cyber-Risk-Assessment.md` içindeki **R-02 ve R-03** senaryolarıyla ilişkilidir.

**Sonuç:** Yazılım envanteri, sonraki `09-SBOM.md`, `10-Vulnerability-Records.md` ve `11-Patch-Update-Records.md` çalışmalarının başlangıç listesidir. **Henüz doğrulanmış sürüm veya güncelleme kaydı yoktur.**

**Ders dayanağı:** `Sunum.pdf` — Evidence Pack 08; LAB 5 — SBOM/CVE/Patch.
