# Hafta 02 – Veri Analizi, Problem Tipleri ve Veri Seti Seçimi

## Dersin Amacı

Geçen hafta yapay zekâ, makine öğrenmesi ve derin öğrenme kavramlarını; kural tabanlı sistemler ile makine öğrenmesi arasındaki temel farkı inceledik.

Makine öğrenmesinde sistemin geçmiş örneklerden öğrenebilmesi için **veriye** ihtiyacı vardır.

Bu hafta şu sorulara cevap arayacağız:

- Veri ve veri seti nedir?
- Siber güvenlikte veriler nereden gelir?
- Bir veri setindeki satır ve sütunlar neyi ifade eder?
- Feature (özellik) ve label (etiket) nedir?
- Denetimli ve denetimsiz öğrenme arasındaki fark nedir?
- Sınıflandırma, kümeleme ve anomali tespiti nedir?
- Bir siber güvenlik problemi için uygun veri seti nasıl bulunur?
- Bir veri setinin projemize uygun olup olmadığını nasıl anlarız?
- Veri setini kullanmadan önce hangi özelliklerini incelemeliyiz?

Bu haftanın sonunda yalnızca hazır bir veri setini kullanmak değil, **kendi projeniz için uygun bir veri setini bulmak ve değerlendirmek** konusunda da temel bilgi sahibi olmanız amaçlanmaktadır.

---

# 1. Veri Nedir?

**Veri (data)**; bir olay, nesne, kullanıcı veya sistem hakkında elde edilen bilgilerin işlenebilir biçimde temsil edilmesidir.

Bir kullanıcının bir sisteme giriş yaptığını düşünelim.

Bu olay sırasında şu bilgiler kaydedilebilir:

| Bilgi | Örnek Değer |
|---|---|
| Kullanıcı | user01 |
| Giriş saati | 14:32 |
| IP adresi | 192.168.1.20 |
| Başarısız giriş sayısı | 2 |
| Kullanılan cihaz | Laptop |
| Konum | Ankara |
| Giriş sonucu | Başarılı |

Tek bir kullanıcı girişi bile birçok farklı veri üretebilir.

Binlerce kullanıcının bulunduğu bir sistemde bu kayıtların sayısı çok hızlı şekilde artabilir.

Makine öğrenmesi sistemleri bu tür büyük veri koleksiyonlarındaki ilişkileri ve örüntüleri analiz etmek için kullanılabilir.

---

# 2. Siber Güvenlikte Veri Nereden Gelir?

Siber güvenlik uygulamalarında farklı kaynaklardan veri elde edilebilir.

## 2.1. Ağ Trafiği

Bilgisayarlar arasındaki ağ iletişimi hakkında bilgiler içerir.

Örneğin:

- Kaynak IP adresi
- Hedef IP adresi
- Kaynak port
- Hedef port
- Protokol
- Paket sayısı
- Bağlantı süresi
- Gönderilen/alınan veri miktarı

Bu tür veriler özellikle **ağ saldırısı tespiti** çalışmalarında kullanılabilir.

---

## 2.2. Sistem ve Uygulama Logları

Bilgisayar sistemlerinde gerçekleşen olayların kayıtlarıdır.

Örneğin:

- Başarılı girişler
- Başarısız girişler
- Dosya erişimleri
- Sistem hataları
- Yetki değişiklikleri
- Uygulama aktiviteleri

Bu kayıtlar şüpheli kullanıcı veya sistem davranışlarının belirlenmesinde kullanılabilir.

---

## 2.3. E-posta Verileri

Phishing ve spam tespitinde kullanılabilir.

Bir e-postadan;

- gönderen adresi,
- konu,
- mesaj içeriği,
- bağlantılar,
- ek dosyalar,
- kullanılan kelimeler

gibi bilgiler elde edilebilir.

---

## 2.4. URL ve Web Sitesi Verileri

Phishing web sitelerinin belirlenmesinde;

- URL uzunluğu,
- özel karakterlerin kullanımı,
- alan adı özellikleri,
- HTTPS kullanımı,
- alt alan adı sayısı

gibi özelliklerden yararlanılabilir.

---

## 2.5. Dosya ve Yazılım Verileri

Zararlı yazılım (malware) tespitinde;

- dosya boyutu,
- dosya türü,
- sistem çağrıları,
- API kullanımları,
- ağ davranışları

