# LAB 3 — Tehdit ve Risk Analizi (Risk Register)

**Ders:** YMH459 — Yazılım Mühendisliğinde Güncel Konular  
**Makine:** FANUC CRX-10iA İşbirlikçi Endüstriyel Robot (Cobot)  
**Tarih:** 23 Ekim 2026  
**Çıktı:** Risk Register (Risk Kayıt Tablosu)  
**Durum:** Sürüm 0.1 — kör analiz / varsayımsal endüstriyel kurulum

> **Önemli:** Bu belge, dersin LAB 3 föyünü FANUC CRX-10iA'ya uyarlayan bir **eğitim çalışmasıdır**. Gerçek bir FANUC kurulumuna erişilmemiş, üreticiyle görüşülmemiş, sızma testi yapılmamıştır. Bu rapordaki saldırı yolları, zayıf yapılandırmalar ve risk puanları **varsayımsal senaryolardır**; FANUC ürününde tespit edilmiş gerçek açıklar veya gerçek bir fabrikanın riskleri değildir. Makinenin yerleşimi, ağ topolojisi ve erişim yetkileri doğrulanmadan nihai risk puanı verilemez.

## 1. Amaç ve yöntem

LAB 1'de korunması gereken emniyet işlevlerini, LAB 2'de ise varsayımsal ağ bölgelerini ve olası erişim yollarını belirledik. Bu laboratuvarda **olası erişim yolu × korunması gereken emniyet işlevi** eşleşmelerinden risk senaryoları çıkarıyoruz.

Ders notlarındaki beş parçalı senaryo yöntemi uygulanmıştır:

1. **Profil:** Kim?
2. **Giriş:** Hangi erişim noktası?
3. **Eylem:** Ne yapar?
4. **Zincir:** Hangi aşamalar üzerinden ilerler, hangi emniyet fonksiyonu etkilenebilir?
5. **Sonuç:** İnsan için somut **fiziksel** etki ne olabilir?

Yalnızca veri kaybıyla veya üretimin durmasıyla biten bir anlatım, bu föyde aranan fiziksel emniyet riskini tek başına açıklamaz.

### Bilgi işaretleri

- **[D]:** Kamuya açık bilgiyle doğrulanmış.
- **[V]:** Örnek fabrika entegrasyonunda varsayılmış.
- **[B]:** Doğrulanmamış / bilinmiyor.

## 2. İncelenen makine ve emniyet hedefi

**[D]** FANUC CRX-10iA; 6 eksenli ve 10 kg taşıma kapasitesine sahip bir işbirlikçi robottur. Üretici tarafından dokunmatik programlama arayüzü ve temas algılama özelliği belirtilmektedir.

**[V] Eğitim senaryomuz:** Robot, bir paketleme hattında kutuları konveyörden alıp palete yerleştiriyor. Tutucu, konveyör, hat HMI'si, varsa mühendislik dizüstü bilgisayarı ve varsa dış bakım bağlantısı bu **örnek entegrasyonun** parçalarıdır; robotun standart kurulumunda bulunduğu iddia edilmez.

LAB 1'e göre başlıca fiziksel tehlike adayları:

- Hareketli robot kolu veya tutucuyla **çarpışma**.
- Robotla sabit bir yüzey arasında **sıkışma / ezilme**.
- Tutulan bir paketin düşmesi nedeniyle **yaralanma**.
- İşçi tehlike bölgesindeyken kontrolsüz **yeniden başlama**.

**Emniyet hedefi (LAB 1):** Tehlike oluştuğunda zararlı hareketi emniyetli biçimde durdurmak ve güvenli koşullar sağlanmadan yeniden başlatmamak. Robotun gerçek kurulumunda bunun hangi donanım/yazılım sınırlarıyla sağlandığı **[B]** bilinmemektedir.

## 3. LAB 2 envanterindeki olası giriş noktaları

LAB 3 föyü, risk senaryosundan önce **en az beş kapının** envanterde gösterilmesini istiyor. Aşağıdakiler LAB 2'deki varsayımsal topolojiye dayanır.

