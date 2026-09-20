# 🏠 Kira Fiyatı Tahmini — İzmir / Buca

İzmir'in Buca ilçesindeki kiralık konut ilanları kullanılarak **kira fiyatlarının analiz edilmesi ve makine öğrenmesi modelleriyle tahmin edilmesi** amacıyla geliştirilmiş bir veri analizi ve makine öğrenmesi projesidir.

Projede veri temizleme, keşifsel veri analizi (EDA), özellik mühendisliği ve modelleme adımlarının ardından **Linear Regression** ve **XGBoost** modelleri karşılaştırılmıştır.

---

## 🎯 Projenin Amacı

Bu projenin temel amacı, konut özellikleri ile kira fiyatı arasındaki ilişkiyi incelemek ve verilen konut özelliklerinden hareketle tahmini kira fiyatı üretmektir.

Proje kapsamında özellikle şu sorulara odaklanılmıştır:

* Konutun metrekare büyüklüğü kira fiyatını nasıl etkiliyor?
* Oda ve salon sayısının kira üzerindeki etkisi nedir?
* Bina yaşı ile kira fiyatı arasında nasıl bir ilişki var?
* Kat bilgisi kira fiyatlarını etkiliyor mu?
* Mahalleler arasında kira fiyatları nasıl değişiyor?
* Linear Regression ve XGBoost modellerinin tahmin performansları nasıl farklılaşıyor?

---

## 📊 Veri Seti

Veri seti **Hepsiemlak'tan alınan İzmir/Buca kiralık konut ilanlarından** oluşmaktadır.

Veri içerisinde konutların:

* Kira fiyatı
* Metrekare bilgisi
* Oda sayısı
* Salon sayısı
* Bina yaşı
* Kat bilgisi
* Kat tipi
* Mahalle

gibi özellikleri kullanılmaktadır.

> ⚠️ Veri yalnızca İzmir/Buca bölgesindeki ilanlardan oluştuğu için elde edilen sonuçların farklı şehir ve ilçelere doğrudan genellenmesi uygun değildir.

---

## 🔎 Proje Akışı

```text
Ham Veri
   ↓
Veri Temizleme
   ↓
Aykırı Değer Analizi
   ↓
Keşifsel Veri Analizi (EDA)
   ↓
Özelliklerin Hazırlanması
   ↓
Train / Test Ayrımı
   ↓
Linear Regression
   ↓
XGBoost
   ↓
Model Değerlendirme
   ↓
Model Karşılaştırması
   ↓
Örnek Kira Tahmini
```

---

## 🧹 Veri Ön İşleme

Ham veri içerisindeki metinsel değerler analiz edilebilir sayısal değişkenlere dönüştürülmüştür.

Örneğin:

* `130 m²` → `130`
* `25 Yaşında` → `25`
* `4 + 1` → `4 oda + 1 salon`
* `20.000` → `20000 TL`

Ayrıca:

* Eksik değerler ele alınmıştır.
* Tekrarlanan ilanlar temizlenmiştir.
* Günlük kiralık ilanlar filtrelenmiştir.
* Satılık ilan gibi kira tahminini bozabilecek kayıtlar çıkarılmıştır.
* Mahalle değişkeni **One-Hot Encoding** ile dönüştürülmüştür.
* Kat bilgisi sayısal kat ve kat tipi olarak ayrılmıştır.

---

## 📈 Keşifsel Veri Analizi

Projede kira fiyatı ile farklı konut özellikleri arasındaki ilişkiler incelenmiştir.

### İncelenen ilişkiler

* Kira ↔ Metrekare
* Kira ↔ Oda sayısı
* Kira ↔ Bina yaşı
* Kira ↔ Kat tipi
* Kira ↔ Mahalle
* Sayısal değişkenler arasındaki korelasyon

Bu analizler sayesinde modelleme öncesinde veri setinin yapısı ve değişkenlerin kira fiyatıyla ilişkisi incelenmiştir.

---

## 🤖 Kullanılan Modeller

Projede iki farklı regresyon modeli kullanılmıştır.

### 1. Linear Regression

Temel ve yorumlanabilir bir regresyon modeli olarak kullanılmıştır.

