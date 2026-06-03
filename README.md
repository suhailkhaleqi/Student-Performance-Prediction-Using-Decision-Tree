# 📚 Student Performance Prediction Using Decision Tree

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.2+-orange.svg)](https://scikit-learn.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## 📌 Proje Hakkında

Bu proje, Portekiz ortaöğretim öğrencilerinin akademik başarısını **Karar Ağacı (Decision Tree)** algoritması kullanarak tahmin etmeyi amaçlamaktadır. Proje, Bursa Teknik Üniversitesi BLM0463 Veri Madenciliğine Giriş dersi kapsamında hazırlanmıştır.

### 🎯 Hedef
Öğrencilerin demografik özellikleri, aile yapıları, çalışma alışkanlıkları ve önceki dönem notlarını kullanarak final notunu (G3) 3 sınıfa ayırmak:
- **Low** (Düşük): G3 < 10
- **Medium** (Orta): 10 ≤ G3 < 15  
- **High** (Yüksek): G3 ≥ 15

### 📊 Model Başarısı
- **Doğruluk (Accuracy):** %89.08
- **Kesinlik (Precision):** %89.47
- **Duyarlılık (Recall):** %89.08
- **F1-Skor:** %89.17

---

## 📁 Veri Seti

| Özellik | Değer |
|---------|-------|
| **Kaynak** | UCI Machine Learning Repository |
| **Yazarlar** | Cortez & Silva (2008) |
| **Dosya Adı** | `student-mat.csv` |
| **Öğrenci Sayısı** | 395 |
| **Özellik Sayısı** | 33 |
| **Hedef Değişken** | G3 (Final notu) |
| **Eksik Veri** | Yok |

### Değişken Açıklamaları

| Değişken | Anlamı | Tipi |
|----------|--------|------|
| school | Okul kodu (GP/MS) | Kategorik |
| sex | Cinsiyet (F/M) | Kategorik |
| age | Yaş (15-22) | Sayısal |
| G1 | 1. dönem notu | Sayısal |
| G2 | 2. dönem notu | Sayısal |
| G3 | Final notu | Sayısal (Hedef) |
| failures | Geçmişte kalma sayısı | Sayısal |
| studytime | Haftalık çalışma süresi | Sayısal |
| absences | Devamsızlık gün sayısı | Sayısal |
| ... | (Toplam 33 özellik) | ... |

---

![image alt](https://github.com/suhailkhaleqi/Student-Performance-Prediction-Using-Decision-Tree/blob/04932add3abd195bc98b24bb92924586bc79acc5/images/1_sinif_dagilimi.png)


## 🛠️ Kullanılan Teknolojiler

| Kütüphane | Versiyon | Kullanım Amacı |
|-----------|----------|----------------|
| pandas | 1.5+ | Veri işleme ve analiz |
| numpy | 1.23+ | Sayısal hesaplamalar |
| matplotlib | 3.6+ | Grafik çizimi |
| seaborn | 0.12+ | İstatistiksel görselleştirme |
| scikit-learn | 1.2+ | Makine öğrenmesi algoritmaları |

## 📊 Proje Adımları

### 1. Veri Ön İşleme (Preprocessing)
- Veri yükleme ve eksik veri kontrolü
- Kategorik değişkenlerin Label Encoding ile dönüştürülmesi
- Hedef değişkenin (G3) 3 sınıfa ayrılması
- **G1 ve G2 değişkenleri modele dahil edildi**
- Eğitim/Test ayrımı: %70 / %30 (stratify ile)

### 2. Keşifsel Veri Analizi (EDA)
- Korelasyon matrisi ve ısı haritası
- G3 ile en yüksek korelasyon gösteren özellikler
- Çalışma süresi, devamsızlık, internet erişimi ve anne eğitiminin başarıya etkisi

### 3. Model Geliştirme
- Karar Ağacı (Decision Tree) algoritması
- **Hiperparametre Optimizasyonu (GridSearchCV)**
  - `max_depth`: 3, 5, 7, 10
  - `min_samples_split`: 2, 5, 10
  - `criterion`: gini, entropy

**En İyi Parametreler:**

| Parametre | Değer |
|-----------|-------|
| max_depth | 3 |
| min_samples_split | 2 |
| criterion | entropy |

### 4. Model Performansı
- Accuracy, Precision, Recall, F1-Score
- Sınıf bazında performans tablosu
- Karışıklık Matrisi (Confusion Matrix)
- ROC Eğrisi ve AUC
- 5-Fold Cross-Validation

### 5. Özellik Önem Analizi (Feature Importance)

| Sıra | Özellik | Önem Skoru |
|------|---------|------------|
| 1 | G2 | 0.452 |
| 2 | G1 | 0.421 |
| 3 | failures | 0.058 |
| 4 | higher | 0.021 |
| 5 | Medu | 0.012 |

> **G1 ve G2 birlikte toplam önemin %87.3'ünü oluşturmaktadır.**

---

## 📈 Sonuçlar

### Performans Metrikleri

| Metrik | Değer |
|--------|-------|
| **Accuracy** | **%89.08** |
| **Precision** | %89.47 |
| **Recall** | %89.08 |
| **F1-Score** | %89.17 |

### Sınıf Bazında Performans

| Sınıf | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| High | 0.86 | 0.86 | 0.86 | 22 |
| Low | 0.87 | 0.87 | 0.87 | 39 |
| Medium | 0.92 | 0.91 | 0.92 | 58 |

### Cross-Validation (5-fold)
- **Ortalama Accuracy:** %87.5
- **Standart Sapma:** ±%2.1

---

## 📚 Literatür Karşılaştırması

| Metrik | Cortez & Silva (2008) | Bu Proje | Fark |
|--------|----------------------|----------|------|
| Accuracy | %90.7 | %89.08 | -%1.62 |

> Bu projede daha zor bir problem olan **3 sınıflı sınıflandırma** yapılmış olmasına rağmen, literatürdeki binary sınıflandırma sonucuna sadece %1.62 farkla yaklaşılmıştır. Bu, modelin başarılı olduğunu göstermektedir.
