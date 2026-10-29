# YMH459 - FANUC CRX-10iA Endüstriyel Robot Analizi

**Ders:** YMH459 - Yazılım Mühendisliğinde Güncel Konular  
**Üniversite:** Fırat Üniversitesi  
**Bölüm:** Yazılım Mühendisliği  
**Öğrenci No:** 265542009  
**İncelenen Makine:** FANUC CRX-10iA İşbirlikçi Endüstriyel Robot (Cobot)

---

## 1. Projenin Amacı

Bu projenin amacı, FANUC tarafından geliştirilen CRX-10iA işbirlikçi endüstriyel robotunun teknik özelliklerini, çalışma prensiplerini, kontrol sistemlerini, işlevsel emniyet mekanizmalarını ve siber güvenlik açısından olası risklerini incelemektir.

Çalışma, üretici firmayla doğrudan iletişime geçilmeden, kamuya açık teknik dokümanlar ve mühendislik değerlendirmeleri kullanılarak **kör analiz (Blind Analysis)** yöntemiyle yürütülmektedir.

Ayrıca ders kapsamında, robotun kullanıldığı varsayımsal bir üretim hücresi için **15 başlıklı siber emniyet kanıt dosyası (Evidence Pack)** hazırlanmaktadır.

## 2. Makinenin Genel Tanıtımı

FANUC CRX-10iA, endüstriyel otomasyon uygulamalarında kullanılan altı eksenli bir işbirlikçi robottur.

### Teknik Özellikler

| Özellik | Değer |
|---|---|
| Üretici | FANUC |
| Menşei | Japonya |
| Model | CRX-10iA |
| Robot Türü | İşbirlikçi Robot (Cobot) |
| Eksen Sayısı | 6 |
| Maksimum Taşıma Kapasitesi | 10 kg |
| Erişim Mesafesi | 1249 mm |
| Kontrolör | R-30iB Plus |

### Kullanım Alanları

- Endüstriyel montaj işlemleri
- Malzeme taşıma
- Makine besleme ve boşaltma
- Paketleme ve paletleme
- Üretim otomasyonu

### Analizde Kullanılan Örnek Senaryo

Analizlerde robotun, bir konveyörden gelen kutuları tutucu yardımıyla alıp palete yerleştirdiği **varsayımsal bir paketleme hücresi** ele alınmaktadır. Konveyör, harici HMI, üretim PLC'si, bakım bilgisayarı ve ağ düzeni bu örnek senaryo için modellenmiştir; FANUC CRX-10iA'nın standart donanımı veya gerçek bir fabrika kurulumu olarak sunulmamaktadır.

## 3. Analiz Yöntemi

Çalışma kapsamında bilgiler üç grupta değerlendirilmektedir:

**Doğrulanmış Bilgiler:** Üreticinin kamuya açık teknik belgeleri ve güvenilir kaynaklarla desteklenen bilgiler.

**Mühendislik Varsayımları:** Robotun olası sistem mimarisi, kullanım senaryoları ve riskleri hakkında yapılan teorik değerlendirmeler.

**Doğrulanamayan Bilgiler:** Üreticinin kamuya açık belgelerinde bulunmayan, erişilemeyen veya kesinleştirilemeyen teknik ayrıntılar.

İlk inceleme ve makine seçimine ilişkin değerlendirmeler [Kör Analiz](Kor-Analiz.md) dosyasında yer almaktadır.

## 4. Çalışma Kapsamı

Siber emniyet dosyası, ders kapsamında belirtilen **15 Evidence Pack başlığına** göre düzenlenmektedir. Aşağıdaki bağlantılar şu ana kadar hazırlanan taslak analizlere yönlendirmektedir.

| No | Evidence Pack Başlığı | Dosya / Durum |
|---|---|---|
| 01 | Asset Inventory (Varlık Envanteri) | [Taslak analiz](01-Asset-Inventory.md) |
| 02 | Network Architecture (Ağ Mimarisi) | [Taslak analiz](02-Network-Architecture.md) |
| 03 | Safety Functions (Emniyet Fonksiyonları) | [Taslak analiz](03-Safety-Functions.md) |
| 04 | Cyber Risk Assessment (Siber Risk Analizi) | [Taslak analiz](04-Cyber-Risk-Assessment.md) |
| 05 | Zone & Conduit (Güvenlik Bölgeleri ve Geçişler) | [Taslak analiz](05-Zone-Conduit.md) |
| 06 | Remote Access Procedure (Uzaktan Erişim Prosedürü) | [Taslak analiz](06-Remote-Access-Procedure.md) |
| 07 | User/Role Matrix (Kullanıcı ve Yetki Matrisi) | [Taslak analiz](07-User-Role-Matrix.md) |
| 08 | Software/Firmware Inventory (Yazılım ve Firmware Envanteri) | LAB 5 sonrası hazırlanacak |
| 09 | SBOM (Yazılım Bileşen Listesi) | LAB 5 sonrası hazırlanacak |
| 10 | Vulnerability Records (Zafiyet Kayıtları) | LAB 5 sonrası hazırlanacak |
| 11 | Patch/Update Records (Yama ve Güncelleme Kayıtları) | LAB 5 sonrası hazırlanacak |
| 12 | Backup & Restore (Yedekleme ve Geri Yükleme) | Planlanıyor |
| 13 | Incident Response (Olay Müdahalesi) | Planlanıyor |
| 14 | Change Management (Değişiklik Yönetimi) | Planlanıyor |
| 15 | Verification/Test (Doğrulama ve Test) | Planlanıyor |

**Not:** Hazırlanan ilk yedi dosya, varsayımsal sisteme ait analiz taslaklarıdır. Gerçek bir tesiste uygulanmış veya bağımsız olarak doğrulanmış güvenlik önlemlerini ifade etmez.

## 5. Haftalık Çalışmalar

Ders kapsamında gerçekleştirilen laboratuvar uygulamaları, analiz raporları ve diğer akademik çalışmalar bu GitHub deposunda düzenli olarak paylaşılmaktadır.

Şu ana kadar hazırlanan laboratuvar çalışmaları `LAB-Calismalari` klasöründe ayrı tutulmaktadır:

- [LAB 1 – Safety Architecture](LAB-Calismalari/LAB1-Safety-Architecture.md)
- [LAB 2 – Zone / Conduit](LAB-Calismalari/LAB2-Zone-Conduit.md)
- [LAB 3 – Threat & Risk Analysis](LAB-Calismalari/LAB3-Threat-Risk-Analysis.md)
- [LAB 4 – Secure Remote Access](LAB-Calismalari/LAB4-Secure-Remote-Access.md)

Laboratuvar dosyalarıyla Evidence Pack başlıkları birbirini desteklese de ayrı çalışmalar olarak saklanmaktadır. **LAB 5 kapsamındaki yazılım, zafiyet ve güncelleme başlıkları**, ders anlatımı tamamlandıktan sonra ele alınacaktır.

## 6. Kaynaklar

- [FANUC CRX-10iA Resmî Ürün Sayfası](https://www.fanuc.eu/eu-en/product/robot/crx-10ia)
- [FANUC CRX-10iA Teknik Veri Sayfası](https://www.fanuc.eu/~/media/files/pdf/products/robots/robots-datasheets-en/collaborative%20robots/crx-10ia-en.pdf?la=en)

---

**Not:** Bu proje akademik amaçlı hazırlanmıştır. Sunulan risk senaryoları ve mühendislik değerlendirmeleri, FANUC tarafından doğrulanmış gerçek güvenlik açıklarını veya resmî güvenlik denetimi sonuçlarını temsil etmez.
