# BGT208 – Yapay Zekâ ve Siber Güvenlik

## Hafta 3 – Python ile Veri Analizi

## Dersin Amacı

Bu haftanın amacı, Python kullanarak bir veri setinin temel yapısını incelemek, veriyi tanımak ve makine öğrenmesi öncesinde veri hakkında temel bilgiler elde etmektir.

Önceki hafta siber güvenlik problemlerine uygun veri setlerinin nasıl bulunabileceği ve bir veri setinin Google Colab ortamına nasıl aktarılabileceği ele alınmıştır.

Bu hafta ise elimizde bulunan veriyi **Python ile incelemeye ve anlamaya** başlayacağız.

Bir veri seti üzerinde çalışmaya başlamadan önce şu soruların cevaplanması önemlidir:

- Veri seti kaç kayıt içeriyor?
- Hangi sütunlar bulunuyor?
- Sütunların veri tipleri nelerdir?
- Eksik değerler var mı?
- Tekrarlanan kayıtlar var mı?
- Sayısal değişkenlerin temel özellikleri nelerdir?
- Hedef değişkende hangi sınıflar bulunuyor?
- Sınıfların dağılımı nasıl?

Bu işlemler, veriyi anlamanın ve sonraki aşamalarda makine öğrenmesine hazırlamanın temelini oluşturur.

---

# 1. Python ile Veri Analizi

Python, veri analizi ve makine öğrenmesi çalışmalarında yaygın olarak kullanılan bir programlama dilidir.

Python'un bu alanlarda yaygın kullanılmasının önemli nedenlerinden biri, veri analizi ve makine öğrenmesi için geliştirilmiş çok sayıda kütüphaneye sahip olmasıdır.

Bu ders kapsamında kullanacağımız temel kütüphaneler:

| Kütüphane | Kullanım Amacı |
|---|---|
| **Pandas** | Tablo biçimindeki verileri okuma ve işleme |
| **NumPy** | Sayısal işlemler |
| **Matplotlib** | Veri görselleştirme |
| **Scikit-learn** | Makine öğrenmesi uygulamaları |

Bu hafta ağırlıklı olarak **Pandas** ve **Matplotlib** kullanılacaktır.

---

# 2. Pandas Kütüphanesi

**Pandas**, Python'da tablo biçimindeki verileri okumak, incelemek ve işlemek için kullanılan bir kütüphanedir.

Pandas genellikle aşağıdaki şekilde programa dahil edilir:

```python
import pandas as pd
```

Buradaki `pd`, Pandas kütüphanesi için kullanılan kısa addır.

---

# 3. DataFrame Nedir?

Pandas içerisinde en sık kullanılan veri yapılarından biri **DataFrame**'dir.

DataFrame, satır ve sütunlardan oluşan iki boyutlu tablo yapısıdır.

Örneğin:

| URL_Length | NoOfDots | NoOfLetters | label |
|---:|---:|---:|---:|
| 54 | 2 | 38 | 1 |
| 126 | 5 | 74 | 0 |
| 43 | 1 | 31 | 1 |

Bu tabloda:

- Her **satır** bir kaydı (gözlemi),
- Her **sütun** bir değişkeni,
- `label` ise tahmin edilmek istenen hedef değişkeni temsil edebilir.

Siber güvenlik veri setlerinde bir satır; bir URL'yi, ağ bağlantısını, e-postayı, dosyayı veya sistem olayını temsil edebilir.

---

# 4. CSV Dosyasının Okunması

CSV biçimindeki bir veri setini Pandas ile okumak için `read_csv()` fonksiyonu kullanılabilir.

```python
df = pd.read_csv("veri.csv")
```

Burada:

- `pd` → Pandas kütüphanesini,
- `read_csv()` → CSV dosyasını okuyan fonksiyonu,
- `df` → oluşturulan DataFrame'i

ifade eder.

---

# 5. Veri Setine İlk Bakış

Bir veri seti yüklendikten sonra ilk olarak birkaç kaydın incelenmesi yararlıdır.

### İlk kayıtlar

```python
df.head()
```

`head()` varsayılan olarak veri setinin ilk 5 satırını gösterir.

İstenilen satır sayısı parantez içerisinde belirtilebilir:

```python
df.head(10)
```

### Son kayıtlar

```python
df.tail()
```

`tail()` veri setinin son 5 satırını gösterir.

### Rastgele kayıtlar

```python
df.sample(5)
```

`sample()` veri setinden rastgele 5 kayıt görüntüler.

Bu işlemler veri setinin genel yapısı hakkında ilk fikirleri edinmemizi sağlar.

---