gibi bilgiler kullanılabilir.

---

## 2.6. Kullanıcı Davranışları

Kullanıcıların sistem üzerindeki normal davranışlarından sapmalar güvenlik açısından önemli olabilir.

Örneğin:

- giriş zamanı,
- kullanılan cihaz,
- giriş yapılan konum,
- oturum süresi,
- erişilen dosyalar,
- başarısız giriş sayısı

incelenebilir.

---

# 3. Veri Seti Nedir?

Makine öğrenmesinde veriler çoğunlukla **veri seti (dataset)** adı verilen yapılarda tutulur.

Örneğin:

| Login_Attempts | Night_Login | New_Device | Country_Changed | Status |
|---:|---:|---:|---:|---|
| 2 | 0 | 0 | 0 | Normal |
| 1 | 0 | 1 | 0 | Normal |
| 18 | 1 | 1 | 1 | Attack |
| 25 | 1 | 1 | 0 | Attack |
| 3 | 0 | 0 | 0 | Normal |

Bu tabloda:

**Her satır → bir gözlem / olay**

**Her sütun → gözlem hakkında bir bilgi**

olarak düşünülebilir.

Örneğin üçüncü satır belirli bir kullanıcı giriş olayını temsil ediyor olabilir.

---

# 4. Feature (Özellik) Nedir?

Geçen hafta kısaca gördüğümüz **feature** kavramını şimdi veri seti üzerinde inceleyelim.

Feature, modelin karar verirken kullanabileceği bilgidir.

Örneğimizde:

- `Login_Attempts`
- `Night_Login`
- `New_Device`
- `Country_Changed`

birer feature'dır.

Örneğin:

```text
Login_Attempts = 18
Night_Login = 1
New_Device = 1
Country_Changed = 1
```

bir kullanıcı girişini tanımlayan özellikler olabilir.

Model bu bilgileri kullanarak girişin normal veya şüpheli olup olmadığını tahmin etmeye çalışabilir.

---

# 5. Label (Etiket) Nedir?

**Label**, modelin tahmin etmeye çalıştığı sonuçtur.

Örneğimizde:

`Status`

sütunu label'dır.

Bu sütunun değerleri:

```text
Normal
Attack
```

olabilir.

Dolayısıyla:

```text
Login_Attempts ────┐
Night_Login ────────┤
New_Device ─────────┼──→ MODEL ──→ Status
Country_Changed ────┘
       FEATURE'LAR                 LABEL
```

şeklinde düşünebiliriz.

---

# 6. Her Problemde Label Var mıdır?

Hayır.

Bu durum bizi makine öğrenmesindeki iki temel öğrenme yaklaşımına götürür:

- Denetimli öğrenme
- Denetimsiz öğrenme

---

# 7. Denetimli Öğrenme – Supervised Learning

Eğitim verilerinin doğru sonuçları önceden biliniyorsa **denetimli öğrenme (supervised learning)** yaklaşımı kullanılabilir.

Örneğin geçmiş ağ trafiği kayıtlarımız şöyle olsun:

| Kayıt | Sonuç |
|---|---|
| Kayıt 1 | Normal |
| Kayıt 2 | Attack |
| Kayıt 3 | Normal |
| Kayıt 4 | Attack |

Model hangi kayıtların normal, hangilerinin saldırı olduğunu eğitim sırasında görebilir.

Genel süreç:

```text
Feature'lar + Bilinen Label
              ↓
           Eğitim
              ↓
            Model
              ↓
           Yeni Veri
              ↓
            Tahmin
```

Örneğin model daha önce görmediği bir ağ bağlantısını:

```text
Normal
```

veya

```text
Attack
```

olarak tahmin edebilir.

---

# 8. Denetimsiz Öğrenme – Unsupervised Learning

Bazı durumlarda elimizde çok sayıda veri bulunmasına rağmen bu verilerin hangi sınıfa ait olduğu bilinmez.

Örneğin 100.000 ağ bağlantımız olabilir fakat bunların hangilerinin:

```text
Normal
Attack
```

olduğuna ilişkin label bulunmayabilir.

Bu durumda sistem;

- benzer kayıtları,
- doğal grupları,
- farklı davranışları,
- sıra dışı gözlemleri

bulmaya çalışabilir.

Genel fikir:

```text
Feature'lar
    ↓
Algoritma
    ↓
Verideki Yapı / Gruplar / Anormallikler
```

