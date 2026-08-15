# Hafta 01 – Yapay Zekâ, Makine Öğrenmesi, Derin Öğrenme ve Siber Güvenlik

## Dersin Amacı

Bu hafta yapay zekânın ne olduğunu, makine öğrenmesi ve derin öğrenmenin yapay zekâ içerisindeki yerini ve bu teknolojilerin siber güvenlik problemlerinde neden kullanıldığını öğreneceğiz.

Bu haftanın temel sorusu şudur:

> **Bir bilgisayar, daha önce hiç görmediği bir siber tehdidi nasıl fark edebilir?**

Bu soruya cevap verebilmek için önce **Yapay Zekâ (AI)**, **Makine Öğrenmesi (ML)** ve **Derin Öğrenme (DL)** kavramlarını birbirinden ayırmamız gerekir.

---

# 1. Yapay Zekâ Nedir?

**Yapay Zekâ (Artificial Intelligence – AI)**, bilgisayar sistemlerinin normalde insan zekâsıyla ilişkilendirilen bazı görevleri gerçekleştirebilmesini amaçlayan geniş bir çalışma alanıdır.

Bu görevler arasında;

- karar verme,
- problem çözme,
- örüntüleri tanıma,
- tahmin yapma,
- doğal dili anlama,
- görüntüleri analiz etme

gibi işlemler bulunabilir.

Burada önemli bir nokta vardır:

**Her yapay zekâ sistemi makine öğrenmesi kullanmak zorunda değildir.**

Bunu bir örnek üzerinden inceleyelim.

---

# 2. Kural Tabanlı Bir Sistem ile Başlayalım

Bir kurumun bilgi sisteminde şu güvenlik kuralının bulunduğunu düşünelim:

```text
EĞER
bir kullanıcı 1 dakika içerisinde 10 kez yanlış parola girerse

O ZAMAN
hesabı geçici olarak kilitle.
```

Bu sistem bir güvenlik kararı vermektedir.

Ancak sistemin davranışı tamamen bir insan tarafından önceden belirlenmiştir.

Bilgisayarın yaptığı şey:

```text
10'dan fazla başarısız giriş var mı?
            ↓
        EVET / HAYIR
            ↓
       Hesabı kilitle
```

Sistem geçmiş saldırılara bakarak herhangi bir şey **öğrenmemiştir**.

Bu nedenle buna **kural tabanlı (rule-based)** bir yaklaşım diyebiliriz.

---

# 3. Kural Tabanlı Sistemlerin Problemi Nedir?

Şimdi saldırganın davranışını değiştirdiğini düşünelim.

Saldırgan artık aynı hesaba 10 kez giriş yapmak yerine:

- farklı kullanıcı hesaplarını deniyor,
- farklı IP adresleri kullanıyor,
- giriş denemelerini zamana yayıyor,
- normal kullanıcı davranışına benzemeye çalışıyor.

Artık yazdığımız basit kural saldırıyı yakalayamayabilir.

Yeni kurallar ekleyebiliriz:

```text
EĞER başarısız giriş > 10 → Uyarı
```

```text
EĞER farklı IP sayısı > 5 → Uyarı
```

```text
EĞER gece giriş yapılmışsa → Kontrol et
```

Ancak gerçek sistemlerde binlerce veya milyonlarca olay gerçekleşebilir.

Bütün olası saldırı davranışlarını tek tek kurallarla tanımlamak giderek zorlaşır.

İşte **makine öğrenmesinin** devreye girdiği noktalardan biri burasıdır.

---

# 4. Makine Öğrenmesi Nedir?

**Makine Öğrenmesi (Machine Learning – ML)**, bilgisayar sistemlerinin verilerde bulunan örüntülerden yararlanarak tahmin veya karar üretmesini sağlayan yapay zekâ alanıdır.

Klasik programlamada genel yaklaşım şöyledir:

```text
VERİ + KURALLAR
       ↓
   PROGRAM
       ↓
    SONUÇ
```

Makine öğrenmesinde ise geçmiş veriler kullanılarak bir **model** oluşturulur:

```text
GEÇMİŞ VERİLER
       ↓
ÖĞRENME ALGORİTMASI
       ↓
      MODEL
       ↓
    YENİ VERİ
       ↓
     TAHMİN
```

