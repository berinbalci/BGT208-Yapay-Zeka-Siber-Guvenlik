# BGT208 – Yapay Zekâ ve Siber Güvenlik

## Hafta 4 – Makine Öğrenmesinin Temelleri

## Dersin Amacı

Bu haftanın amacı, **makine öğrenmesinin temel çalışma mantığını** kavramak ve bir veri setinin makine öğrenmesi sürecinde nasıl kullanıldığını öğrenmektir.

Önceki hafta Python ve Pandas kullanılarak veri setinin yapısı incelenmiş, temel keşifsel veri analizi işlemleri gerçekleştirilmiştir.

Bu hafta ise şu sorular üzerinde durulacaktır:

- Makine öğrenmesi nedir?
- Bir makine öğrenmesi modeli nasıl öğrenir?
- Özellik (feature) ve hedef (target/label) nedir?
- Eğitim ve test verisi neden ayrılır?
- Bir model nasıl eğitilir?
- Eğitilen model yeni veriler üzerinde nasıl tahmin yapar?

---

# 1. Makine Öğrenmesi Nedir?

**Makine Öğrenmesi (Machine Learning – ML)**, bilgisayar sistemlerinin verilerden örüntüler öğrenmesini ve öğrendiği örüntüleri kullanarak yeni veriler üzerinde tahmin veya karar üretmesini sağlayan yapay zekâ alanıdır.

Geleneksel programlamada bir problemi çözmek için kurallar programcı tarafından açık şekilde tanımlanır.

Basitleştirilmiş olarak:

```text
Geleneksel Programlama

Veri + Kurallar → Sonuç
```

Makine öğrenmesinde ise sistem, örnek verileri kullanarak kuralları veya örüntüleri öğrenmeye çalışır.

```text
Makine Öğrenmesi

Veri + Beklenen Sonuçlar → Öğrenme → Model
                                  ↓
                              Yeni Veri
                                  ↓
                                Tahmin
```

Örneğin phishing tespitinde bütün zararlı URL'leri tek tek kurallarla tanımlamak yerine, daha önce bilinen phishing ve güvenilir URL örneklerinden yararlanılarak bir makine öğrenmesi modeli geliştirilebilir.

---

# 2. Makine Öğrenmesinin Temel Türleri

Makine öğrenmesi yöntemleri farklı öğrenme biçimlerine göre gruplandırılabilir.

## Denetimli Öğrenme (Supervised Learning)

Denetimli öğrenmede veri setinde hem **girdi özellikleri** hem de doğru sonuçları gösteren **etiketler** bulunur.

Örneğin:

| URL_Length | NoOfDots | NoOfLetters | label |
|---:|---:|---:|---:|
| 54 | 2 | 38 | 1 |
| 126 | 5 | 74 | 0 |
| 43 | 1 | 31 | 1 |

Burada URL ile ilgili özellikler modelin girdilerini, `label` ise doğru sonucu temsil eder.

Denetimli öğrenmenin iki temel problem türü vardır:

- **Sınıflandırma (Classification):** Bir örneğin hangi sınıfa ait olduğunu tahmin etmek.
- **Regresyon (Regression):** Sayısal bir değeri tahmin etmek.

Siber güvenlikte sınıflandırma örnekleri:

- Phishing / güvenilir web sitesi
- Spam / normal e-posta
- Zararlı / güvenilir dosya
- Saldırı / normal ağ trafiği

---

## Denetimsiz Öğrenme (Unsupervised Learning)

Denetimsiz öğrenmede verilerin doğru sınıflarını gösteren etiketler bulunmaz.

Algoritma, veriler arasındaki benzerlikleri ve örüntüleri kendisi keşfetmeye çalışır.

Siber güvenlikte örnek kullanım alanları:

- Benzer ağ davranışlarının gruplanması
- Olağandışı sistem davranışlarının belirlenmesi
- Anomali tespiti

Denetimsiz öğrenme yöntemleri ilerleyen haftalarda ayrıca ele alınacaktır.

---

# 3. Özellik (Feature) ve Hedef (Target)

Denetimli makine öğrenmesinde veri seti genel olarak iki temel bölüme ayrılır:

- **X → Özellikler (Features)**
- **y → Hedef değişken (Target / Label)**

## Özellik (Feature)

Modelin tahmin yapmak için kullandığı bilgilerdir.

PhiUSIIL phishing veri setinde URL'nin uzunluğu, karakter yapısı veya web sayfasıyla ilgili çeşitli bilgiler özellik olarak kullanılabilir.

## Hedef (Target / Label)

Modelin tahmin etmeye çalıştığı değişkendir.

Örneğin:

```text
X = URL ile ilgili özellikler
y = phishing / legitimate
```

Python'da bu ayrım genel olarak şu şekilde yapılabilir:

```python
X = df.drop("label", axis=1)
y = df["label"]
```

Burada:

- `X` modelin kullanacağı özellikleri,
- `y` modelin tahmin etmeye çalışacağı hedef değişkeni

