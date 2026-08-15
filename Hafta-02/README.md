# Hafta 02 – Veri Analizi ve Siber Güvenlik Problem Tipleri

## Dersin Amacı

Bir makine öğrenmesi sisteminin temelinde **veri** bulunur.

Geçen hafta bir güvenlik sisteminin geçmiş verilerdeki örüntülerden yararlanarak yeni olaylar hakkında tahmin yapabileceğini gördük.

Bu hafta şu sorulara cevap arayacağız:

- Veri nedir?
- Veri seti nasıl yapılandırılır?
- Siber güvenlikte hangi tür veriler kullanılır?
- Feature ve label nasıl belirlenir?
- Sınıflandırma, kümeleme ve anomali tespiti arasındaki fark nedir?
- Bir siber güvenlik problemi hangi makine öğrenmesi problemine dönüştürülebilir?

---

# 1. Veri Nedir?

**Veri (data)**, bir olay, nesne, kullanıcı veya sistem hakkında elde edilen bilgilerin işlenebilir biçimde temsil edilmesidir.

Örneğin bir kullanıcı bir sisteme giriş yaptığında şu bilgiler kaydedilebilir:

| Bilgi | Örnek Değer |
|---|---|
| Kullanıcı | user01 |
| Giriş saati | 14:32 |
| IP adresi | 192.168.1.20 |
| Başarısız giriş sayısı | 2 |
| Cihaz | Laptop |
| Konum | Ankara |
| Giriş sonucu | Başarılı |

Tek bir kullanıcı girişi bile birçok farklı veri üretebilir.

Binlerce kullanıcının bulunduğu bir sistemde bu kayıtların sayısı çok hızlı şekilde artar.

---

# 2. Siber Güvenlikte Veri Nereden Gelir?

Siber güvenlik sistemleri çok farklı kaynaklardan veri üretebilir.

### Ağ Trafiği

Ağ üzerinden gerçekleşen iletişim hakkında bilgiler içerir.

Örneğin:

- kaynak IP,
- hedef IP,
- kaynak port,
- hedef port,
- protokol,
- paket sayısı,
- bağlantı süresi,
- gönderilen veri miktarı.

### Sistem Logları

İşletim sistemi veya uygulamalarda gerçekleşen olayların kayıtlarıdır.

Örneğin:

- kullanıcı girişleri,
- başarısız girişler,
- dosya erişimleri,
- sistem hataları,
- yetki değişiklikleri.

### E-posta Verileri

Phishing ve spam tespiti için kullanılabilir.

Örneğin:

- gönderen adresi,
- konu,
- mesaj içeriği,
- bağlantılar,
- ek dosyalar.

### Dosya ve Yazılım Verileri

Malware tespitinde kullanılabilir.

Örneğin:

- dosya boyutu,
- dosya türü,
- sistem çağrıları,
- API kullanımları,
- dosya davranışları.

### Kullanıcı Davranışları

Kullanıcının sistem üzerindeki davranışları analiz edilebilir.

Örneğin:

- giriş zamanı,
- kullanılan cihaz,
- konum,
- erişilen kaynaklar,
- oturum süresi.

---

# 3. Veri Seti Nedir?

Makine öğrenmesinde veriler çoğunlukla **veri seti (dataset)** adı verilen yapılarda tutulur.

Basit bir güvenlik veri seti düşünelim:

| Login_Attempts | Night_Login | New_Device | Country_Changed | Status |
|---:|---:|---:|---:|---|
| 2 | 0 | 0 | 0 | Normal |
| 1 | 0 | 1 | 0 | Normal |
| 18 | 1 | 1 | 1 | Attack |
| 25 | 1 | 1 | 0 | Attack |
| 3 | 0 | 0 | 0 | Normal |

Bu tabloda:

**Her satır → bir gözlem/olay**

**Her sütun → olay hakkında bir bilgi**

olarak düşünülebilir.

Örneğin üçüncü satır bir kullanıcı giriş olayını temsil etmektedir.

---

# 4. Feature Nedir?

Geçen hafta kısaca gördüğümüz **feature (özellik)** kavramını şimdi veri seti üzerinde inceleyelim.

Feature, modelin tahmin yapmak için kullanabileceği bilgidir.

Örneğin:

- `Login_Attempts`
- `Night_Login`
- `New_Device`
- `Country_Changed`

birer feature olabilir.

Bir kullanıcı için:

