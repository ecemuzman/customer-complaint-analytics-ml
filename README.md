# 📊 Şikayet Analiz Sistemi

## 📌 Proje Hakkında

Bu proje, müşteri şikayetlerini yalnızca sınıflandırmakla kalmayıp, aynı zamanda bu şikayetlerden **churn (müşteri kaybı) riskini proaktif olarak tespit etmeyi** amaçlayan modern ve kapsamlı bir karar destek platformudur. **BERT tabanlı derin öğrenme (Deep Learning) ve NLP yaklaşımları** kullanılarak müşteri şikayetleri analiz edilmekte; alt kategori tahmini, churn sinyal tespiti, dinamik churn skoru hesaplama, benzer şikayet analizi ve zaman serisi tahminleri tek bir platform altında birleştirilmektedir. Streamlit tabanlı interaktif arayüz sayesinde hem operasyonel ekipler hem de karar vericiler için **ölçülebilir, yorumlanabilir ve aksiyon alınabilir içgörüler** sunulmaktadır.

🌐 **Canlı Uygulama (Streamlit Demo):**  
Müşteri şikayetlerini analiz ederek alt kategori, churn skoru, churn bandı ve tetiklenen sinyalleri gerçek zamanlı olarak görüntüleyebilirsiniz.  
👉 https://customercomplaintclassificationchurnscore-8iyyvutmqfyt59nku84u.streamlit.app/

## 🚀 Özellikler

### 🔍 Şikayet Analizi (Alt Kategoriler)
- Otomatik Kategori Tahmini**: BERT tabanlı Derin Öğrenme (DL) modeli ile şikayetleri 10 farklı alt kategoriye sınıflandırır
- Ürün ile ilgili sorunlar ( ürün performansı, ürün kalitesi vb. )           
- Uygulama  ( kupon sorunu, ödeme sorunu )                           
- İade reddi                         
- Garanti sorunu                       
- İade süreci                         
- Satıcı sipariş iptali                 
- Kargo teslimat sorunu  ( hasarlı paket, geç teslimat, kargoya geç teslim ve kargoya teslim edilmemiş paket)              
- Yanlış veya eksik ürün gönderimi    
- Fiyat farkı talebi                  
- Müşteriye teslim edilmeyen paket 


## 🔍 Churn Sinyal Kategorileri (Keyword-Based)

Bu projede churn sinyalleri, müşteri şikayet metinleri içerisinde geçen **anahtar kelime ve kalıplar** üzerinden tespit edilmektedir. Her sinyal kategorisi, churn riskini temsil eden farklı bir davranışsal örüntüyü ifade eder.

### 1️⃣ Kesin Kopuş
Müşterinin platformla ilişkiyi tamamen sonlandırma niyetini açıkça ifade ettiği sinyallerdir.  
Örn: *"bir daha alışveriş yapmayacağım",  "bir daha asla"*
### 2️⃣ Duygusal Kopuş
Hayal kırıklığı, pişmanlık ve güven kaybını yansıtan duygusal ifadeleri kapsar.  
Örn: *"hayal kırıklığı yaşadım", "pişman oldum"*
### 3️⃣ Çözümsüzlük & Güven Kaybı
Müşterinin geri dönüş alamadığını veya çözüm sunulmadığını belirttiği sinyallerdir.  
Örn: *"geri dönüş yapılmadı", "çözüm sunulmadı"*
### 4️⃣ Mağduriyet
Müşterinin kendisini mağdur hissettiğini ve bunun giderilmesini talep ettiği durumları ifade eder.  
Örn: *"mağdur oldum", "mağduriyetim devam ediyor"*
### 5️⃣ Sabır Tükenişi
Sorunun uzun süredir devam ettiğini ve müşterinin sabrının azaldığını gösteren ifadeleri kapsar.  
Örn: *"defalarca", "halen çözülmedi", "artık"*
### 6️⃣ Tekrarlayan Problem
Aynı veya benzer sorunların daha önce de yaşandığını belirten sinyallerdir.  
Örn: *"daha önce de benzer", "aynı sorun tekrar"*
### 7️⃣ Yasal Tehdit
Müşterinin hukuki veya resmi mercilere başvurma niyetini ifade ettiği yüksek riskli sinyallerdir.  
Örn: *"tüketici hakem heyeti", "hukuki süreç"*
### 8️⃣ İlk Kez Sorun
Müşterinin ilk defa sorun yaşadığını belirtmesi; düşük riskli ancak izlenmesi gereken sinyaldir.  
Örn: *"ilk kez böyle bir sorun", "ilk kez başıma geliyor"*