| Kapı ID | Envanterdeki varlık / bağlantı | LAB 2 bölgesi | Ulaşım biçimi | Kanıt |
|---|---|---|---|---|
| **K-01** | Dokunmatik programlama arayüzü | Z4 — Robot kontrol | Makine yanında yetkili kullanıcı | Arayüz [D], belirli kullanıcı yetkileri [B] |
| **K-02** | Örnek hat HMI'si ve operatör hesabı | Z3 — Hücre kontrol | Fabrika içinden / operatör panelinden | Varlık ve haklar [V] |
| **K-03** | Örnek mühendislik / servis dizüstü bilgisayarı | Z3 → Z4 | Yerel bakım ve program yükleme yolu | [V] |
| **K-04** | Dışarıdan bakım için DMZ geçidi, **kurulmuşsa** | C2: dış bakım → Z2 DMZ | Kontrollü dış bağlantı | [V]; gerçekte varlığı [B] |
| **K-05** | Hücre kontrolünden robot kontrolörüne komut/veri geçişi | C4: Z3 → Z4 | İç ağ entegrasyonu | [V]; gerçek protokol ve erişim kuralları [B] |

**Uyarı:** Bunlar saptanmış açık portlar ya da doğrulanmış zafiyetler değil; erişim **olursa** incelenecek yüzeylerdir. Özellikle K-04 üzerinden internete doğrudan açık bir FANUC servisi olduğu ileri sürülmüyor.

## 4. Risk puanlama yöntemi

Föyde verilen **Safety 4.0 Risk Matrix** kullanılır:

**Risk skoru = L × S × E** (her parametre 1 ile 3 arasında).

| Ölçüt | 1 | 2 | 3 |
|---|---|---|---|
| **L — İstismar edilebilirlik** | Zor: özel bilgi/birden fazla engel gerekir | Orta: örn. zayıf veya ele geçirilebilir kimlik bilgisi | Kolay: örn. varsayılan parola veya korumasız erişim |
| **S — Fiziksel sonucun şiddeti** | Yaralanma yok; üretim/ekipman etkisi | Hafif, geri dönüşlü yaralanma | Ağır/kalıcı yaralanma veya ölüm potansiyeli |
| **E — Dışa açıklık** | Yerel fiziksel erişim | Kurumsal/fabrika ağı ya da kontrollü dış erişim | İnternete doğrudan/sürekli açık erişim |

| Skor | Öncelik |
|---|---|
| **18–27** | Kritik |
| **9–17** | Yüksek |
| **4–8** | Orta |
| **1–3** | Düşük |

**S3 kuralı:** S = 3 olan senaryo, çarpım küçük çıksa bile **S3 bayrağı** ile ayrıca görünür tutulur; önlem veya belgelenmiş kabul değerlendirmesi olmadan kapatılmaz.

**Puanların sınırı:** Burada her sayı, **açıkça belirtilen örnek yapılandırma doğru olsaydı** geçerli olacak eğitim puanıdır. Gerçek FANUC kurulumu için ölçülmüş olasılık veya risk seviyesi değildir.

## 5. Üç tehdit senaryosu

### R-01 — İçeriden aşırı yetkiyle hareket programının değiştirilmesi

- **Profil:** Meraklı / yetkisini aşan içeriden çalışan.
- **Giriş (kapı):** **K-02** — Varsayımsal hat HMI'sinde yetkileri gereğinden geniş operatör hesabı.
- **Eylem:** Kendisine tanımlanmaması gereken hareket veya yeniden başlatma komutlarını değiştirir.
- **Zincir:** Fazla yetkili operatör hesabı → Z3 hat arayüzü → **K-05** üzerinden Z4 robot programı/hareket isteği → **eğer** kurulumun emniyet sınırlamaları ve yeniden başlatma koruması bu değişikliği bağımsız olarak engellemiyorsa tehlikeli hareket.
- **Etkilenen emniyet hedefi:** İnsan tehlikeli bölgede olduğunda hareketin güvenli şekilde durdurulması / güvenli yeniden başlatma.
- **Fiziksel sonuç:** Yakındaki çalışanın robot kolu ile sabit yüzey arasında sıkışıp **ağır yaralanması**.

**Varsayımlar:** [V] HMI mevcut; hesaplar gereğinden geniş yetkili; değişiklik Z4'e iletilebiliyor; ilgili tehlikeli hareket bağımsız emniyet önlemleriyle engellenmiyor. Bunlar FANUC'a ilişkin gerçek bulgu değildir.