```text
Login_Attempts = 18
Night_Login = 1
New_Device = 1
Country_Changed = 1
```

değerleri modelin karar verirken kullanabileceği bilgileri oluşturur.

---

# 5. Label Nedir?

**Label (etiket)**, modelin tahmin etmeye çalıştığı sonuçtur.

Örneğimizde:

`Status`

sütunu label'dır.

Değerleri:

```text
Normal
Attack
```

olabilir.

Dolayısıyla:

```text
Login_Attempts ─┐
Night_Login ─────┤
New_Device ──────┼──→ MODEL ──→ Status
Country_Changed ─┘
```

şeklinde düşünebiliriz.

---

# 6. Her Problemde Label Var mıdır?

Hayır.

Bu ayrım bizi makine öğrenmesinin iki temel yaklaşımına götürür.

## Denetimli Öğrenme – Supervised Learning

Eğitim verilerinin sonuçları önceden biliniyorsa **denetimli öğrenme** yaklaşımı kullanılabilir.

Örneğin:

| Trafik | Sonuç |
|---|---|
| Kayıt 1 | Normal |
| Kayıt 2 | Attack |
| Kayıt 3 | Normal |
| Kayıt 4 | Attack |

Model geçmişte hangi kayıtların saldırı olduğunu bilir ve bu örneklerden öğrenmeye çalışır.

```text
Feature + Bilinen Label
          ↓
       Eğitim
          ↓
        Model
```

---

# 7. Denetimsiz Öğrenme – Unsupervised Learning

Bazı durumlarda verilerin hangi sınıfa ait olduğu önceden bilinmez.

Örneğin elimizde 100.000 ağ bağlantısı olabilir fakat bunların:

```text
Normal mi?
Saldırı mı?
```

olduğuna ilişkin etiketler bulunmayabilir.

Bu durumda sistem veriler arasındaki benzerlikleri, grupları veya sıra dışı davranışları bulmaya çalışabilir.

```text
Feature'lar
    ↓
Algoritma
    ↓
Verideki Yapı / Gruplar / Anormallikler
```

Bu yaklaşıma **denetimsiz öğrenme** denir.

---

# 8. Siber Güvenlikte Problem Tipleri

Bu derste özellikle üç problem tipi üzerinde duracağız:

1. Sınıflandırma
2. Kümeleme
3. Anomali tespiti

Bunların birbirinden ayrılması önemlidir.

---

# 9. Sınıflandırma – Classification

**Sınıflandırma**, bir örneğin önceden belirlenmiş sınıflardan hangisine ait olduğunu tahmin etme problemidir.

Örneğin:

```text
Yeni Ağ Trafiği
       ↓
     Model
       ↓
Normal / Saldırı
```

Burada sınıflar önceden bellidir:

- Normal
- Saldırı

### Siber Güvenlik Örnekleri

**Phishing tespiti**

```text
E-posta → Normal / Phishing
```

**Malware tespiti**

```text
Dosya → Benign / Malware
```

**Ağ saldırısı tespiti**

```text
Ağ bağlantısı → Normal / Attack
```

Birden fazla saldırı türü de bulunabilir:

```text
Normal
DoS
Brute Force
Botnet
Web Attack
```

Bu durumda problem yine sınıflandırmadır ancak ikiden fazla sınıf vardır.

---

# 10. İkili ve Çok Sınıflı Sınıflandırma

## Binary Classification

İki sınıf bulunur.

```text
Normal / Attack
```

veya:

```text
Legitimate / Phishing
```

## Multiclass Classification

İkiden fazla sınıf bulunur.

Örneğin:

```text
Normal
DoS
Brute Force
Botnet
Web Attack
```

Model gelen verinin bu sınıflardan hangisine ait olduğunu tahmin etmeye çalışır.

---

# 11. Kümeleme – Clustering

Şimdi farklı bir problem düşünelim.

Elimizde binlerce ağ bağlantısı var ancak hangi bağlantının hangi tür davranış olduğunu bilmiyoruz.

Yani **label yok**.

Algoritmadan benzer davranışları bir araya getirmesini isteyebiliriz.

Örneğin:

```text
              Ağ Trafiği
                  ↓
              Kümeleme
             ↙    ↓    ↘
         Küme 1 Küme 2 Küme 3
```

Algoritma:

> “Bunlar saldırıdır.”

demek zorunda değildir.