### 📏 Şikayet Uzunluğu & Alt Kategori Katkısı

Churn skoru yalnızca anahtar kelime bazlı sinyallerle değil; **şikayet metninin uzunluğu** ve **tahmin edilen alt kategori bilgisi** ile birlikte hesaplanmaktadır.

- **Şikayet Uzunluğu:**  
  Uzun ve detaylı şikayet metinleri, müşterinin konuya harcadığı eforu ve memnuniyetsizlik seviyesini yansıttığı için churn skoruna ek bir risk faktörü olarak dahil edilmiştir.

- **Alt Kategori Etkisi:**  
  Şikayetler, NLP tabanlı sınıflandırma modeli ile alt kategorilere ayrılmakta ve her alt kategori churn riski açısından farklı ağırlıklarla değerlendirilerek skora katkı sağlamaktadır.

Bu çok boyutlu yaklaşım sayesinde churn skoru; metinsel sinyaller, içerik yoğunluğu ve operasyonel bağlam birlikte değerlendirilerek oluşturulmaktadır.

### ⚙️ Scoring Logic (Summary)
Tespit edilen churn sinyalleri, `CATEGORY_WEIGHTS` üzerinden ağırlıklandırılarak **dinamik churn skoruna** dönüştürülür. Bir şikayet metninde birden fazla sinyal bulunabilir ve toplam risk skoru bu sinyallerin ağırlıklarına göre hesaplanır.

- **Churn Skoru Hesaplama**: Dinamik algoritma ile müşteri kaybı riskini ölçer
- **Churn Band Sınıflandırması**: 
  - 🟣 **Kritik Riskli (MOR)**: ≥70 skor
  - 🔴 **Yüksek Yüksek (KIRMIZI)**: ≥50 skor
  - 🟡 **Orta Riskli (SARI)**: ≥35 skor
  - 🟢 **Düşük Riskli (YEŞİL)**: <35 skor
- **Benzer Şikayetler**: Cosine similarity ile en benzer 10 şikayeti bulur
- **Churn Sinyal Analizi**: 8 farklı churn sinyalini tespit eder

### 📊 Dashboard
- **KPI Kartları**: Toplam şikayet, ortalama churn skoru, yüksek riskli şikayetler
- **Churn Band Dağılımı**: Görsel pie chart ile risk dağılımı
- **Birim Bazlı Analiz**: Ana kategorilere göre şikayet dağılımı
- **Alt Kategori Analizi**: Churn band renkli stacked bar chart
- **Churn Sinyal Analizi**: En çok tetiklenen sinyaller
- **Birim × Churn Skoru**: Birim bazlı ortalama churn skorları
- **Churn Skoru Dağılımı**: Histogram ile skor dağılımı
- **Gelişmiş Filtreleme**: Ana kategori, alt kategori, churn band ve tarih aralığı

### 📈 Zaman Serisi Analizi
- **Günlük Tahmin**: SARIMAX modeli ile günlük şikayet tahmini
- **Haftalık Tahmin**: Prophet modeli ile haftalık trend analizi
- **Anomali Tespiti**: İstatistiksel yöntemlerle anomali tespiti
- **Kategori Bazlı Analiz**: Kategori seçimine göre özelleştirilmiş analiz
- **Strong Active Start**: Veri kalitesi için otomatik filtreleme