Bu yaklaşıma **denetimsiz öğrenme** denir.

---

# 9. Siber Güvenlikte Temel Problem Tipleri

Bu derste özellikle üç problem tipi üzerinde duracağız:

1. **Sınıflandırma (Classification)**
2. **Kümeleme (Clustering)**
3. **Anomali Tespiti (Anomaly Detection)**

Bunların birbirinden ayrılması önemlidir.

---

# 10. Sınıflandırma – Classification

**Sınıflandırma**, yeni bir örneğin önceden belirlenmiş sınıflardan hangisine ait olduğunu tahmin etme problemidir.

Örneğin:

```text
Yeni Ağ Trafiği
       ↓
     Model
       ↓
Normal / Attack
```

Burada sınıflar önceden bellidir.

## Siber Güvenlik Örnekleri

### Phishing Tespiti

```text
E-posta → Normal / Phishing
```

### Malware Tespiti

```text
Dosya → Benign / Malware
```

### Ağ Saldırısı Tespiti

```text
Ağ Bağlantısı → Normal / Attack
```

---

# 11. İkili ve Çok Sınıflı Sınıflandırma

## Binary Classification

İki sınıf bulunur.

Örneğin:

```text
Normal / Attack
```

veya:

```text
Legitimate / Phishing
```

Bu tür problemlere **ikili sınıflandırma** denir.

---

## Multiclass Classification

İkiden fazla sınıf bulunur.

Örneğin:

```text
Normal
DoS
DDoS
Brute Force
Botnet
Web Attack
```

Model yeni bir ağ trafiğinin bu sınıflardan hangisine ait olduğunu tahmin etmeye çalışır.

Bu tür problemlere **çok sınıflı sınıflandırma** denir.

---

# 12. Kümeleme – Clustering

Şimdi farklı bir problem düşünelim.

Elimizde binlerce ağ bağlantısı var fakat hangi bağlantının hangi davranış türüne ait olduğunu bilmiyoruz.

Yani **label yok**.

Algoritmadan birbirine benzeyen davranışları gruplamasını isteyebiliriz.

```text
             Ağ Trafiği
                 ↓
             Kümeleme
            ↙    ↓    ↘
        Küme 1 Küme 2 Küme 3
```

Burada algoritma doğrudan:

> “Küme 3 saldırıdır.”

demek zorunda değildir.

Algoritma yalnızca birbirine benzeyen kayıtları gruplamaya çalışır.

Daha sonra bir güvenlik uzmanı kümeleri inceleyebilir.

Örneğin:

```text
Küme 1 → Normal kullanıcı davranışları

Küme 2 → Yoğun veri transferi yapan kullanıcılar

Küme 3 → İncelenmesi gereken sıra dışı davranışlar
```

şeklinde yorumlanabilir.

---

# 13. Sınıflandırma ile Kümeleme Arasındaki Fark

| Sınıflandırma | Kümeleme |
|---|---|
| Genellikle label vardır | Label yoktur |
| Sınıflar önceden bellidir | Gruplar veriden ortaya çıkar |
| Yeni örneğin sınıfı tahmin edilir | Benzer örnekler gruplanır |
| Denetimli öğrenmedir | Denetimsiz öğrenmedir |

Örneğin:

**Sınıflandırma:**

> “Bu e-posta phishing mi, normal mi?”

**Kümeleme:**

> “Bu e-postalar içerisinde birbirine benzeyen gruplar var mı?”

---

# 14. Anomali Tespiti – Anomaly Detection

**Anomali**, genel davranıştan önemli ölçüde farklı olan gözlem veya davranıştır.

Bir kullanıcının normal davranışını düşünelim:

```text
Giriş saati: 08.00–18.00
Konum: Ankara
Cihaz: Kendi bilgisayarı
Günlük giriş sayısı: 2–4
```

Bir gün şu kayıt oluşsun:

```text
Saat: 03.42
Konum: Farklı ülke
Cihaz: Daha önce görülmemiş
Giriş denemesi: 48
```

Bu davranış kullanıcının normal davranışından oldukça farklıdır.

Basit şekilde:

```text
Normal davranışlar:

●  ●  ●  ●  ●  ●  ●  ●

                              X

                         Anormal davranış
```

`X` noktası bir **anomali** olarak değerlendirilebilir.

---

