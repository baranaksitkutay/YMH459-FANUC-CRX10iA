# FANUC CRX-10iA — Kör Analiz (İlk Taslak)

**Ders:** YMH459 — Yazılım Mühendisliğinde Güncel Konular  
**Makine:** FANUC CRX-10iA İşbirlikçi Endüstriyel Robot (Cobot)  
**Çalışma türü:** Kamuya açık kaynaklarla bağımsız teknik değerlendirme  
**Tarih:** 23.10.2026  
**Sürüm:** 0.1 — Ön analiz

> **Kapsam:** Bu rapor, üretici firma veya sektör temsilcilerinden özel bilgi talep edilmeden hazırlanmıştır. Robotun gerçek bir fabrikadaki kurulumu incelenmemiştir. Doğrulanmış bilgiler, tasarım varsayımları ve bilinmeyen ayrıntılar ayrı gösterilir. Bu bir sertifikasyon veya gerçek sisteme yönelik sızma testi değildir.

## 1. Çalışmanın amacı

FANUC CRX-10iA modelinin çalışma prensibini ve olası endüstriyel kullanımını incelemek; insan emniyetini ilgilendiren tehlikeleri, emniyet fonksiyonlarını, dijital bağımlılıkları ve siber güvenlikle kesişen noktaları ön değerlendirme düzeyinde ortaya koymak.

Çalışma, laboratuvarlarda ele alınan **Safety Architecture (Emniyet Mimarisi)**, **Safety Function Map (Emniyet Fonksiyon Haritası)**, **Zone / Conduit (Bölge / Kontrollü Geçiş)** ve **Risk Register (Risk Kaydı)** çalışmalarına temel hazırlamak amacıyla düzenlenmiştir.

## 2. Kaynak ve kanıt yöntemi

Bu dosyadaki ifadeler şu üç gruba ayrılır:

- **[D] Doğrulanmış:** Kamuya açık üretici sayfasında veya erişilebilir teknik kaynaklarda doğrudan belirtiliyor.
- **[V] Varsayım:** Bir uygulama senaryosu kurmak veya olası riskleri tartışmak için yapılan mühendislik çıkarımı.
- **[B] Bilinmiyor:** Kamuya açık kaynaklarla, seçilen makinenin belirli bir kurulumunda doğrulanmamış ayrıntı.

**Yöntem kuralı:** [V] veya [B] bilgileri FANUC'un gerçek ürün açığı, kurulumu ya da zayıflığı gibi sunulmaz.

## 3. Makinenin genel tanıtımı

FANUC CRX-10iA, insanlarla ortak çalışma alanında kullanılmaya yönelik tasarlanmış, altı eksenli bir endüstriyel robot koludur. Üreticinin açıklamalarına göre dokunmatik kumanda arayüzünde sürükle-bırak programlama ve hassas temas algılama özelliklerine sahiptir.

| Özellik | Bilgi | Durum |
|---|---|---|
| Üretici | FANUC | [D] |
| Model | CRX-10iA | [D] |
| Tür | İşbirlikçi endüstriyel robot (cobot) | [D] |
| Eksen sayısı | 6 | [D] |
| Azami taşıma kapasitesi | 10 kg | [D] |
| Erişim mesafesi | 1.249 mm | [D] |
| Kontrolör ailesi | R-30iB Plus | [D] |
| Programlama | Dokunmatik arayüzle sürükle-bırak | [D] |
| Temas algılama | Üreticinin belirttiği hassas temas algılama | [D] |
| İnternete açık uzaktan bakım portu | Bilgi doğrulanmadı | [B] |
| Kurulu bir Safety PLC'nin marka/modeli | Bilgi doğrulanmadı | [B] |
| Kullanılan yazılım/firmware sürümü | Belirli bir cihaz için bilinmiyor | [B] |

**Not:** CRX-10iA ile erişim mesafesi farklı olan **CRX-10iA/L** modeli karıştırılmamalıdır.

## 4. Örnek kullanım senaryosu — varsayımsal

**[V] Senaryo:** Robot bir paketleme hattında, banttan gelen ve uygun şekilde kavranabilen paketleri alarak belirlenmiş bir palet konumuna yerleştiriyor. Robotun görevi şişeleri doldurmak değil, paketlenmiş ürünleri taşımak.

Örnek işlem sırası:

1. Hat, taşıma noktasına bir paket getirir.
2. Ürün varlığı, kurulumda uygun bir algılama sistemi varsa denetlenir.
3. Robot kontrolörü önceden tanımlanmış hareket programını yürütür.
4. Uç efektör/tutucu paketi kavrar ve palet üzerine bırakır.
5. Döngü güvenli çalışma koşulları sağlanıyorsa tekrarlanır.

