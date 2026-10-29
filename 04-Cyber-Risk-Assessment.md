# 04 — Cyber Risk Assessment (Siber Risk Analizi)

**Makine:** FANUC CRX-10iA  
**Senaryo:** Konveyörden kutu alıp palete yerleştiren varsayımsal robot hücresi.  
**Çıktı:** Risk Register (Risk Kayıt Tablosu) — kör analiz.

## Amaç ve kapsam

`01-Asset-Inventory` içindeki cihazlar, `02-Network-Architecture` içindeki bağlantılar ve `03-Safety-Functions` içindeki emniyet fonksiyonları birlikte değerlendirildi. Amaç, olası bir siber müdahalenin **hangi fiziksel tehlikeye dönüşebileceğini** incelemektir. Buradaki açıklıklar ve puanlar **FANUC'ta tespit edilmiş gerçek zafiyetler değildir**; ders için oluşturulmuş koşullu senaryolardır.

## 1. Olası giriş noktaları

| Kod | Giriş noktası | İlgili varlık / bölge |
|---|---|---|
| K-01 | Robotun dokunmatik programlama paneli | A03 / Z4 |
| K-02 | Harici hat HMI'si ve kullanıcı hesabı | A08 / Z3 |
| K-03 | Servis / mühendislik bilgisayarı | A10 / Z3–Z4 |
| K-04 | Varsayımsal uzaktan bakım geçidi | A11 / Z2 |
| K-05 | Üretim PLC'si ile robot kontrolörü arasındaki komut bağlantısı | A07–A02 / Z3–Z4 |

Bu noktaların açık, zayıf parolalı veya yetkisiz erişime uygun olduğu **doğrulanmamıştır**.

## 2. Risk puanlama yöntemi

Hocanın LAB 3 yöntemine göre **Risk = L × S × E**; her değişken **1–3** arasındadır.

- **L:** Giriş noktasını istismar etmek ne kadar kolay? (1 zor, 3 kolay)
- **S:** Olası fiziksel sonucun şiddeti nedir? (1 yaralanma yok, 3 ağır yaralanma)
- **E:** Giriş noktasına erişim ne kadar açık? (1 yerel, 3 doğrudan dışa açık)

**1–3 Düşük · 4–8 Orta · 9–17 Yüksek · 18–27 Kritik.** S=3 olan her kayıt, puanı düşük olsa bile ayrıca **S3** olarak izlenir.

## 3. Risk Register

| Risk | Tehdit profili ve giriş | Olası zincir → fiziksel sonuç | L | S | E | Skor / öncelik |
|---|---|---|---:|---:|---:|---|
| **R-02** | Fırsatçı dış saldırgan; **K-04** | Bakım hesabı ele geçirilir → yetkisiz robot ayarı değiştirilir → koruyucu duruş yetersiz kalırsa çalışan robot/yük nedeniyle ağır yaralanabilir (**SF-02**). | 2 | 3 | 2 | **12 / Yüksek · S3** |
| **R-01** | Yetkisini aşan çalışan; **K-02, K-05** | HMI'dan uygunsuz başlatma komutu/ayar değişikliği → robot kontrolüne ulaşır → güvenli yeniden başlatma sağlanamazsa çalışan sıkışabilir (**SF-03**). | 2 | 3 | 1 | **6 / Orta · S3** |
| **R-03** | Tedarik zinciri kaynaklı tehdit; **K-03** | Kaynağı doğrulanmamış program bakım PC'sinden yüklenir → beklenmedik hareket → koruma yetersizse çalışan ağır yaralanabilir (**SF-02**). | 1 | 3 | 1 | **3 / Düşük · S3** |

**Puanların gerekçesi:**

- **R-02:** L=2 (hesap ele geçirilmesi varsayılıyor), S=3 (ağır yaralanma), E=2 (kontrollü dış bakım yolu).
- **R-01:** L=2 (yetki sınırının zayıf olduğu varsayılıyor), S=3 (sıkışma sonucu ağır yaralanma), E=1 (yerel HMI).
- **R-03:** L=1 (zararlı dosyanın ayrıca bakım sürecinde yüklenmesi gerekiyor), S=3 (ağır yaralanma), E=1 (yerel servis erişimi).

## 4. Önerilen önlemler ve sorumlular

| Risk | İlk önlem | Önerilen sorumlu | Takip |
|---|---|---|---|
| R-02 | Kişisel servis hesabı, VPN + MFA, DMZ/jump server, süreli izin ve oturum kaydı | IT / OT / bakım | Öncelikli |
| R-01 | HMI yetkilerini sınırlama, değişiklik onayı, güvenli yeniden başlatma | Otomasyon / üretim | Planlı |
| R-03 | Program kaynağını doğrulama, yükleme öncesi test ve kayıt | Bakım / yazılım | Her güncellemede |

**Mevcut önlemler:** Gerçek tesiste neyin kurulu olduğu bilinmiyor. `02-Network-Architecture` dosyasındaki VPN/MFA/DMZ yapısı **önerilen mimaridir**, uygulandığı doğrulanmış bir koruma değildir. Bu nedenle puanlar varsayımsal başlangıç koşullarına aittir; önlemler uygulandıktan sonra **artık risk yeniden puanlanmalıdır**. Özellikle S3 kayıtları önlem veya yazılı kabul olmadan kapatılmamalıdır.

## Sonuç

En yüksek puanlı senaryo **R-02 (12, Yüksek)** oldu. Ancak **R-03'ün puanı 3 olsa bile S3 bayrağı** taşıması gerekir. Kritik ders: Siber olayın emniyet riski sayılması için, **etkilenen emniyet fonksiyonunu ve olası fiziksel sonucu** açıklamak gerekir. Bir sonraki adımda geçiş kuralları `05-Zone-Conduit`, uzak bakım tedbirleri `06-Remote-Access-Procedure` altında ele alınacaktır.

**Ders dayanağı:** `LAB3.pdf` (tehdit senaryosu, L/S/E ve S3 kuralı); `2.1. lab_foyleri_genel.pdf` sayfa 4; önceki `LAB3-Threat-Risk-Analysis.md` çalışması.