temsil eder.

---

# 4. Model Nedir?

Bir **makine öğrenmesi modeli**, eğitim verilerindeki ilişkileri ve örüntüleri öğrenen matematiksel yapıdır.

Modelin amacı yalnızca daha önce gördüğü örnekleri hatırlamak değildir.

Asıl amaç, öğrendiği örüntüleri kullanarak **daha önce görmediği yeni veriler üzerinde doğru tahminler yapabilmektir.**

Örneğin bir phishing tespit modeli:

```text
URL özellikleri
      ↓
Makine Öğrenmesi Modeli
      ↓
Phishing / Legitimate
```

şeklinde düşünülebilir.

---

# 5. Modelin Eğitilmesi

Bir makine öğrenmesi modelinin verilerden örüntüleri öğrenmesi sürecine **eğitim (training)** adı verilir.

Scikit-learn kütüphanesinde birçok makine öğrenmesi modeli benzer kullanım yapısına sahiptir.

Genel olarak:

```python
model.fit(X_train, y_train)
```

komutu modelin eğitim verileri üzerinde öğrenmesini sağlar.

Burada:

- `X_train` → eğitim için kullanılan özellikler
- `y_train` → bu örneklerin doğru sınıfları

anlamına gelir.

---

# 6. Eğitim ve Test Verisi

Bir makine öğrenmesi modelinin yalnızca eğitim sırasında gördüğü veriler üzerindeki başarısına bakmak yeterli değildir.

Modelin **daha önce görmediği veriler üzerinde** nasıl çalıştığını da değerlendirmek gerekir.

Bu nedenle veri seti genellikle iki bölüme ayrılır:

```text
Tüm Veri Seti
      |
      |-------------------|
      |                   |
 Eğitim Verisi         Test Verisi
      |                   |
 Model öğrenir       Model değerlendirilir
```

Örneğin veri setinin:

- `%80` → eğitim
- `%20` → test

için ayrılması mümkündür.

Bu oran her problem için zorunlu bir kural değildir ancak sık kullanılan yaklaşımlardan biridir.

---

# 7. Train-Test Split

Scikit-learn kütüphanesindeki `train_test_split()` fonksiyonu veri setini eğitim ve test bölümlerine ayırmak için kullanılabilir.

```python
from sklearn.model_selection import train_test_split
```

Örnek kullanım:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42
)
```

Burada:

- `X_train` → eğitim özellikleri
- `X_test` → test özellikleri
- `y_train` → eğitim etiketleri
- `y_test` → test etiketleri
- `test_size=0.20` → verinin %20'sinin test için ayrılması
- `random_state=42` → veri bölme işleminin tekrar edilebilir olmasını sağlar

---

# 8. Neden Verinin Tamamıyla Eğitim Yapmıyoruz?

Eğer bütün veri modelin eğitiminde kullanılırsa modeli değerlendirmek için bağımsız veri kalmaz.

Bu durumda modelin gerçekten yeni örnekleri öğrenip öğrenmediğini anlamak zorlaşır.

Amaç:

> Modelin eğitim verisini ne kadar iyi bildiğini değil, görmediği veriler üzerinde ne kadar iyi çalışabildiğini değerlendirmektir.

Bu kavram **genelleme (generalization)** açısından önemlidir.

İyi bir model yalnızca eğitim örneklerinde değil, benzer özelliklere sahip yeni veriler üzerinde de doğru sonuçlar üretebilmelidir.

---

# 9. `random_state` Nedir?

Veri seti eğitim ve test olarak ayrılırken kayıtlar genellikle rastgele seçilir.

Bu nedenle aynı kod farklı zamanlarda çalıştırıldığında farklı eğitim ve test grupları oluşabilir.

Örneğin:

```python
random_state=42
```

kullanılması, aynı veri ve aynı kod kullanıldığında aynı rastgele bölmenin tekrar elde edilmesini sağlar.

`42` özel veya zorunlu bir sayı değildir.

Önemli olan sabit bir değer kullanıldığında işlemin **tekrarlanabilir** olmasıdır.

---

# 10. Sınıf Dağılımını Korumak

Sınıflandırma problemlerinde eğitim ve test verilerinin sınıf dağılımlarının benzer olması istenebilir.

Örneğin veri setinde phishing ve legitimate örnekleri bulunuyorsa, veri bölünürken bu sınıfların dağılımının korunması yararlı olabilir.

Scikit-learn'de bunun için `stratify` parametresi kullanılabilir.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42,
    stratify=y
)
```

`stratify=y`, hedef değişkendeki sınıf oranlarının eğitim ve test gruplarında yaklaşık olarak korunmasını sağlar.

---

# 11. Eğitim (Training) ve Tahmin (Prediction)

Makine öğrenmesi süreci basitleştirilmiş olarak iki temel aşamada düşünülebilir.

## Eğitim

Model eğitim verisini kullanarak örüntüleri öğrenir.