Modelin amacı, konut özellikleri ile kira fiyatı arasındaki doğrusal ilişkileri incelemektir.

### 2. XGBoost

Daha karmaşık ve doğrusal olmayan ilişkileri yakalayabilen **XGBoost Regressor** modeli kullanılmıştır.

Hiperparametre optimizasyonu için:

* GridSearchCV
* 5-Fold Cross Validation

kullanılmıştır.

Her iki model de:

* Aynı özellikler
* Aynı train/test bölünmesi
* Aynı veri ön işleme süreci

üzerinden karşılaştırılmıştır.

---

## 📏 Model Değerlendirme

Modeller aşağıdaki metrikler kullanılarak değerlendirilmiştir:

| Metrik   | Açıklama                              |
| -------- | ------------------------------------- |
| **RMSE** | Tahmin hatalarının karekök ortalaması |
| **MAE**  | Ortalama mutlak hata                  |
| **MAPE** | Ortalama yüzde hata                   |
| **R²**   | Modelin açıklama gücü                 |

Ayrıca model performansının daha güvenilir şekilde incelenebilmesi için **5-Fold Cross Validation** uygulanmıştır.

---

## 📊 Görselleştirmeler

Projede aşağıdaki görselleştirmeler oluşturulmuştur:

* 📌 Kira - metrekare ilişkisi
* 📌 Kira - oda sayısı ilişkisi
* 📌 Kira - bina yaşı ilişkisi
* 📌 Kira - kat tipi ilişkisi
* 📌 Korelasyon matrisi
* 📌 Mahallelere göre kira dağılımı
* 📌 Gerçek değer - tahmin edilen değer karşılaştırması
* 📌 XGBoost özellik önemleri
* 📌 Linear Regression katsayıları

---

## 🔮 Örnek Tahmin

Model kullanılarak örnek bir konut için kira tahmini yapılabilmektedir.

Örneğin:

```text
100 m²
3 + 1
5 yaşında
3. kat
Atatürk Mahallesi
```

gibi konut özellikleri modele verilerek tahmini kira fiyatı elde edilebilir.

---

## 🛠️ Kullanılan Teknolojiler

* 🐍 Python
* 🐼 Pandas
* 🔢 NumPy
* 📊 Matplotlib
* 📈 Seaborn
* 🤖 Scikit-learn
* ⚡ XGBoost
* 📓 Jupyter Notebook

---

## 📁 Proje Dosya Yapısı

```text
kira-fiyati-tahmini/
│
├── hepsiemlak.csv
├── Verianalizi.ipynb
├── Teknik_Rapor_Kira_Tahmini.pdf
└── README.md
```

### Dosyalar

**`hepsiemlak.csv`**
Konut ilanlarından oluşan veri seti.

**`Verianalizi.ipynb`**
Veri temizleme, EDA, modelleme, değerlendirme ve tahmin işlemlerinin gerçekleştirildiği Jupyter Notebook.

**`Teknik_Rapor_Kira_Tahmini.pdf`**
Projenin teknik raporu.

---

## 🚀 Kurulum

Projeyi bilgisayarınıza klonlayın:

```bash
git clone https://github.com/kullanici-adi/kira-fiyati-tahmini.git
```

Proje klasörüne geçin:

```bash
cd kira-fiyati-tahmini
```

Gerekli kütüphaneleri yükleyin:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
```

Jupyter Notebook'u çalıştırın:

```bash
jupyter notebook
```

Ardından:

```text
Verianalizi.ipynb
```

dosyasını açarak hücreleri sırasıyla çalıştırabilirsiniz.

---

## 📌 Proje Çıktısı

Bu proje ile gerçek bir konut ilanı veri seti üzerinde:

**Veri Toplama → Veri Temizleme → EDA → Özellik Hazırlama → Makine Öğrenmesi → Model Değerlendirme → Kira Tahmini**

süreci uçtan uca uygulanmıştır.

Proje aynı zamanda farklı regresyon algoritmalarının aynı veri ve değerlendirme koşulları altında karşılaştırılması üzerine kurulmuştur.

---

## 👩‍💻 Proje

**Sakine Cansu Topci**

Yönetim Bilişim Sistemleri (YBS) Mezunu

Veri Analizi & Makine Öğrenmesi Projeleri