# 15. Anomali Her Zaman Saldırı mıdır?

**Hayır.**

Bu ayrım siber güvenlik açısından önemlidir.

Bir davranış sıra dışı olabilir fakat kötü amaçlı olmayabilir.

Örneğin kullanıcı:

- yurt dışına seyahat etmiş olabilir,
- yeni bir bilgisayar kullanıyor olabilir,
- gece çalışıyor olabilir.

Dolayısıyla:

> **Anormal davranış ≠ Kesin saldırı**

Bir anomali tespit sistemi çoğunlukla:

> “Bu davranış normal örneklerden farklıdır ve incelenmesi gerekebilir.”

şeklinde değerlendirilmelidir.

---

# 16. Üç Problem Tipini Karşılaştıralım

| Problem | Amaç | Label | Siber Güvenlik Örneği |
|---|---|---|---|
| **Sınıflandırma** | Veriyi bilinen sınıfa atamak | Genellikle var | Normal / Attack |
| **Kümeleme** | Benzer verileri gruplamak | Yok | Benzer ağ davranışlarını gruplamak |
| **Anomali Tespiti** | Sıra dışı davranışları bulmak | Her zaman gerekli değil | Şüpheli kullanıcı davranışı |

---

# 17. Hangi Problem Tipi?

## Senaryo 1

10.000 e-postamız var.

Her e-posta daha önce:

```text
Normal
Phishing
```

olarak etiketlenmiş.

Yeni e-postaların phishing olup olmadığını tahmin etmek istiyoruz.

**Problem tipi:** Sınıflandırma

---

## Senaryo 2

Elimizde binlerce kullanıcı davranışı var.

Herhangi bir label bulunmuyor.

Benzer davranış gösteren kullanıcıları gruplamak istiyoruz.

**Problem tipi:** Kümeleme

---

## Senaryo 3

Bir şirket çalışanlarının normal giriş davranışlarını biliyor.

Normal davranıştan ciddi şekilde farklı yeni girişleri belirlemek istiyor.

**Problem tipi:** Anomali Tespiti

---

## Senaryo 4

Elimizde şu sınıflara ayrılmış ağ trafiği kayıtları var:

```text
Normal
DoS
Brute Force
Botnet
```

Yeni bir ağ bağlantısının hangi gruba ait olduğunu tahmin etmek istiyoruz.

**Problem tipi:** Çok sınıflı sınıflandırma

---

# 18. Problem Tipini Belirlemek Neden Önemlidir?

Bir makine öğrenmesi projesine:

> “Hangi algoritmayı kullanalım?”

sorusuyla başlamak doğru değildir.

Önce:

> **“Hangi problemi çözmeye çalışıyoruz?”**

sorusuna cevap vermeliyiz.

Genel yaklaşım:

```text
Gerçek Dünya Problemi
        ↓
Problemi Tanımlama
        ↓
Uygun Veriyi Bulma
        ↓
Veriyi Anlama
        ↓
Problem Tipini Belirleme
        ↓
Uygun Yöntemi Seçme
        ↓
Model Geliştirme
```

Örneğin:

> “Phishing web sitelerini tespit etmek istiyorum.”

dediğimizde önce bu probleme uygun veriyi bulmamız gerekir.

Eğer elimizde daha önce:

```text
Legitimate
Phishing
```

olarak etiketlenmiş URL'ler bulunuyorsa problemimizi bir **sınıflandırma problemi** olarak ele alabiliriz.

---

# 19. Siber Güvenlik Projesi İçin Veri Seti Nasıl Bulunur?

Dönemin ikinci yarısında kendi siber güvenlik projenizi geliştireceksiniz.

Bu nedenle yalnızca öğretim elemanının verdiği hazır veri setini kullanmak değil, **kendi probleminize uygun bir veri setini bulmayı da öğrenmeniz gerekir.**

İlk kural:

> **Önce problemi belirleyin, sonra veri setini arayın.**

Yanlış yaklaşım:

```text
Bir dataset buldum.
       ↓
Bununla ne yapabilirim?
```

Daha doğru yaklaşım:

```text
Çözmek istediğim problem nedir?
            ↓
Hangi verilere ihtiyacım var?
            ↓
Bu verileri nereden bulabilirim?
            ↓
Bulduğum veri problemime uygun mu?
```

---

# 20. Örnek: Problemden Veri Setine

## Problem 1 – Phishing URL Tespiti

