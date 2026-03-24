# Akademik Tez Sınıflandırma: Geleneksel vs. Derin Öğrenme Karşılaştırması

Bu proje, akademik tezlerin kategorilerini **ham metin verisi** üzerinden tahmin etmek amacıyla geliştirilmiştir. Proje, veri toplama (OCR), veri mühendisliği ve geniş kapsamlı bir model kıyaslamasını (Benchmarking) içerir.

---

### Projenin Öne Çıkan Özellikleri

* **Uçtan Uca Veri Hattı:** Google Drive üzerindeki PDF'lerden `pdfplumber` ve `Tesseract OCR` ile otomatik metin çıkarımı.
* **Zero Preprocessing Challenge:** Metin temizliği (stop-words, stemming vb.) yapılmadan ham veriyle eğitim.
* **Zorlayıcı Kategoriler:** Birbirine terminolojik olarak çok yakın 5 farklı bilim dalı (Fizik, Kimya, Biyokimya, Dahiliye, Eczacılık).
* **Kapsamlı Model Yelpazesi:** Klasik Makine Öğrenmesi (ML) ve modern Derin Öğrenme (DL) mimarilerinin performans kıyaslaması.

---

### Model Performans Karşılaştırması (Benchmark)

Deneyler sonucunda, TF-IDF ile beslenen klasik modellerin bu veri seti üzerinde derin öğrenme modellerinden daha yüksek başarı sergilediği gözlemlenmiştir.

| Model | Accuracy (%) | Tip | Eğitim Süresi |
| :--- | :---: | :--- | :---: |
| **Random Forest** | **%92.52** | **Klasik ML** | 1.38 sn |
| **SVM (Linear)** | **%90.65** | **Klasik ML** | 4.19 sn |
| **Logistic Regression** | **%86.92** | **Klasik ML** | 0.62 sn |
| **Naive Bayes** | **%85.98** | **Klasik ML** | 0.01 sn |
| **Bidirectional LSTM** | **%76.64** | **Derin Öğrenme** | ~25 sn |
| **BERTurk (Transformer)** | **%72.90** | **Fine-tuned** | ~120 sn |

---

### Kritik Çıkarımlar

1.  **Klasik Modellerin Dominansı:** Küçük veri setlerinde (534 kayıt) TF-IDF + Random Forest kombinasyonunun, karmaşık derin öğrenme mimarilerine göre çok daha güçlü genelleme yaptığı kanıtlanmıştır.
2.  **Kategori Bazlı Analiz:**
    * **Fizik:** Tüm modellerde %100 başarıya ulaşarak en ayırt edici kategori olmuştur.
    * **Dahiliye:** Tıp terminolojisinin gücü sayesinde klasik modellerde %90+ recall başarısı yakalamıştır.
    * **Biyokimya vs Kimya:** En zorlayıcı ayrım bu noktada yaşanmış olsa da Random Forest %90 recall ile bu zorluğun üstesinden gelmiştir.
3.  **Hız ve Verimlilik:** Naive Bayes 0.01 saniye gibi rekor bir sürede %86 başarı sağlayarak maliyet/performans dengesinde öne çıkmıştır.

---

### Kurulum ve Kullanım

Proje Google Colab ortamında geliştirilmiştir. Gerekli tüm bağımlılıklar:

```bash
pip install pdfplumber pytesseract transformers torch pandas scikit-learn matplotlib seaborn
apt-get install tesseract-ocr-tur