Bu senaryonun tutucu modeli, sensör tipi, konveyör protokolü ve üretim hızı **bilinmemektedir**. Bunlar gerçek FANUC CRX-10iA kurulumuna ait tespitler değildir.

## 5. Olası sistem bileşenleri ve bilgi düzeyi

| Bileşen / unsur | Rolü | Durum |
|---|---|---|
| 6 eksenli robot kolu | Fiziksel hareketi gerçekleştirir | [D] |
| R-30iB Plus kontrolör | Robot hareketlerinin kontrolü ve program çalıştırma | [D] |
| Tablet tipi programlama arayüzü | Operatörün robot hareketlerini tanımlaması | [D] |
| Temas algılama özelliği | İşbirlikçi kullanımda temasın algılanmasına yardımcı olur | [D] |
| Ürünü kavrayan tutucu | Varsayımsal paket taşıma uygulaması | [V] |
| Konveyör ve ürün algılama sensörü | Varsayımsal hat entegrasyonu | [V] |
| Harici emniyet tarayıcısı / koruyucu kapı | Risk değerlendirmesine bağlı olası ek koruma | [V] |
| Uzaktan erişim / bulut bağlantısı | Bu kurulum için kanıt yok | [B] |
| Bağımsız Safety PLC topolojisi | Bu kurulum için kanıt yok | [B] |

## 6. LAB 1 için ön değerlendirme — Safety Function Map

Aşağıdaki sekiz başlık, ders föyündeki soruların **CRX-10iA'ya uyarlanmış ilk cevaplarıdır**. Tam bir doğrulama için uygulamanın risk değerlendirmesi ve ayrıntılı emniyet dokümantasyonu gerekir.

### 6.1. İnsan hangi tehlikeden zarar görebilir?

Robot kolu ile sabit bir yüzey arasında **sıkışma/ezilme**, hareket sırasında **çarpma** ve taşınan paketin veya tutucunun neden olduğu **düşme/çarpma** riskleri düşünülebilir. Tehlikenin büyüklüğü; hız, yük, tutucu tasarımı, çevre ekipmanı ve operatörün konumuna bağlıdır. **[V]**

### 6.2. Safety function (emniyet fonksiyonu) hangisidir?

Üretici, robotun hassas **temas algılama** özelliğini belirtmektedir. **[D]** Tehlikeli bir durumda hareketin güvenli biçimde durdurulması değerlendirmemizin merkezindeki emniyet hedefidir. Bunun yanında acil durdurma veya ilave alan korumasının seçilen kurulumda nasıl uygulandığı ayrıca doğrulanmalıdır. **[B]**

### 6.3. Safety-related control system nerede?

Robotun güvenlikle ilişkili kontrol fonksiyonları ve ilgili donanımının kesin mimarisini yalnızca ürün tanıtımından çıkaramıyoruz. **[B]** Bu nedenle dersteki örnek şemada görülen **ayrı Safety PLC** yapısının CRX-10iA'nın içinde veya yanında mutlaka bulunduğu varsayılmıyor.

**Kavramsal akış (gerçek bağlantı şeması değildir):**

- Normal kontrol: Operatör programı → Robot kontrolörü → Robot hareketi / tutucu.
- Emniyet hedefi: Tehlikeli durumun algılanması → Emniyetle ilgili kontrol fonksiyonu → Tehlikeli hareketin güvenli biçimde durdurulması.

### 6.4. Normal kontrol ile emniyet kontrolü arasındaki fark nedir?

**Normal kontrol**, üretimin planlanan sıra ve hareketlerle devam etmesini sağlar. **Emniyet kontrolü**, anormal/tehlikeli koşullarda insanı korumaya yöneliktir. Emniyet fonksiyonunun güvenilirliği ve kontrolün normal üretim yazılımından ne kadar bağımsız olduğu ayrıca değerlendirilmelidir.

### 6.5. PLr / SIL neden önemlidir?

PLr (gerekli performans seviyesi) ve SIL (emniyet bütünlük seviyesi), korumanın riskle orantılı güvenilirlik gereksinimini belirlemeye yarar. Yalnızca robot modeli ve taşıma kapasitesine bakarak belirli bir çalışma hücresinin PLr/SIL değeri atanamaz; uygulama temelli risk değerlendirmesi gerekir. **[B]**

### 6.6. Safe state (güvenli durum) nedir?

Bu senaryoda güvenli durum, **insan için tehlike oluşturan robot hareketinin güvenli biçimde durdurulmasıdır**. Yükün tutulması veya düşmemesi gibi hususlar da tutucu ve uygulama tasarımına göre ayrıca değerlendirilmelidir. **[V]**