Buradaki en önemli kavram **modeldir**.

---

# 5. Model Nedir?

Bir makine öğrenmesi **modeli**, eğitim verilerinde bulunan ilişkileri öğrenerek daha önce görmediği veriler hakkında tahmin yapmaya çalışan yapıdır.

Örneğin elimizde geçmiş ağ bağlantıları olsun.

| Bağlantı | Süre | Veri Miktarı | Başarısız Giriş | Sonuç |
|---       |---:  |---:          |---:|.---|
| A        | 5 sn | 2 MB | 0 | Normal |
| B        | 2 sn | 1 MB | 0 | Normal |
| C        | 1 sn | 30 MB | 15 | Saldırı |
| D        | 3 sn | 25 MB | 12 | Saldırı |

Model bu örnekleri inceleyerek **normal trafik ile saldırı trafiği arasındaki ilişkileri** öğrenmeye çalışır.

Daha sonra yeni bir bağlantı geldiğinde:

```text
Yeni bağlantı
Süre: 2 sn
Veri: 28 MB
Başarısız giriş: 14
```

model:

```text
SALDIRI
```

şeklinde bir tahmin üretebilir.

Burada karar:

> “Başarısız giriş 10'dan fazlaysa kesin saldırıdır.”

şeklinde bizim yazdığımız tek bir kurala dayanmak zorunda değildir.

Model veriler arasındaki ilişkileri kullanır.

---

# 6. Veri Makine Öğrenmesi İçin Neden Önemlidir?

Makine öğrenmesinin merkezinde **veri** vardır.

Bir modelin öğrenebilmesi için geçmiş örneklere ihtiyacı vardır.

Siber güvenlik açısından veri;

- ağ trafiği kayıtları,
- giriş kayıtları (login logs),
- e-postalar,
- URL adresleri,
- sistem logları,
- dosya özellikleri,
- kullanıcı davranışları

gibi birçok kaynaktan gelebilir.

Bu nedenle şu ifadeyi akılda tutmak önemlidir:

> **Makine öğrenmesi modeli, kendisine verilen veriden öğrenir.**

Veri yetersiz veya hatalıysa modelin ürettiği sonuçlar da güvenilir olmayabilir.

Bu konu ilerleyen haftalarda ayrıntılı olarak ele alınacaktır.

---

# 7. Feature ve Label Kavramlarına İlk Bakış

Makine öğrenmesinde sık kullanacağımız iki kavram vardır.

## Feature (Özellik)

Modelin karar verirken kullandığı bilgiler **feature** olarak adlandırılır.

Örneğin bir ağ bağlantısında:

```text
Bağlantı süresi
Paket sayısı
Gönderilen veri miktarı
Kaynak port
Hedef port
Başarısız giriş sayısı
```

birer feature olabilir.

## Label (Etiket)

Modelin tahmin etmeye çalıştığı sonuç ise **label** olarak düşünülebilir.

Örneğin:

```text
0 → Normal
1 → Saldırı
```

Dolayısıyla basitleştirilmiş bir güvenlik verimiz şöyle olabilir:

| Süre | Paket | Veri Miktarı | Başarısız Giriş | Etiket |
|---:|---:|---:|---:|---|
| 5 | 12 | 2 MB | 0 | Normal |
| 3 | 10 | 1 MB | 0 | Normal |
| 1 | 300 | 35 MB | 18 | Saldırı |

Model;

```text
FEATURE'LAR
     ↓
    MODEL
     ↓
   LABEL
```

ilişkisini öğrenmeye çalışır.

Feature ve label kavramlarını ilerleyen haftalarda Python üzerinde uygulamalı olarak kullanacağız.

---

# 8. Makine Öğrenmesinde Eğitim Mantığı

Bir öğrencinin geçmiş soruları çözerek sınava hazırlanmasını düşünelim.

Öğrenci:

1. örnekleri görür,
2. örnekler arasındaki ilişkileri öğrenir,
3. daha önce görmediği bir soruyla karşılaşır,
4. öğrendiklerini kullanarak cevap verir.

Makine öğrenmesinde de benzer bir mantık vardır.