Yalnızca birbirine benzeyen kayıtları gruplamaya çalışır.

Sonrasında bir güvenlik uzmanı kümeleri inceleyebilir.

Örneğin:

```text
Küme 1 → Normal kullanıcı davranışları

Küme 2 → Yoğun veri transferi yapan kullanıcılar

Küme 3 → Şüpheli davranış gösteren kullanıcılar
```

Bu yorumları algoritma değil, daha sonra yapılan analiz ortaya çıkarabilir.

---

# 12. Sınıflandırma ile Kümeleme Arasındaki Temel Fark

### Sınıflandırma

Sınıflar önceden bellidir.

```text
Normal
Attack
```

Model yeni veriyi bu sınıflardan birine atar.

### Kümeleme

Sınıflar önceden belli değildir.

Algoritma benzer verileri gruplar.

| Sınıflandırma | Kümeleme |
|---|---|
| Genellikle label vardır | Label yoktur |
| Sınıflar önceden bellidir | Gruplar veriden ortaya çıkar |
| Tahmin yapılır | Benzer kayıtlar gruplanır |
| Denetimli öğrenme | Denetimsiz öğrenme |

---

# 13. Anomali Tespiti – Anomaly Detection

**Anomali**, genel davranıştan önemli ölçüde farklı olan gözlem veya davranıştır.

Örneğin bir kullanıcının normal davranışı:

```text
Giriş saati: 08.00–18.00
Konum: Ankara
Cihaz: Kendi bilgisayarı
Günlük giriş: 2–4
```

olsun.

Bir gün:

```text
Saat: 03.42
Konum: Farklı ülke
Cihaz: Bilinmeyen cihaz
Giriş denemesi: 48
```

kaydı oluşuyor.

Bu davranış normal profilden oldukça farklıdır.

```text
Normal davranışlar: ● ● ● ● ● ● ● ●

Anormal davranış:                    X
```

`X` noktası bir **anomali** olarak değerlendirilebilir.

---

# 14. Anomali Her Zaman Saldırı mıdır?

**Hayır.**

Bu ayrım siber güvenlik açısından çok önemlidir.

Bir davranış sıra dışı olabilir fakat kötü amaçlı olmayabilir.

Örneğin bir çalışan:

- yurt dışına seyahat etmiş olabilir,
- yeni bilgisayar kullanıyor olabilir,
- gece çalışıyor olabilir.

Dolayısıyla:

> **Anormal ≠ Kesin saldırı**

Anomali tespit sistemi çoğunlukla:

> “Bu davranış alışılmış davranıştan farklı, incelenmesi gerekebilir.”

şeklinde düşünülmelidir.

---

# 15. Sınıflandırma mı, Anomali Tespiti mi?

Elimizde geçmiş saldırı örnekleri ve bunların etiketleri varsa:

```text
Normal / Attack
```

bir **sınıflandırma problemi** oluşturabiliriz.

Ancak yeni veya daha önce görülmemiş saldırı davranışlarını arıyorsak, normal davranıştan sapmaları belirlemek için **anomali tespiti** yararlı olabilir.

Bu nedenle problem türünü seçerken elimizdeki verinin yapısını ve çözmek istediğimiz güvenlik problemini anlamamız gerekir.

---

# 16. Üç Problem Tipini Karşılaştıralım

| Problem | Amaç | Label | Siber Güvenlik Örneği |
|---|---|---|---|
| **Sınıflandırma** | Veriyi bilinen sınıfa atamak | Genellikle var | Normal / Attack |
| **Kümeleme** | Benzer verileri gruplamak | Yok | Benzer ağ davranışlarını gruplama |
| **Anomali Tespiti** | Sıra dışı davranışı bulmak | Her zaman gerekli değil | Şüpheli kullanıcı davranışı |

---

# 17. Hangi Problem Tipi?

### Senaryo 1

10.000 e-postamız var.

Her e-posta daha önce:

```text
Normal
Phishing
```

olarak etiketlenmiş.

Yeni e-postaların phishing olup olmadığını belirlemek istiyoruz.

**Problem:** Sınıflandırma

---

### Senaryo 2

Elimizde binlerce kullanıcı davranışı var.

Herhangi bir etiket bulunmuyor.

Benzer davranış gösteren kullanıcıları gruplamak istiyoruz.

**Problem:** Kümeleme

---

### Senaryo 3