Amacımız:

> Bir URL'nin phishing olup olmadığını tahmin etmek.

Bu durumda aradığımız veri setinin URL veya web sitesi özellikleri içermesi gerekir.

Örneğin feature'lar:

```text
URL_Length
HTTPS
Special_Characters
Domain_Age
Subdomain_Count
```

Label:

```text
Legitimate
Phishing
```

olabilir.

---

## Problem 2 – Ağ Saldırısı Tespiti

Amacımız:

> Bir ağ bağlantısının normal mi yoksa saldırı mı olduğunu tahmin etmek.

Bekleyebileceğimiz feature'lar:

```text
Flow Duration
Packet Count
Bytes
Destination Port
Protocol
SYN Flag Count
```

Label:

```text
Normal
Attack
```

veya farklı saldırı türleri olabilir.

---

## Problem 3 – Malware Tespiti

Amacımız:

> Bir dosyanın zararlı olup olmadığını tahmin etmek.

Feature'lar:

```text
Dosya boyutu
API çağrıları
Sistem çağrıları
Dosya özellikleri
Ağ davranışları
```

Label:

```text
Benign
Malware
```

olabilir.

---

# 21. Veri Setleri Nereden Bulunabilir?

Makine öğrenmesi ve siber güvenlik çalışmalarında kullanılabilecek açık veri setleri farklı kaynaklarda bulunabilir.

Örneğin:

- **Kaggle**
- **UCI Machine Learning Repository**
- **Canadian Institute for Cybersecurity (CIC)**
- Üniversitelerin açık veri kaynakları
- Araştırma merkezlerinin veri sayfaları

Ancak internette bulunan her veri seti güvenilir veya projemiz için uygun değildir.

Bu nedenle veri setini indirmeden önce **dataset sayfasını incelemek gerekir.**

---

# 22. Veri Seti Nasıl Aranır?

Yalnızca:

```text
cyber security dataset
```

şeklinde arama yapmak çok geniş sonuçlar verebilir.

Probleme özel arama yapmak daha doğrudur.

### Phishing

```text
phishing URL dataset
```

### Ağ Saldırısı

```text
network intrusion detection dataset
```

### Malware

```text
malware detection dataset
```

### Spam

```text
spam email dataset
```

### Kullanıcı Davranışı

```text
user behavior cybersecurity dataset
```

Burada mantığımız:

```text
Problem
   ↓
Anahtar Kelimeler
   ↓
Dataset Arama
```

şeklindedir.

---

# 23. Bir Dataset Sayfasında Neye Bakmalıyız?

Bir veri setini bulduğumuzda hemen indirmemeliyiz.

Önce bazı soruların cevaplarını bulmalıyız.

---

## 23.1. Veri Seti Ne Hakkında?

İlk olarak açıklamasını okuyun.

Şu soruyu cevaplayabilmelisiniz:

> **Bu veri setinde ne kayıt altına alınmış?**

Örneğin:

- Ağ bağlantıları mı?
- URL'ler mi?
- E-postalar mı?
- Kullanıcı girişleri mi?
- Dosya davranışları mı?

Bu soruya cevap veremiyorsanız veri setini henüz yeterince anlamamışsınız demektir.

---

## 23.2. Bir Satır Neyi Temsil Ediyor?

Bu soru çok önemlidir.

Örneğin:

### Phishing Dataset

```text
1 satır → 1 URL
```

### Network Intrusion Dataset

```text
1 satır → 1 ağ bağlantısı / network flow
```

### E-mail Dataset

```text
1 satır → 1 e-posta
```

Bir satırın neyi temsil ettiğini bilmeden veriyi doğru yorumlamak mümkün değildir.

---

# 24. Kaç Kayıt Var?

Veri setinde kaç gözlem bulunduğunu kontrol edin.

Örneğin:

```text
5.000 kayıt
50.000 kayıt
1.000.000 kayıt
```

Daha fazla veri her zaman otomatik olarak daha iyi değildir.

Çok büyük veri setleri;

- daha uzun işlem süresi,
- daha fazla bellek kullanımı,
- daha uzun model eğitim süresi

gerektirebilir.

Özellikle eğitim amaçlı projelerde **yönetilebilir büyüklükte veri setleri** tercih edilmelidir.

---

# 25. Kaç Feature Var?

Veri setindeki sütunları inceleyin.