```text
Geçmiş Veriler
      ↓
    Eğitim
      ↓
     Model
      ↓
Daha Önce Görülmemiş Veri
      ↓
    Tahmin
```

Burada dikkat edilmesi gereken nokta:

**Modelin amacı eğitim verisini ezberlemek değil, yeni veriler üzerinde doğru tahmin yapabilmektir.**

Bu kavram ilerleyen haftalarda **overfitting** konusu altında tekrar ele alınacaktır.

---

# 9. Yapay Zekâ – Makine Öğrenmesi – Derin Öğrenme İlişkisi

Bu üç kavram sıklıkla birbirinin yerine kullanılmaktadır ancak aynı şeyi ifade etmez.

İlişkileri şöyle gösterilebilir:

```text
YAPAY ZEKÂ (AI)
│
│  En geniş alan
│
└── MAKİNE ÖĞRENMESİ (ML)
    │
    │  Verilerden öğrenme
    │
    └── DERİN ÖĞRENME (DL)
        │
        └── Çok katmanlı yapay sinir ağları
```

Yani:

**Her derin öğrenme yöntemi → makine öğrenmesidir.**

**Her makine öğrenmesi yöntemi → yapay zekâ kapsamındadır.**

Ancak:

**Her yapay zekâ sistemi → derin öğrenme değildir.**

---

# 10. Derin Öğrenme Nedir?

**Derin Öğrenme (Deep Learning – DL)**, çok katmanlı yapay sinir ağlarını kullanan makine öğrenmesi yaklaşımıdır.

Özellikle büyük ve karmaşık verilerde güçlü sonuçlar verebilir.

Örneğin:

- görüntüler,
- ses kayıtları,
- doğal dil,
- karmaşık ağ trafiği,
- zararlı yazılım davranışları

üzerinde kullanılabilir.

---

# 11. ML ile DL Arasındaki Farkı Bir Örnekle Düşünelim

Bir dosyanın zararlı yazılım olup olmadığını belirlemek istediğimizi düşünelim.

## Geleneksel Makine Öğrenmesi Yaklaşımı

Öncelikle dosyadan bazı özellikler çıkarabiliriz:

```text
Dosya boyutu
Kullandığı API sayısı
Şüpheli sistem çağrıları
Dosya türü
Ağ bağlantısı sayısı
```

Bu özellikleri bir makine öğrenmesi modeline veririz:

```text
Özellikler
    ↓
ML Modeli
    ↓
Normal / Malware
```

## Derin Öğrenme Yaklaşımı

Derin öğrenme sistemleri bazı problemlerde daha ham veya yüksek boyutlu verilerden karmaşık özellikleri kendileri öğrenebilir.

```text
Ham / Karmaşık Veri
        ↓
Derin Sinir Ağı
        ↓
Özelliklerin Öğrenilmesi
        ↓
Normal / Malware
```

Bu nedenle derin öğrenme özellikle büyük ve karmaşık veri setlerinde tercih edilebilir.

Ancak bu:

> **“Derin öğrenme her zaman daha iyidir.”**

anlamına gelmez.

Probleme, veri miktarına, hesaplama kaynaklarına ve açıklanabilirlik ihtiyacına göre daha basit bir makine öğrenmesi modeli daha uygun olabilir.

---

# 12. Siber Güvenlik Nedir?

Siber güvenlik; bilgisayarların, ağların, sistemlerin, uygulamaların ve verilerin dijital tehditlere karşı korunmasını kapsar.

Temel amaçlardan bazıları:

- yetkisiz erişimi engellemek,
- verilerin değiştirilmesini önlemek,
- sistemlerin kullanılabilirliğini korumak,
- saldırıları tespit etmek,
- saldırılara hızlı şekilde müdahale etmektir.

---

# 13. Siber Güvenlikte Karşılaşabileceğimiz Tehditler

## Phishing

Kullanıcıyı kandırarak parola, kredi kartı veya kişisel bilgi elde etmeye yönelik saldırılardır.

Örneğin:

> “Hesabınız askıya alınmıştır. Hesabınızı doğrulamak için bağlantıya tıklayın.”

Bir ML sistemi e-postanın;