### 6.7. Emniyet fonksiyonunun hangi dijital bağımlılıkları olabilir?

Kavramsal olarak kontrolör yazılımı, kayıtlı programlar, hareket ve güvenlikle ilgili parametrelerin yönetimi, operatör yetkileri ve varsa harici entegrasyonlar değerlendirilir. **[V]** Ancak bunların hangilerinin emniyet fonksiyonuna etki edebildiği ve gerçek cihazın yazılım sürümleri **bilinmiyor**. **[B]**

### 6.8. Siber müdahale emniyeti hangi noktadan bozabilir?

**Koşullu senaryo:** Bir kurulumda yetkisiz kişinin hareket veya güvenlikle ilgili parametrelere erişebildiği varsayılırsa, tehlikeli hareket koşulları oluşabilir. Robotun başka bir sisteme bağlandığı durumda o bağlantı da değerlendirme kapsamına alınır. **[V]**

**Önemli:** Bu, CRX-10iA üzerinde keşfedilmiş bir güvenlik açığı veya FANUC'un internete açık bir portu olduğu iddiası değildir. Gerçek saldırı yüzeyi, erişim topolojisi ve yetki mekanizmaları henüz **doğrulanmamıştır**. **[B]**

## 7. Ön risk listesi — puanlama öncesi

Henüz LAB 2 varlık/envanter çalışması yapılmadığından aşağıdaki riskler için **L × S × E puanı verilmemiştir**.

| Risk adayı | Olası fiziksel sonuç | Açıklama |
|---|---|---|
| Robot ve sabit yüzey arasında sıkışma | Ezilme yaralanması | [V] Kurulum yerleşimine bağlı |
| Robotun taşıdığı paketin düşmesi | Çarpma/yaralanma | [V] Tutucu tasarımına ve yüke bağlı |
| Yetkisiz hareket parametresi değişikliği | Beklenmeyen hareket nedeniyle yaralanma | [V] Ancak ilgili erişimin mümkün olduğu doğrulanmadı |
| Hatalı yeniden başlatma düzeni | Operatör yakınındayken tehlikeli hareket | [V] Entegrasyon tasarımına bağlı |

## 8. Açık sorular ve sonraki doğrulamalar

- [ ] Kullanılacak uygulama (paketleme, makine besleme vb.) kesinleştirilecek.
- [ ] Üreticinin kamuya açık emniyet/kullanım dokümanları incelenecek.
- [ ] Acil durdurma, temas algılama ve harici koruma seçenekleri kaynaklarla ayrıştırılacak.
- [ ] Harici ağ, yazılım sürümü ve kullanıcı rolleri hakkında yalnızca doğrulanabilen bilgiler envantere yazılacak.
- [ ] LAB 2'de varsayımsal bir **Zone / Conduit** mimarisi çizilecek; gerçek kurulum olduğu iddia edilmeyecek.
- [ ] LAB 3'te en az üç tehdit senaryosu, dayandığı giriş noktasıyla birlikte yazılacak ve puanlanacak.

## 9. Sonuç

İlk kör analiz, CRX-10iA'nın robot hareketi ve işbirlikçi kullanımı nedeniyle **işlevsel emniyet** bakımından incelenmeye uygun bir makine olduğunu göstermektedir. Kamuya açık ürün bilgileri temel özellikleri ortaya koyarken, belirli bir fabrikanın ağ topolojisini, kullanılan kontrol yazılımı sürümünü ve emniyet sistemi ayrıntılarını **kanıtlamamaktadır**. Bu eksikler ayrıca kaydedilmeli; varsayımsal tehditler gerçek güvenlik açığı gibi sunulmamalıdır.

## 10. Açık kaynaklar

1. [FANUC Türkiye — CRX-10iA ürün sayfası](https://www.fanuc.eu/tr-tr/urun/robot/crx-10ia) — Model, 6 eksen, 10 kg, 1249 mm, kontrolör, kullanım ve temas algılama bilgileri.
2. [FANUC America — CRX-10iA](https://www.fanucamerica.com/products/robots/series/collaborative-robot/crx-10ia) — Uygulama alanları ve teknik özelliklerin ikinci üretici kaynağı.
3. Ders kapsamında sağlanan *Safety 4.0 Bootcamp* sunumu ve *Genel Laboratuvar Föyleri* — LAB 1 soru yapısı ve sonraki analiz çıktıları için başvuru materyali (dosyaların kendisi bu depoda paylaşılmamıştır).

---

*Bu doküman yaşayan bir akademik çalışma dosyasıdır. Sonraki sürümlerde doğrulanan bilgiler, yeni kaynaklar ve laboratuvar çıktıları eklenecektir.*