Örneğin bir ağ güvenliği veri setinde:

```text
Flow Duration
Destination Port
Packet Count
Bytes per Second
SYN Flag Count
ACK Flag Count
```

gibi feature'lar bulunabilir.

Burada önemli soru:

> **Bu feature'lar çözmek istediğim problemle ilişkili mi?**

Bir phishing projesi yapıyorsanız URL veya web sitesiyle ilgili özellikler görmeniz beklenir.

---

# 26. Label Var mı?

Özellikle **sınıflandırma** projesi yapacaksanız bu soru önemlidir.

Örneğin:

| URL_Length | HTTPS | Domain_Age | Label |
|---:|---:|---:|---|
| 42 | 1 | 850 | Legitimate |
| 125 | 0 | 3 | Phishing |

Burada:

`Label`

sütunu modelin tahmin etmeye çalışacağı sonucu göstermektedir.

Ancak veri setinde yalnızca:

```text
URL_Length
HTTPS
Domain_Age
```

bulunuyor ve hangi URL'nin phishing olduğu bilinmiyorsa aynı şekilde denetimli sınıflandırma modeli oluşturamayız.

---

# 27. Hangi Sınıflar Var?

Label'ın bulunması tek başına yeterli değildir.

Hangi sınıfları içerdiğini de incelemeliyiz.

Örneğin:

```text
Normal
Attack
```

iki sınıflı bir problem olabilir.

Başka bir veri setinde:

```text
Normal
DoS
DDoS
Brute Force
Botnet
Web Attack
```

bulunabilir.

Bu durumda çok sınıflı bir sınıflandırma problemi oluşturulabilir.

---

# 28. Sınıflar Dengeli mi?

Şu veri setini düşünelim:

```text
Normal : 9.900
Attack :   100
```

Toplam:

```text
10.000 kayıt
```

Verinin %99'u normal sınıfındadır.

Bir model:

> “Her şey Normal.”

derse bile kayıtların büyük bölümünde doğru sonuç üretmiş gibi görünebilir.

Ancak hiçbir saldırıyı tespit edemediği için güvenlik açısından kullanışlı değildir.

Bu probleme **sınıf dengesizliği (class imbalance)** denir.

Bu problemi ilerleyen haftalarda daha ayrıntılı inceleyeceğiz.

Şimdilik veri seti seçerken:

> **Sınıfların dağılımı nasıl?**

sorusunu sormamız yeterlidir.

---

# 29. Dosya Formatı Nedir?

Veri setleri farklı dosya formatlarında bulunabilir:

```text
.csv
.xlsx
.json
.txt
.pcap
```

Bu derste başlangıçta özellikle **CSV** formatındaki veri setlerini tercih edeceğiz.

Çünkü CSV dosyalarını Python ve Pandas ile kolayca açabiliriz.

Örneğin:

```python
import pandas as pd

df = pd.read_csv("dataset.csv")
```

Bu kodun nasıl çalıştığını **Hafta 03'te** ayrıntılı olarak öğreneceğiz.

---

# 30. Veri Setinin Boyutu Uygun mu?

Dosyanın boyutuna dikkat edilmelidir.

Örneğin:

```text
5 MB
50 MB
5 GB
```

aynı şey değildir.

5 GB büyüklüğündeki bir veri seti araştırma açısından değerli olabilir ancak öğrenci projesi için gereksiz derecede büyük olabilir.

Gerekirse büyük bir veri setinin daha küçük bir bölümü kullanılabilir.

---

# 31. Eksik Değerler Var mı?

Gerçek veri setleri her zaman kusursuz değildir.

Örneğin:

| Duration | Packets | Protocol | Label |
|---:|---:|---|---|
| 12 | 30 | TCP | Normal |
| 5 | ? | TCP | Attack |
| ? | 20 | UDP | Normal |

Burada bazı değerler eksiktir.

Makine öğrenmesi modeline geçmeden önce bu tür problemlerin ele alınması gerekir.

Bu işlemler **veri ön işleme (data preprocessing)** kapsamında ilerleyen haftalarda tekrar ele alınacaktır.

---

# 32. Veri Setinin Kaynağı Güvenilir mi?

Dosyanın adı:

```text
cybersecurity_dataset_final.csv
```

olduğu için veri setinin güvenilir olduğunu varsayamayız.

Mümkünse şu bilgileri kontrol edin:

- Veri setini kim hazırladı?
- Hangi kurum tarafından yayımlandı?
- Nasıl toplandı?
- Ne amaçla oluşturuldu?
- Veri setinin açıklaması var mı?
- Veri setiyle ilişkili akademik çalışma var mı?

Mümkün olduğunda veri setinin **orijinal kaynağına** ulaşmaya çalışın.

---

# 33. Kullanım ve Lisans Koşulları

Bir veri setinin internette bulunması:

> **“İstediğim her şekilde kullanabilirim.”**

anlamına gelmez.

Veri setinin:

- lisansı,
- kullanım şartları,
- atıf gereksinimleri

olabilir.

Özellikle akademik çalışmalarda veri setinin kaynağının doğru şekilde belirtilmesi önemlidir.

---

# 34. Örnek Vaka: Ağ Saldırısı Tespiti

Şimdi bu süreci gerçek bir problem üzerinde düşünelim.

## Problem

> Ağ trafiğinin normal mi yoksa saldırı mı olduğunu belirlemek istiyoruz.

### İhtiyacımız olan veri

Ağ trafiği veya network flow verileri.

### Bekleyebileceğimiz feature'lar

Örneğin:

```text
Flow Duration
Destination Port
Packet Count
Bytes
Protocol
Flag bilgileri
```

### Beklediğimiz label

```text
BENIGN
ATTACK
```

veya farklı saldırı türleri.

---

# 35. Ders Boyunca Kullanacağımız Örnek: CIC-IDS2017

Ders uygulamalarında ağ saldırısı tespiti problemini incelemek için **CIC-IDS2017** veri setinden yararlanacağız.

Burada amacımız yalnızca belirli bir veri setini kullanmayı öğrenmek değildir.

Asıl önemli soru:

> **Bu veri setinin problemimize uygun olduğunu nasıl anlarız?**

Problemimiz:

```text
Ağ saldırısı tespiti
```

Verimiz:

```text
Ağ trafiği / network flow özellikleri
```

Tahmin etmek istediğimiz sonuç:

```text
Normal trafik / Saldırı
```

veya belirli saldırı türleridir.

Dolayısıyla veri setinin içeriği ile çözmek istediğimiz problem arasında anlamlı bir ilişki bulunmaktadır.

Dersin ilerleyen haftalarında aynı veri üzerinden;

- veri analizi,
- veri hazırlama,
- makine öğrenmesi,
- sınıflandırma,
- model değerlendirme,
- anomali tespiti

uygulamaları gerçekleştireceğiz.

---

# 36. Veri Seti Seçim Kontrol Listesi

Kendi projeniz için bir veri seti bulduğunuzda aşağıdaki soruları cevaplayabilmelisiniz:

- [ ] Çözmek istediğim problemi açıkça tanımladım mı?
- [ ] Veri setinin ne hakkında olduğunu biliyor muyum?
- [ ] Bir satırın neyi temsil ettiğini biliyor muyum?
- [ ] Kayıt sayısını biliyor muyum?
- [ ] Feature'ları inceledim mi?
- [ ] Feature sayısını biliyor muyum?
- [ ] Label var mı?
- [ ] Label içerisindeki sınıfları biliyor muyum?
- [ ] Sınıfların dağılımını kontrol ettim mi?
- [ ] Dosya formatını biliyor muyum?
- [ ] Dosya boyutu çalışma ortamım için uygun mu?
- [ ] Eksik değerler hakkında bilgi var mı?
- [ ] Veri setinin orijinal kaynağını buldum mu?
- [ ] Kullanım veya lisans koşullarını kontrol ettim mi?
- [ ] Veri seti gerçekten çözmek istediğim probleme uygun mu?

Bu soruların çoğuna cevap veremiyorsanız veri setini kullanmaya başlamadan önce biraz daha incelemeniz gerekir.

---

# 37. Uygulama – Veri Setini Birlikte İnceleyelim

Bu haftanın uygulamasında henüz bir makine öğrenmesi modeli oluşturmayacağız.

Öncelikle bir veri setinin nasıl bulunduğunu ve değerlendirildiğini göreceğiz.

Uygulamada:

1. Bir siber güvenlik problemi tanımlayacağız.
2. Probleme uygun veri seti arayacağız.
3. Veri setinin orijinal kaynak sayfasını bulacağız.
4. Dataset açıklamasını okuyacağız.
5. Bir satırın neyi temsil ettiğini belirleyeceğiz.
6. Kayıt ve feature sayısını inceleyeceğiz.
7. Label'ı belirleyeceğiz.
8. Sınıfları inceleyeceğiz.
9. Dosya formatını kontrol edeceğiz.
10. Veri setinin problemimize uygun olup olmadığını değerlendireceğiz.
11. Veri dosyasını Google Colab ortamına alacağız.
12. Veri setinin ilk kayıtlarını görüntüleyeceğiz.

Örnek olarak **CIC-IDS2017** veri setini kullanacağız.

---

# 38. Mini Görev – Kendi Veri Setini Bul

Şimdi sıra sizde.

Aşağıdaki siber güvenlik problemlerinden **birini** seçin:

- Phishing URL tespiti
- Spam e-posta tespiti
- Ağ saldırısı tespiti
- Malware tespiti
- Şüpheli kullanıcı davranışı tespiti

İsterseniz başka bir siber güvenlik problemi de seçebilirsiniz.

Henüz model oluşturmayacaksınız.

Amacınız yalnızca **uygun bir veri seti bulmak ve incelemek**.

---

## Bulduğunuz Veri Seti İçin Aşağıdaki Bilgileri Doldurun

**Problem:**

**Veri setinin adı:**

**Veri setinin kaynağı:**

**Veri setinin bağlantısı:**

**Veri setini hazırlayan kurum/kişi:**

**Dosya formatı:**

**Dosya boyutu:**

**Kayıt sayısı:**

**Feature sayısı:**

**Örnek feature'lar:**

**Label:**

**Sınıflar:**

**Sınıfların dağılımı:**

**Bir satır neyi temsil ediyor?:**

**Bu veri setiyle ne tahmin edilebilir?:**

**Neden bu veri setini seçtiniz?:**

**Kullanım/lisans bilgisi:**

---

# 39. Son Soru

Aşağıdaki cümleyi tamamlayın:

> **Bu veri setinin problemim için uygun olduğunu düşünüyorum çünkü...**

Bu soruya vereceğiniz cevap:

> “Çünkü çok fazla verisi var.”

olmamalıdır.

Problem ile veri arasındaki ilişkiyi açıklayabilmelisiniz.

Örneğin:

> “Phishing URL'lerini sınıflandırmak istiyorum. Veri setinde URL özellikleri ve URL'lerin phishing/legitimate etiketleri bulunduğu için problemime uygundur.”

---

# 40. Bu Haftadan Akılda Kalması Gerekenler

**Dataset:** Analiz veya model geliştirmek için kullanılan veri koleksiyonudur.

**Feature:** Modelin karar verirken kullandığı bilgidir.

**Label:** Modelin tahmin etmeye çalıştığı sonuçtur.

**Supervised Learning:** Etiketli verilerden öğrenmedir.

**Unsupervised Learning:** Etiket bulunmadan verideki yapıların araştırılmasıdır.

**Classification:** Bir örneği önceden belirlenmiş sınıflardan birine atamaktır.

**Clustering:** Benzer örnekleri gruplamaktır.

**Anomaly Detection:** Normal davranıştan önemli ölçüde farklı örnekleri belirlemektir.

Bir veri setini kullanmadan önce:

**Problem → Veri Kaynağı → Feature → Label → Sınıflar → Boyut → Kalite → Kullanım Koşulları**

incelenmelidir.

En önemli nokta:

> **Makine öğrenmesi projesinde önce model değil, problem ve veri anlaşılır.**

---

# Sonraki Hafta

## Hafta 03 – Python ile Veri Analizi

Bir sonraki hafta veri setini artık yalnızca gözümüzle incelemek yerine **Python kullanarak analiz etmeye** başlayacağız.

Pandas, NumPy ve Matplotlib ile;

- veri setini Python'a aktarma,
- satır ve sütunları görüntüleme,
- veri tiplerini inceleme,
- temel istatistikleri elde etme,
- eksik değerleri bulma,
- sınıf dağılımını inceleme,
- temel grafikler oluşturma

işlemlerini gerçekleştireceğiz.

Böylece bu hafta **“Doğru veriyi nasıl bulurum ve anlarım?”**, gelecek hafta ise **“Bulduğum veriyi Python ile nasıl analiz ederim?”** sorusuna cevap vereceğiz.