- kullandığı kelimeleri,
- bağlantıları,
- gönderen bilgilerini,
- URL özelliklerini

inceleyerek phishing olup olmadığını tahmin edebilir.

---

## Malware

Bilgisayar sistemlerine zarar vermek veya yetkisiz işlemler gerçekleştirmek amacıyla oluşturulan kötü amaçlı yazılımlardır.

Bir yapay zekâ sistemi dosyaların davranışlarını inceleyerek zararlı yazılımları tespit etmeye yardımcı olabilir.

---

## Ağ Saldırıları

Saldırganlar ağ üzerindeki sistemlere erişmeye, hizmetleri engellemeye veya bilgi elde etmeye çalışabilir.

Makine öğrenmesi modelleri ağ trafiğini analiz ederek:

```text
NORMAL TRAFİK
```

ile

```text
SALDIRI TRAFİĞİ
```

arasındaki farkları öğrenebilir.

---

# 14. Yapay Zekâ Siber Güvenlikte Nerelerde Kullanılır?

Yapay zekâ ve makine öğrenmesinin siber güvenlikte kullanım alanlarından bazıları şunlardır:

### 1. Phishing Tespiti

Şüpheli e-posta ve web sitelerinin belirlenmesi.

### 2. Intrusion Detection

Ağ üzerinde saldırı niteliği taşıyan aktivitelerin tespit edilmesi.

### 3. Malware Detection

Dosya veya program davranışlarının analiz edilerek zararlı yazılımların belirlenmesi.

### 4. Anomali Tespiti

Normal davranıştan önemli ölçüde farklı aktivitelerin belirlenmesi.

### 5. Kullanıcı Davranışı Analizi

Bir kullanıcının normal davranışının dışına çıkmasının tespit edilmesi.

---

# 15. Örnek Senaryo: Şüpheli Kullanıcı Girişi

Bir kullanıcının normal davranışı şöyle olsun:

```text
Giriş saati: 08.00 – 18.00
Konum: Türkiye
Günlük giriş sayısı: 2–5
Cihaz: Kişisel bilgisayar
```

Bir gün sistem şunu görüyor:

```text
Saat: 03.17
Konum: Farklı ülke
Giriş denemesi: 47
Cihaz: Daha önce görülmemiş
```

Tek tek bakıldığında bu özelliklerin her biri kesin olarak saldırı anlamına gelmeyebilir.

Ancak hepsi birlikte değerlendirildiğinde davranış oldukça sıra dışıdır.

Bir makine öğrenmesi sistemi bu tür ilişkileri kullanarak:

```text
Normal davranış
       ↓
   karşılaştır
       ↓
Yeni davranış
       ↓
ANORMAL DAVRANIŞ
```

şeklinde bir sonuç üretebilir.

Bu yaklaşım ilerleyen haftalarda işleyeceğimiz **anomali tespitinin** temel fikridir.

---

# 16. Yapay Zekâ Her Sorunu Çözer mi?

Hayır.

Yapay zekâ güçlü bir araçtır ancak hatasız değildir.

Örneğin bir saldırı tespit sistemi:

### False Positive

Normal bir davranışı saldırı olarak işaretleyebilir.

```text
Gerçek: Normal
Model: Saldırı
```

### False Negative

Gerçek bir saldırıyı normal olarak değerlendirebilir.

```text
Gerçek: Saldırı
Model: Normal
```

Siber güvenlikte özellikle **false negative** ciddi sonuçlara yol açabilir çünkü gerçek bir saldırı gözden kaçabilir.

Bu nedenle ilerleyen haftalarda yalnızca:

> “Model doğru tahmin yaptı mı?”

sorusunu sormayacağız.

Aynı zamanda:

> “Hangi hataları yaptı?”

sorusunu da inceleyeceğiz.

---

# 17. Dönem Boyunca Kuracağımız Sistem

Dersin ilerleyen haftalarında temel olarak aşağıdaki süreci öğreneceğiz:

```text
SİBER GÜVENLİK PROBLEMİ
          ↓
       VERİ SETİ
          ↓
      VERİ ANALİZİ
          ↓
     VERİ ÖN İŞLEME
          ↓
        MODEL
          ↓
       EĞİTİM
          ↓
       TAHMİN
          ↓
   MODEL DEĞERLENDİRME
          ↓
GÜVENLİK AÇISINDAN YORUMLAMA
```