# 6. Veri Setinin Boyutu

Veri setinin kaç satır ve kaç sütundan oluştuğunu görmek için:

```python
df.shape
```

kullanılır.

Sonuç:

```text
(satır sayısı, sütun sayısı)
```

biçimindedir.

Örneğin:

```text
(10000, 20)
```

sonucu, veri setinin **10.000 kayıt ve 20 sütundan** oluştuğunu gösterir.

---

# 7. Sütunların İncelenmesi

Veri setindeki sütun isimlerini görüntülemek için:

```python
df.columns
```

kullanılır.

Sütunların incelenmesi, veri setinde hangi bilgilerin bulunduğunu anlamamıza yardımcı olur.

Makine öğrenmesinde modelin tahmin yaparken kullandığı değişkenlere **özellik (feature)** adı verilir.

Tahmin edilmek istenen değişken ise **hedef değişken (target/label)** olarak adlandırılır.

---

# 8. Veri Tiplerinin İncelenmesi

Bir veri setindeki bütün sütunlar aynı türde veri içermek zorunda değildir.

Python'da sık karşılaşılan veri tiplerinden bazıları:

| Veri Tipi | Açıklama |
|---|---|
| `int` | Tam sayı |
| `float` | Ondalıklı sayı |
| `object` | Metin veya kategorik veri |
| `bool` | Doğru / yanlış değerleri |

Sütunların veri tiplerini görmek için:

```python
df.dtypes
```

kullanılabilir.

Veri seti hakkında daha ayrıntılı bilgi almak için:

```python
df.info()
```

komutu kullanılabilir.

`info()` ile;

- sütun isimleri,
- boş olmayan değer sayıları,
- veri tipleri

birlikte görüntülenebilir.

---

# 9. Temel İstatistiksel Bilgiler

Sayısal sütunların temel istatistiklerini görmek için:

```python
df.describe()
```

kullanılır.

Bu komut aşağıdaki bilgileri gösterebilir:

| Değer | Anlamı |
|---|---|
| `count` | Gözlem sayısı |
| `mean` | Ortalama |
| `std` | Standart sapma |
| `min` | Minimum değer |
| `25%` | Birinci çeyrek |
| `50%` | Medyan |
| `75%` | Üçüncü çeyrek |
| `max` | Maksimum değer |

Bu değerler değişkenlerin genel yapısı ve dağılımı hakkında bilgi verir.

---

# 10. Eksik Verilerin Kontrol Edilmesi

Gerçek veri setlerinde bazı değerler eksik olabilir.

Eksik değerleri kontrol etmek için:

```python
df.isnull().sum()
```

kullanılabilir.

Bu işlem her sütunda kaç eksik değer bulunduğunu gösterir.

Eksik veriler sonraki analizleri ve makine öğrenmesi modellerini etkileyebileceği için kontrol edilmelidir.

---

# 11. Tekrarlanan Kayıtların Kontrol Edilmesi

Bir veri setinde aynı kayıt birden fazla kez bulunabilir.

Tekrarlanan kayıtların sayısını görmek için:

```python
df.duplicated().sum()
```

kullanılabilir.

Tekrarlanan kayıtlar veri kalitesini ve yapılacak analizleri etkileyebilir.

Bu nedenle veri seti incelenirken tekrar eden kayıtlar da kontrol edilmelidir.

---

# 12. Hedef Değişkenin İncelenmesi

Sınıflandırma problemlerinde hedef değişkenin hangi sınıflardan oluştuğunu ve her sınıfta kaç örnek bulunduğunu incelemek önemlidir.

Örneğin hedef sütunun adı `label` ise:

```python
df["label"].value_counts()
```

kullanılabilir.

Örneğin:

```text
1    6000
0    4000
```

sonucu veri setinde iki farklı sınıf bulunduğunu ve bu sınıflardaki kayıt sayılarının farklı olduğunu gösterir.

Sınıflardaki örnek sayılarının birbirinden çok farklı olması **sınıf dengesizliği (class imbalance)** olarak adlandırılır.

---

# 13. Veri Seçme ve Filtreleme

Veri analizi sırasında yalnızca belirli sütunları veya belirli koşulları sağlayan kayıtları incelemek isteyebiliriz.

### Bir sütunun seçilmesi

```python
df["label"]
```

### Birden fazla sütunun seçilmesi

```python
df[["URL_Length", "NoOfDots", "label"]]
```

### Belirli bir koşula göre filtreleme

Örneğin yalnızca `label` değeri `0` olan kayıtları görüntülemek için:

```python
df[df["label"] == 0]
```

`label` değeri `1` olan kayıtları görüntülemek için:

```python
df[df["label"] == 1]
```

Filtreleme, belirli veri gruplarını ayrı ayrı incelememizi sağlar.

---

# 14. Basit Veri Görselleştirme

Verileri yalnızca tablolar üzerinden incelemek her zaman yeterli olmayabilir.

Grafikler, verideki dağılımları ve farklılıkları daha kolay görmemizi sağlar.

Python'da temel veri görselleştirme işlemleri için **Matplotlib** kütüphanesi kullanılabilir.

```python
import matplotlib.pyplot as plt
```

Örneğin hedef değişkenin sınıf dağılımını göstermek için:

```python
df["label"].value_counts().plot(kind="bar")

plt.xlabel("Sınıf")
plt.ylabel("Kayıt Sayısı")
plt.title("Sınıf Dağılımı")

plt.show()
```

Bu grafik her sınıfta bulunan kayıt sayısının görsel olarak karşılaştırılmasını sağlar.

---

# 15. Keşifsel Veri Analizi (EDA)

Bir veri setinin model geliştirilmeden önce sistematik biçimde incelenmesine **Keşifsel Veri Analizi (Exploratory Data Analysis – EDA)** adı verilir.

EDA'nın temel amacı **veriyi anlamaktır**.

Bu süreçte şu sorulara cevap aranabilir:

- Veri setinin büyüklüğü nedir?
- Hangi değişkenler bulunuyor?
- Değişkenlerin veri tipleri nelerdir?
- Eksik değerler var mı?
- Tekrarlanan kayıtlar var mı?
- Değişkenlerin temel istatistikleri nelerdir?
- Hedef değişkenin dağılımı nasıldır?
- Veride dikkat çeken durumlar var mı?

EDA sonucunda elde edilen bilgiler, sonraki aşamalarda gerçekleştirilecek veri ön işleme ve makine öğrenmesi çalışmalarına temel oluşturur.

---

# 16. Siber Güvenlik Açısından Veriyi Yorumlama

Veri analizi yalnızca Python komutlarını çalıştırmaktan ibaret değildir.

Asıl amaç elde edilen bilgileri **siber güvenlik problemi açısından yorumlamaktır.**

Bir siber güvenlik veri seti incelenirken şu sorular sorulabilir:

- Veri setindeki her kayıt neyi temsil ediyor?
- Hangi sütunlar güvenlik açısından anlamlı bilgiler içeriyor?
- Hedef değişken nedir?
- Hedef değişkende hangi sınıflar bulunuyor?
- Normal ve zararlı örneklerin sayıları nasıl dağılıyor?
- Eksik veya tekrarlanan kayıtlar bulunuyor mu?
- Bazı özellikler normal ve zararlı örneklerde farklı davranıyor olabilir mi?

Bu soruların cevapları, sonraki aşamada uygulanacak makine öğrenmesi yöntemleri için yol gösterir.

---

# Uygulama

Bu haftanın Google Colab uygulamasında önceki hafta kullanılan **PhiUSIIL Phishing URL Dataset** üzerinde Python ile veri analizi gerçekleştirilecektir.

Uygulamada sırasıyla:

1. Veri setinin yüklenmesi
2. İlk, son ve rastgele kayıtların görüntülenmesi
3. Veri setinin boyutunun belirlenmesi
4. Sütunların incelenmesi
5. Veri tiplerinin incelenmesi
6. Temel istatistiklerin görüntülenmesi
7. Eksik değerlerin kontrol edilmesi
8. Tekrarlanan kayıtların kontrol edilmesi
9. Hedef değişkenin incelenmesi
10. Veri seçme ve filtreleme
11. Sınıf dağılımının görselleştirilmesi
12. Sonuçların siber güvenlik açısından yorumlanması

işlemleri gerçekleştirilecektir.

---

# Haftanın Özeti

Bu hafta Python ve Pandas kullanılarak bir veri setinin temel olarak nasıl incelenebileceği ele alınmıştır.

Kullanılan temel komutlar:

```python
df.head()
df.tail()
df.sample()
df.shape
df.columns
df.dtypes
df.info()
df.describe()
df.isnull().sum()
df.duplicated().sum()
df["label"].value_counts()
```

Ayrıca veri seçme, filtreleme ve temel veri görselleştirme işlemleri incelenmiştir.

Bu işlemlerin amacı yalnızca kod çalıştırmak değil, **makine öğrenmesi modeli geliştirilmeden önce veriyi tanımak ve veri kalitesini değerlendirmektir.**

Bir sonraki hafta **makine öğrenmesinin temel kavramları** ele alınacaktır.
