# Tez Konuları Sınıflandırma Projesi: Geleneksel ve Derin Öğrenme Yaklaşımları

Bu proje, akademik tez metinlerinden yola çıkarak tezlerin ait olduğu bilimsel kategorileri tahmin etmeyi amaçlar. Veri seti, Google Drive üzerindeki PDF formatındaki tezlerden **pdfplumber** ve **Tesseract OCR** kullanılarak otomatik olarak oluşturulmuştur.

---

### Projenin Öne Çıkan Özellikleri

* **Özgün Veri Seti:** Veri seti, çeşitli akademik kategorilerdeki (Fizik, Kimya, Biyokimya, Dahiliye, Eczacılık) tezlerin PDF dosyalarından metin madenciliği yöntemleriyle bizzat tarafımdan derlenmiştir.
* **Zorlayıcı Senaryo:** Kategoriler, modelin ayırt ediciliğini test etmek amacıyla birbirine **terminolojik olarak çok yakın** akademik alanlardan seçilmiştir.
* **Ham Veri ile Eğitim:** Modeller, metin temizleme (stop-words, stemming vb.) işlemleri yapılmadan, **ham metin verisi** ile eğitilerek modellerin karmaşık metin yapılarındaki doğal başarımı ölçülmüştür.
* **Geniş Model Yelpazesi:** Klasik ML (Logistic Regression, SVM, RF, Naive Bayes) ile Derin Öğrenme (Bi-LSTM ve BERTurk) modelleri kıyaslanmıştır.

---

### Kullanılan Modeller ve Metodoloji

1.  **Metin Çıkarımı:** PDF dosyalarından metinler okunmuş, metin içermeyen veya taranmış sayfalar için **OCR (Optik Karakter Tanıma)** uygulanmıştır.
2.  **Vektörizasyon:** Klasik modeller için **TF-IDF (1,2 n-gram)**, derin öğrenme için **Tokenizer** ve **Transformer-based** gömme (embeddings) kullanılmıştır.
3.  **Modeller:**
    * **Klasik ML:** Logistic Regression (Hiperparametre optimizasyonu yapılmıştır), SVM, Random Forest, Naive Bayes.
    * **Derin Öğrenme:** Bidirectional LSTM (RNN tabanlı).
    * **Transfer Learning:** **BERTurk** (*dbmdz/bert-base-turkish-cased*) kullanılarak ince ayar (fine-tuning) yapılmıştır.

---

### Elde Edilen Sonuçlar

Yapılan testler sonucunda modellerin başarı oranları (Accuracy) aşağıda özetlenmiştir:

| Model | Accuracy (%) | Tip |
| :--- | :---: | :--- |
| **Bidirectional LSTM** | **%76.64** | **Derin Öğrenme** |
| **BERTurk (Transformer)** | **%72.90** | **Transfer Learning** |
| **Logistic Regression** | **%70.00+** | **Klasik ML** |
| **SVM (Linear)** | **%70.00+** | **Klasik ML** |

> **Not:** Sonuçlar, verilerin temizlenmemiş ham haliyle elde edilmesine rağmen oldukça yüksek başarım sergilemiştir. Bu durum, modellerin özellikle akademik dildeki karmaşık bağlamları anlama yeteneğini kanıtlamaktadır.

---

### Kurulum ve Kullanım

Proje Google Colab ortamında geliştirilmiştir. Gerekli kütüphaneleri yüklemek için terminale veya notebook hücresine aşağıdaki komutları yazabilirsiniz:

```bash
pip install pdfplumber pytesseract transformers torch pandas scikit-learn matplotlib seaborn
apt-get install tesseract-ocr-tur