Dönemin ikinci yarısında bu süreci kendi siber güvenlik projenizde uygulayacaksınız.

---

# 18. Düşünelim

### Soru 1

Bir banka aşağıdaki kuralı kullanıyor:

> “Bir kullanıcı parolasını 5 kez yanlış girerse hesabı kilitle.”

Bu sistem makine öğrenmesi kullanıyor mudur?

**Cevap:** Hayır. Çünkü davranış önceden insan tarafından tanımlanmış bir kurala dayanmaktadır.

---

### Soru 2

Bir sistem geçmişte gerçekleşen 100.000 ağ bağlantısını analiz ederek saldırı davranışlarını öğreniyor ve yeni bağlantıları “Normal” veya “Saldırı” olarak sınıflandırıyor.

Bu sistem makine öğrenmesi kullanıyor mudur?

**Cevap:** Evet. Sistem geçmiş verilerden öğrenerek yeni veriler üzerinde tahmin üretmektedir.

---

### Soru 3

Bir model eğitim verisindeki bütün örnekleri doğru tahmin ediyor ancak yeni verilerde çok fazla hata yapıyor.

Model gerçekten iyi öğrenmiş midir?

**Cevap:** Büyük olasılıkla hayır. Model veriyi öğrenmek yerine fazla ezberlemiş olabilir. Bu problemi ilerleyen haftalarda **overfitting** olarak inceleyeceğiz.

---

# 19. Hafta 01 Uygulaması

Bu haftanın uygulamasında henüz makine öğrenmesi modeli oluşturmayacağız.

Öncelikle dönem boyunca kullanacağımız çalışma ortamını tanıyacağız.

## Kullanacağımız Araçlar

- GitHub
- Google Colab
- Python

## Uygulama Adımları

1. Ders GitHub repository'sini inceleme
2. Hafta klasörlerinin yapısını öğrenme
3. Google Colab ortamını açma
4. Notebook ve hücre kavramlarını öğrenme
5. İlk Python kodunu çalıştırma
6. Kod ve çıktı hücrelerini inceleme
7. Notebook'u kaydetme

Örneğin ilk Python kodumuz:

```python
print("Yapay Zekâ ve Siber Güvenlik")
```

Ardından küçük bir güvenlik senaryosu:

```python
basarisiz_giris = 12

if basarisiz_giris > 10:
    print("Şüpheli giriş tespit edildi!")
else:
    print("Normal giriş")
```

Bu örnek henüz **makine öğrenmesi değildir**.

Neden?

Çünkü:

```python
basarisiz_giris > 10
```

kuralını bilgisayar öğrenmedi.

**Biz yazdık.**

İlerleyen haftalarda aynı tür bir kararı, kuralları bizim tek tek yazmamız yerine **veriden öğrenen makine öğrenmesi modellerine** verdireceğiz.

---

# Bu Haftadan Akılda Kalması Gerekenler

**AI** → En geniş kavramdır.

**ML** → Verilerden örüntüler öğrenerek tahmin üretmeye odaklanır.

**DL** → Çok katmanlı yapay sinir ağlarına dayanan ML yaklaşımıdır.

**Feature** → Modelin karar verirken kullandığı bilgidir.

**Label** → Modelin tahmin etmeye çalıştığı sonuçtur.

**Model** → Geçmiş verilerden öğrenilen ilişkileri kullanarak yeni veriler üzerinde tahmin üretir.

**Siber güvenlik + ML** → Büyük miktardaki güvenlik verisinden saldırı, anomali ve şüpheli davranışları belirlemeye yardımcı olabilir.

---

# Sonraki Hafta

## Hafta 02 – Veri Analizi ve Siber Güvenlik Problem Tipleri

Bir sonraki hafta;

- veri seti nedir,
- satır ve sütun neyi temsil eder,
- feature ve label nasıl belirlenir,
- sınıflandırma nedir,
- kümeleme nedir,
- anomali tespiti nedir

konularını gerçek bir siber güvenlik veri seti üzerinden inceleyeceğiz.