```python
model.fit(X_train, y_train)
```

## Tahmin

Eğitilmiş model daha önce görmediği test verileri için tahmin üretir.

```python
y_pred = model.predict(X_test)
```

Burada:

- `y_test` → gerçek değerler
- `y_pred` → modelin tahmin ettiği değerler

olarak düşünülebilir.

---

# 12. Makine Öğrenmesi Sürecinin Genel Akışı

Bir makine öğrenmesi projesinin temel adımları şu şekilde özetlenebilir:

```text
Problem Belirleme
       ↓
Veri Toplama / Veri Seti Bulma
       ↓
Veriyi İnceleme
       ↓
Veri Ön İşleme
       ↓
Özellik (X) ve Hedef (y) Ayrımı
       ↓
Eğitim / Test Ayrımı
       ↓
Model Seçimi
       ↓
Model Eğitimi
       ↓
Tahmin
       ↓
Model Değerlendirme
```

Bu derste ilk aşamalar adım adım ele alınmaktadır.

---

# 13. Veri Sızıntısı (Data Leakage)

Makine öğrenmesi çalışmalarında dikkat edilmesi gereken problemlerden biri **veri sızıntısı (data leakage)**dır.

Veri sızıntısı, modelin eğitim sırasında normalde erişmemesi gereken bilgilerden yararlanması durumudur.

Örneğin modelin test verilerindeki sonuçları eğitim sırasında görmesi, gerçek kullanım koşullarını temsil etmeyen yanıltıcı sonuçlara yol açabilir.

Bu nedenle:

- Eğitim ve test verilerinin doğru ayrılması,
- Test verisinin model eğitiminde kullanılmaması,
- Hedef değişkenin yanlışlıkla özellikler arasına dahil edilmemesi

önemlidir.

---

# 14. Siber Güvenlikte Makine Öğrenmesi

Makine öğrenmesi siber güvenlikte birçok farklı problem için kullanılabilir.

Örnekler:

| Siber Güvenlik Problemi | Makine Öğrenmesi Görevi |
|---|---|
| Phishing tespiti | Sınıflandırma |
| Spam e-posta tespiti | Sınıflandırma |
| Malware tespiti | Sınıflandırma |
| Ağ saldırısı tespiti | Sınıflandırma |
| Şüpheli ağ davranışlarının bulunması | Anomali tespiti |
| Benzer saldırı davranışlarının gruplanması | Kümeleme |

Bu derste kullanılan PhiUSIIL veri setindeki temel problem **phishing tespiti**dir.

Modelin amacı web sitelerine ait özelliklerden yararlanarak bir örneğin phishing veya legitimate olup olmadığını tahmin etmektir.

---

# Uygulama

Bu haftanın Google Colab uygulamasında önceki haftalarda kullanılan **PhiUSIIL Phishing URL Dataset** üzerinden makine öğrenmesinin temel çalışma süreci incelenecektir.

Uygulamada:

1. Veri setinin Google Drive üzerinden açılması
2. Özellik ve hedef değişkenin belirlenmesi
3. Makine öğrenmesinde kullanılabilecek özelliklerin incelenmesi
4. `X` ve `y` değişkenlerinin oluşturulması
5. Verinin eğitim ve test olarak ayrılması
6. Eğitim ve test veri boyutlarının incelenmesi
7. Eğitim ve test sınıf dağılımlarının karşılaştırılması
8. Basit bir model üzerinden `fit()` ve `predict()` mantığının görülmesi

işlemleri gerçekleştirilecektir.

Bu haftanın amacı farklı makine öğrenmesi algoritmalarını karşılaştırmak değildir.

---

# Haftanın Özeti

Bu hafta makine öğrenmesinin temel çalışma mantığı ele alınmıştır.

Temel kavramlar:

- **Feature (X):** Modelin tahmin için kullandığı özellikler
- **Target / Label (y):** Modelin tahmin etmeye çalıştığı sonuç
- **Training:** Modelin verilerden öğrenmesi
- **Test:** Modelin görmediği veriler üzerinde değerlendirilmesi
- **Model:** Verideki örüntüleri öğrenen yapı
- **Prediction:** Eğitilmiş modelin yeni veriler için ürettiği tahmin
- **Generalization:** Modelin görmediği veriler üzerinde çalışabilme yeteneği
- **Data Leakage:** Modelin eğitim sırasında erişmemesi gereken bilgilerden yararlanması

Temel Python yapısı:

```python
X = df.drop("label", axis=1)
y = df["label"]

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42,
    stratify=y
)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

Bu kodların her bir bölümü Google Colab uygulamasında adım adım incelenecektir.

---

# Sonraki Hafta

Bir sonraki hafta **Sınıflandırma Modelleri** ele alınacaktır.

Farklı sınıflandırma algoritmalarının aynı siber güvenlik problemi üzerinde nasıl kullanılabileceği incelenecek ve modeller arasındaki temel farklılıklar ele alınacaktır.