## 📦 Kurulum

### Gereksinimler
- Python 3.8+
- CUDA destekli GPU (opsiyonel, CPU'da da çalışır)

### Adımlar

1. **Repository'yi klonlayın:**
```bash
git clone <repository-url>
cd Customer_Voice
```

2. **Sanal ortam oluşturun (önerilir):**
```bash
python -m venv venv
venv\Scripts\activate  # Windows
# veya
source venv/bin/activate  # Linux/Mac
```

3. **Bağımlılıkları yükleyin:**
```bash
pip install -r requirements.txt
```

4. **Model dosyalarını kontrol edin:**
   - `bert_based_classification_models/` klasörü mevcut olmalı
   - `df_weigthed_final.pkl` veri dosyası mevcut olmalı

5. **Uygulamayı çalıştırın:**
```bash
streamlit run app.py
```

## 🌐 Streamlit Cloud'a Deploy Etme

1. **GitHub'a yükleyin:**
   - Repository'yi GitHub'a push edin
   - Büyük dosyalar (.pkl, model dosyaları) için Git LFS kullanın veya harici depolama kullanın

2. **Streamlit Cloud'a bağlayın:**
   - [streamlit.io](https://streamlit.io/cloud) adresine gidin
   - GitHub hesabınızla giriş yapın
   - Repository'yi seçin
   - Main file: `streamlit_app_v3.py`
   - Deploy edin!

## 📁 Proje Yapısı

```
Customer_Voice/
├── streamlit_app_v3.py          # Ana uygulama dosyası
├── requirements.txt               # Python bağımlılıkları
├── README.md                      # Bu dosya
├── bert_based_classification_models/      # BERT model dosyaları
│   ├── config.json
│   ├── model.safetensors
│   └── ...
├── df_weigthed_final.pkl         # Veri dosyası
└── .gitignore                    # Git ignore dosyası
```

## 🔧 Kullanım

### Şikayet Analizi
1. "🔍 Şikayet Analizi" sekmesine gidin
2. Şikayet başlığı ve metnini girin (başlık opsiyonel)
3. "Analiz et" butonuna tıklayın veya otomatik analiz bekleyin
4. Sonuçları inceleyin:
   - Sorumlu birim
   - Alt kategori
   - Churn skoru ve band
   - Tetiklenen kategoriler
   - Benzer şikayetler

### Dashboard
1. "📊 Dashboard" sekmesine gidin
2. Filtreleri kullanın:
   - Ana Kategori
   - Alt Kategori (ana kategori seçildiğinde otomatik filtrelenir)
   - Churn Band
   - Tarih Aralığı
3. Grafikleri ve KPI'ları inceleyin

### Zaman Serisi Analizi
1. "📈 Zaman Serisi" sekmesine gidin
2. Opsiyonel: Excel dosyası yükleyin (varsayılan veri kullanılır)
3. Kategori/Segment seçin
4. Tahmin veya anomali analizi butonlarına tıklayın

## 🎨 Özellikler

- **Dark Mode**: Modern, göz yormayan karanlık tema
- **Responsive Design**: Tüm ekran boyutlarına uyumlu
- **Interactive Charts**: Plotly ile interaktif grafikler
- **Real-time Analysis**: Anlık analiz ve tahmin
- **Advanced Filtering**: Gelişmiş filtreleme seçenekleri

## 📝 Notlar

- Model dosyaları büyük olduğu için Git LFS kullanılması önerilir
- İlk yükleme sırasında modeller indirileceği için biraz zaman alabilir
- GPU kullanımı performansı önemli ölçüde artırır

## 📄 Lisans

Bu proje özel kullanım içindir.

## 👤 Geliştirici

İbrahim Akdaş

## 🤝 Katkıda Bulunma

Katkılarınızı bekliyoruz! Lütfen pull request göndermeden önce değişikliklerinizi test edin.