**Puan gerekçesi:**

- **L = 2:** Yetkiyi kötüye kullanmak için hesaba erişim gerekli; örnek senaryoda hesap/rol sınırlandırması yetersiz.
- **S = 3:** Robotun ezme/sıkıştırma etkisi ciddi veya kalıcı yaralanmaya yol açabilir.
- **E = 1:** K-02 erişimi bu örnekte fabrika içindeki fiziksel operatör paneliyle sınırlı.

**Skor: 2 × 3 × 1 = 6 → Orta, S3 bayrağı.**

**Önerilen önlem:** Rol tabanlı en az yetki, değişiklik onayı/kaydı, güvenli yeniden başlatma koşullarının doğrulanması; emniyetin sıradan üretim komutlarından bağımsız korunması.

### R-02 — Zayıf varsayımsal uzak bakım hesabından uygunsuz değişiklik

- **Profil:** Fırsatçı dış saldırgan.
- **Giriş (kapı):** **K-04** — Dış bakımın kullanıldığı **örnek bir kurulumda** ele geçirilmiş/paylaşılan servis hesabı.
- **Eylem:** Bakım oturumundaki gereğinden geniş yetkileri kullanarak hücre/robot ayarlarına uygunsuz değişiklik yaptırır.
- **Zincir:** Kontrollü dış erişim yolu **bulunuyorsa** → Z2 DMZ → Z3 bakım/HMI arayüzü → **K-05** Z4 robot kontrolü → korumaların kurulumda hatalı ayrıştırıldığı durumda tehlikeli hareket veya uygunsuz yeniden başlatma.
- **Etkilenen emniyet hedefi:** İnsan çalışma alanındayken tehlikeli hareketin durdurulması / izinsiz yeniden başlatmanın engellenmesi.
- **Fiziksel sonuç:** Robot yakınındaki operatörün kol hareketinden veya taşıdığı yükten **ağır şekilde yaralanması**.

**Varsayımlar:** [V] Örnek tesiste uzaktan bakım vardır; hesap paylaşılır veya çalınmıştır; MFA eksik/etkisizdir; bakım rolü fazla geniştir; emniyet bağımsızlığı yetersizdir. **LAB 2'de önerilen hedef mimari** (kişisel hesap, MFA, sınırlı erişim, kayıt) bu zayıf başlangıç durumundan daha güvenlidir. FANUC ürününde böyle bir açık saptanmamıştır.

**Puan gerekçesi:**

- **L = 2:** Saldırganın kullanılabilir servis kimliği edinmesi gerekir; örnekte paylaşılan/zayıf hesap vardır.
- **S = 3:** Korumalar da başarısız olursa fiziksel ağır yaralanma olası sonuçtur.
- **E = 2:** Örnekte dış bakım, aracı/kontrollü erişim katmanından geçer; robot internete doğrudan açık kabul edilmez.

**Skor: 2 × 3 × 2 = 12 → Yüksek, S3 bayrağı.**

**Önerilen önlem:** Kişisel hesap, MFA, jump server, süre sınırlı erişim, tam oturum kaydı, değişikliklerin çift onayı; ayrıca emniyet fonksiyonlarının erişim yolu ele geçirilse de korunması.

### R-03 — Servis bilgisayarından denetlenmemiş program yüklenmesi

- **Profil:** Tedarik zinciri / servis aracı kaynaklı tehdit.
- **Giriş (kapı):** **K-03** — Varsayımsal mühendislik veya servis dizüstü bilgisayarı.
- **Eylem:** İçeriği doğrulanmamış bir robot görev programı veya konfigürasyon dosyası yüklenir.
- **Zincir:** Servis bilgisayarındaki değiştirilmiş dosya → yetkili bakım sırasında K-03 üzerinden Z4'e aktarım → robot hareket dizisinin beklenenden farklı olması → **eğer** bağımsız emniyet sınırlamaları riski önleyemiyorsa çalışma alanında tehlikeli hareket.
- **Etkilenen emniyet hedefi:** Hareketin güvenli sınırlar içinde tutulması ve insanı tehlikeli harekete maruz bırakmama.
- **Fiziksel sonuç:** Bakım sırasında yakındaki operatörün hareketli robot veya yük nedeniyle **ağır yaralanması**.