Bir şirket çalışanlarının normal giriş davranışlarını biliyor.

Normal davranıştan ciddi şekilde farklı yeni girişleri belirlemek istiyor.

**Problem:** Anomali Tespiti

---

# 18. Problem Tipini Belirlemek Neden Önemlidir?

Bir makine öğrenmesi projesine:

> “Hangi algoritmayı kullanalım?”

sorusuyla başlamak doğru değildir.

Önce:

> **“Hangi problemi çözmeye çalışıyoruz?”**

sorusunu cevaplamamız gerekir.

Genel yaklaşım:

```text
Gerçek Dünya Problemi
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

> “Phishing e-postaları tespit etmek istiyorum.”

dedikten sonra elimizde etiketli e-postalar varsa bunu bir **sınıflandırma problemine** dönüştürebiliriz.

---

# 19. Siber Güvenlik Verisinin Kalitesi

Çok fazla veriye sahip olmak tek başına yeterli değildir.

Veride;

- eksik değerler,
- yanlış kayıtlar,
- tekrar eden kayıtlar,
- hatalı etiketler,
- dengesiz sınıflar

bulunabilir.

Örneğin:

```text
99.000 Normal
1.000 Attack
```

kaydımız olduğunu düşünelim.

Bu durumda veri setindeki kayıtların %99'u normaldir.

Model:

> “Her şeye Normal de.”

şeklinde davranırsa bile sonuçların büyük bölümünü doğru tahmin etmiş gibi görünebilir.

Bu nedenle yalnızca veri miktarına değil, **verinin yapısına ve kalitesine** de dikkat etmek gerekir.

Bu konuları ilerleyen haftalarda ayrıntılı olarak inceleyeceğiz.

---

# 20. Düşünelim

### Soru 1

Elimizde etiketlenmiş 50.000 ağ bağlantısı var:

- Normal
- DoS
- Brute Force
- Botnet

Yeni bir bağlantının hangi sınıfa ait olduğunu tahmin etmek istiyoruz.

**Hangi problem tipi?**

**Cevap:** Çok sınıflı sınıflandırma.

---

### Soru 2

Elimizde etiketlenmemiş kullanıcı davranışları var ve benzer kullanıcıları gruplamak istiyoruz.

**Hangi problem tipi?**

**Cevap:** Kümeleme.

---

### Soru 3

Normal ağ davranışından çok farklı olan bağlantıları bulmak istiyoruz.

**Hangi problem tipi?**

**Cevap:** Anomali tespiti.

---

### Soru 4

Bir kullanıcının gece sisteme girmesi anomali olarak tespit edildi.

Bu kullanıcının kesinlikle saldırgan olduğunu söyleyebilir miyiz?

**Cevap:** Hayır. Anomali, davranışın alışılmış örneklerden farklı olduğunu gösterir; tek başına saldırı olduğunu kanıtlamaz.

---

# Bu Haftadan Akılda Kalması Gerekenler

**Dataset:** Analiz veya model geliştirmek için kullanılan veri koleksiyonudur.

**Feature:** Modelin karar verirken kullandığı bilgidir.

**Label:** Modelin tahmin etmeye çalıştığı sonuçtur.

**Supervised Learning:** Etiketli verilerden öğrenmedir.

**Unsupervised Learning:** Etiket bulunmadan verideki yapıların araştırılmasıdır.

**Classification:** Bir örneği önceden belirlenmiş sınıflardan birine atamaktır.

**Clustering:** Benzer örnekleri gruplamaktır.

**Anomaly Detection:** Normal davranıştan önemli ölçüde farklı örnekleri belirlemektir.

---

# Hafta 02 Uygulaması

Bu haftanın uygulamasında gerçek bir siber güvenlik veri setini inceleyeceğiz.

Henüz makine öğrenmesi modeli oluşturmayacağız.

Amacımız:

1. Veri setini açmak,
2. Satır ve sütunları incelemek,
3. Feature'ları belirlemek,
4. Label'ı belirlemek,
5. Veri türlerini incelemek,
6. Sınıfları görmek,
7. Bu veriyle hangi makine öğrenmesi problemlerinin çözülebileceğini tartışmak.

---

# Sonraki Hafta

## Hafta 03 – Python ile Veri Analizi

Bir sonraki hafta aynı veri seti üzerinde **Pandas, NumPy ve Matplotlib** kullanarak veriyi Python ile analiz etmeye başlayacağız.
