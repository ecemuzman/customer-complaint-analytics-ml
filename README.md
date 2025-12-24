# 📊 Customer Complaint Analytics (ML)

## 📌 Proje Özeti
**customer-complaint-analytics-ml**, müşteri şikayetlerini yalnızca sınıflandırmakla kalmayıp, aynı zamanda **müşteri kaybı (churn) riskini proaktif olarak tespit etmeyi** hedefleyen uçtan uca bir karar destek sistemidir.  

BERT tabanlı Derin Öğrenme ve NLP teknikleri kullanılarak;
- Şikayet alt kategori tahmini  
- Churn sinyal analizi  
- Dinamik churn skoru hesaplama  
- Benzer şikayet analizi  
- Zaman serisi tahmini  

tek bir **Streamlit tabanlı interaktif platform** altında sunulmaktadır.

🌐 **Canlı Demo (Streamlit):**  
👉 https://customercomplaintclassificationchurnscore-8iyyvutmqfyt59nku84u.streamlit.app/

---

## 🚀 Temel Özellikler

### 🔍 Şikayet Alt Kategori Tahmini
BERT tabanlı sınıflandırma modeli ile şikayetler otomatik olarak aşağıdaki alt kategorilere ayrılır:
- Ürün sorunları (performans, kalite)
- Uygulama sorunları (ödeme, kupon)
- İade reddi
- İade süreci
- Garanti sorunları
- Satıcı sipariş iptali
- Kargo teslimat sorunları
- Yanlış veya eksik ürün gönderimi
- Fiyat farkı talebi
- Teslim edilmeyen paket

---

### 🔔 Churn Sinyal Kategorileri (Keyword-Based)
Şikayet metinleri içerisinde geçen anahtar kelime ve ifade kalıpları üzerinden **8 farklı churn sinyali** tespit edilir:

1. **Kesin Kopuş** – “bir daha asla”, “alışveriş yapmayacağım”  
2. **Duygusal Kopuş** – hayal kırıklığı, pişmanlık  
3. **Çözümsüzlük & Güven Kaybı** – geri dönüş yapılmadı  
4. **Mağduriyet** – mağdur oldum  
5. **Sabır Tükenişi** – defalarca, hâlâ çözülmedi  
6. **Tekrarlayan Problem** – aynı sorun tekrar  
7. **Yasal Tehdit** – hakem heyeti, hukuki süreç  
8. **İlk Kez Sorun** – düşük riskli ancak izlenmeli sinyal  

---

### 📏 Churn Skoru Hesaplama Mantığı
Churn skoru;
- Tespit edilen churn sinyallerinin ağırlıkları  
- Şikayet metni uzunluğu  
- Tahmin edilen alt kategori etkisi  

birlikte değerlendirilerek **dinamik olarak** hesaplanır.

#### 🎯 Churn Bandları
- 🟣 **Kritik Risk (MOR)**: ≥ 70  
- 🔴 **Yüksek Risk (KIRMIZI)**: ≥ 50  
- 🟡 **Orta Risk (SARI)**: ≥ 35  
- 🟢 **Düşük Risk (YEŞİL)**: < 35  

---

### 📊 Dashboard & Analitik
- KPI kartları (ortalama churn skoru, yüksek riskli şikayetler)
- Churn band dağılımı
- Alt kategori × churn band analizi
- En sık tetiklenen churn sinyalleri
- Birim bazlı ortalama churn skorları
- Gelişmiş filtreleme (kategori, tarih, risk bandı)

---

### 📈 Zaman Serisi Analizi
- **SARIMAX** ile günlük şikayet tahmini  
- **Prophet** ile haftalık trend analizi  
- Anomali tespiti  
- Kategori bazlı özelleştirilmiş analizler  

---

## 🛠️ Kurulum & Çalıştırma

```bash
git clone https://github.com/<username>/customer-complaint-analytics-ml.git
cd customer-complaint-analytics-ml

python -m venv venv
source venv/bin/activate   # Mac/Linux
pip install -r requirements.txt

streamlit run app.py

Proje Yapısı

customer-complaint-analytics-ml/
├── app.py
├── README.md
├── requirements.txt
├── bert_based_classification_models/
├── df_weigthed_final.pkl
└── .gitignore



Geliştirici

Ecem Uzman

Data Science | NLP | Machine Learning