**Varsayımlar:** [V] Bu tesiste servis bilgisayarıyla dosya aktarımı yapılır; dosya bütünlüğü doğrulanmaz; kontrol ve emniyet sınırları bu durumu yeterince önleyemez. Ürünün doğrulanmış bir zafiyeti değildir.

**Puan gerekçesi:**

- **L = 1:** Örnekte servis dosyasının değiştirilmesi ve yetkili bakım oturumunda yüklenmesi gibi birden fazla ön koşul gerekir.
- **S = 3:** Hatalı tehlikeli hareket ağır fiziksel yaralanmayla sonuçlanabilir.
- **E = 1:** K-03 için yerel, fiziksel servis erişimi gerektiği varsayılmıştır.

**Skor: 1 × 3 × 1 = 3 → Düşük, ancak S3 bayrağı nedeniyle ayrıca izlenir.**

**Önerilen önlem:** Dosya bütünlüğü ve kaynak doğrulaması, değişiklik onayı, test ortamında deneme, sürüm ve yükleme kayıtları, bakım sonrası emniyet doğrulaması.

## 6. Risk Register — toplu kayıt

**Değerlendirme tarihi:** 23.10.2026  
**Makine:** FANUC CRX-10iA; belirli fabrika/sürüm: **bilinmiyor**  
**Kanıt olgunluğu:** Varsayımsal eğitim senaryosu / **taslak**

| Risk ID | Profil | Kapı ve bölge | Etkilenen emniyet hedefi | L | S | E | Skor | Bant | S3? |
|---|---|---|---|---:|---:|---:|---:|---|---|
| **R-02** | Fırsatçı dış | K-04: dış bakım → Z2; K-05 → Z4 | Tehlikeli hareketi durdurma / güvenli yeniden başlatma | 2 | 3 | 2 | **12** | **Yüksek** | **Evet** |
| **R-01** | Meraklı içeriden | K-02: Z3 HMI; K-05 → Z4 | Tehlikeli hareketi durdurma / yeniden başlatmayı engelleme | 2 | 3 | 1 | **6** | **Orta** | **Evet** |
| **R-03** | Tedarik zinciri | K-03: yerel servis → Z4 | Güvenli hareket sınırları | 1 | 3 | 1 | **3** | **Düşük** | **Evet** |

> Bunlar **birbiriyle tutarlı, fakat varsayımsal başlangıç yapılandırmalarının** puanlarıdır. LAB 2'de çizilen **hedef güvenli mimari uygulanmış** olsaydı, ilgili girişlerin L ve/veya E değerleri yeniden puanlanırdı. Risk puanı gerçek bir kurulum için nihai kabul kararı değildir.

### Risk eylem listesi

| Risk | Önerilen risk sahibi (rol) | Öncelikli eylem | Kanıt / kontrol | Durum |
|---|---|---|---|---|
| R-02 | OT / IT sorumlusu, yönetim onayıyla | Uzak erişimde kişisel hesap, MFA ve oturum denetimi | Erişim prosedürü ve oturum kayıtları | Taslak |
| R-01 | Hücre/otomasyon sorumlusu | Operatör yetkilerini sınırlandırma, güvenli yeniden başlatmayı doğrulama | Rol matrisi, test tutanağı | Taslak |
| R-03 | Bakım ve yazılım değişiklik sorumlusu | Servis dosyalarını doğrulama ve yükleme öncesi test | Değişiklik onayı, dosya bütünlük kaydı | Taslak |

**Hedef tarih:** Bu çalışma gerçek bir işletme üzerinde yapılmadığından sorumlular atanmış ve tarihler onaylanmış değildir. Gerçek bir projede risk sahibinin ve hedef tarihin işletme tarafından belirlenmesi gerekir.

## 7. Föy sorularına cevaplar

### 7.1. En yüksek öncelikli senaryonuz hangisi, neden?

**R-02** seçilmiştir. Çünkü bu **varsayımsal** senaryoda bakım yolu dış erişime de açılmakta (E = 2), kullanılabilir fakat zayıf servis kimliği gerektirmekte (L = 2) ve bağımsız emniyet başarısız olursa ağır fiziksel yaralanmaya yol açabilmektedir (S = 3). Skor **12 (Yüksek)** ile üç örneğin en büyüğüdür.

### 7.2. S = 3 olup skoru düşük kalan bir senaryonuz var mı?

**Evet: R-03, skor 3 (Düşük).** Bununla birlikte ağır yaralanma potansiyeli olduğundan **S3 bayrağı** konmuştur. Sayısal bant düşük olsa da ayrı izlenecek ve ilgili önlemler değerlendirilmeden kapatılmayacaktır.

### 7.3. Bu senaryolarda hangi sorular henüz açık?

- Gerçek kurulumda dış bakım erişimi, HMI ve servis bilgisayarı var mı?
- Robot kontrolörü ile ilgili gerçek program/yetki sınırları neler?
- Güvenlikle ilgili parametreler hangi şartlarda ve kimler tarafından değiştirilebiliyor?
- Robotun hareketini durduran emniyet fonksiyonları, normal programdan ne düzeyde bağımsız?
- Uygulamanın risk değerlendirmesi, güvenlik mesafeleri ve güvenli yeniden başlatma koşulları nasıl tanımlanmış?

Bu sorular yanıtlanmadan gerçek ürün için zafiyet iddiası, kesin saldırı olasılığı veya uygunluk kararı verilmez.

## 8. Mevcut (varsayımsal) ve hedef mimari ayrımı

| Başlık | Örnek zayıf başlangıç | LAB 2 hedef mimarisi |
|---|---|---|
| Operatör yetkileri | Geniş tanımlanmış rol | En az yetki, rol ayrımı, değişiklik kayıtları |
| Uzaktan bakım | Paylaşılan veya ele geçirilmiş hesap | Kişisel hesap + MFA + jump server + süre sınırlaması |
| Servis dosyaları | Kaynağı/bütünlüğü doğrulanmamış aktarım | Onaylı, bütünlüğü doğrulanan ve test edilen değişiklik |
| Emniyet | Bağımsız korumanın yeterliliği **bilinmiyor** | Emniyetin yetkisiz üretim/bakım kontrolünden etkilenmemesini doğrulama |

Önlemlerin gerçek sistemde etkili olduğunu söylemek için yalnızca önerilmeleri değil, **uygulanmaları ve testlerle doğrulanmaları** gerekir.

## 9. Sonuç ve LAB 4'e geçiş

Üç farklı profil üzerinden üç risk senaryosu oluşturulmuş; her birinde **giriş kapısı**, **eylem**, **olay zinciri**, **korunan emniyet fonksiyonu**, **fiziksel sonuç**, **L / S / E gerekçeleri** ve **S3 bayrağı** belirtilmiştir.

**LAB 4'te** en yüksek örnek skorlu **R-02** senaryosunu ele alarak güvenli uzaktan erişim gereksinimlerini ve emniyetin kontrol ağından bağımsız korunması ilkesini değerlendireceğiz.

## 10. Kaynaklar

**Ders materyalleri:**

1. *LAB3.pdf*, özellikle s. 11–20 (senaryo), s. 23–30 (L/S/E ölçekleri, S3), s. 33 ve s. 43–45 (Risk Register ve değerlendirme).
2. *2.1. lab_foyleri_genel.pdf*, s. 4, LAB 3 — üç senaryo, L × S × E ve iki değerlendirme sorusu.
3. *Sunum.pdf*, LAB 3 — Threat & Risk Lab + Safety 4.0 Risk Matrix.
4. *LAB1-Safety-Architecture.md* — korunacak emniyet işlevleri.
5. *LAB2-Zone-Conduit.md* — varsayımsal varlık envanteri ve bölgeler.

**Kamuya açık üretici kaynağı:**

6. [FANUC — CRX-10iA ürün sayfası](https://www.fanuc.eu/tr-tr/urun/robot/crx-10ia) — modelin genel teknik özellikleri. Bu kaynak **varsayımsal siber senaryoların gerçek olduğunu doğrulamaz**.

---

*Bu çalışma eğitim amaçlı kör analiz taslağıdır; ürün güvenlik uyarısı, sertifikasyon veya sızma testi raporu değildir.*
