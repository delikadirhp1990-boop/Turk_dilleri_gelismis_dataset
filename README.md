# Türk Dilleri Dil Verisi Yönetim Sistemi (Masaüstü Uygulaması)

Bu proje; Türkçe başta olmak üzere Kazakça, Özbekçe, Türkmence gibi çağdaş Türk dillerine ait dil bilgisi, etimoloji, sözdizimi, fonetik ve söz varlığı verilerini **yapay zekâ destekli** olarak yönetmek için geliştirilmiş **cross‑platform** bir sistemdir.

---

## 🚀 Özellikler

- 📋 **Kapsamlı Veri Modeli:** Dil bilgisi özellikleri, AI eğitim verisi, senkronizasyon alanlarını içeren esnek JSON yapısı.
- 💻 **PyQt5 Masaüstü Uygulaması:**
  - Canlı arama, kategori / etiket / tarih filtreleme
  - Dinamik içerik alanları (kullanıcı istediği kadar alan ekleyebilir)
  - JSON önizleme paneli
  - İçe / dışa aktarma (JSON)
  - Koyu / açık tema desteği
- 📱 **Android Uygulaması (Kotlin + Jetpack Compose):**
  - Firebase Authentication ile güvenli giriş
  - Kayıt ekleme, düzenleme, silme
  - Canlı arama ve detaylı JSON görüntüleme
  - Offline‑first kullanım (Firestore çevrimdışı veri desteği)
- ☁️ **Firebase Firestore Entegrasyonu:**
  - Masaüstü ↔ Android arasında anlık veri senkronizasyonu
  - Çatışma çözümü (`last_write_wins`)
  - Toplu içe / dışa aktarma (JSON ↔ Firestore)
- 🤖 **Yapay Zekâ Modülü:**
  - Dil bilgisi özellik tespiti (ünlü düşmesi, ünsüz yumuşaması, büyük ünlü uyumu)
  - Otomatik etiketleme
  - Sentence‑Transformers ile anlamsal arama (semantic search)
  - Embedding vektörlerinin hesaplanması ve saklanması
- 📊 **İstatistik Paneli:** Toplam kayıt, dil dağılımı, kategori yoğunluğu, en çok kullanılan etiketler.

---

## 🧱 Mimari
[Android App] ←─ Firestore ──→ [Python Desktop App]
│ │
└────→ AI Backend (FastAPI) ←──┘

text

- **Desktop (`PyQt5`)** – Tam yönetim, toplu işlem, AI analizleri.
- **Android (`Kotlin + Compose`)** – Hızlı veri girişi, mobil erişim.
- **AI Backend (`FastAPI`)** – Dil bilgisi analizi, embedding, semantik arama.
- **Firebase Firestore** – Merkezi bulut veritabanı.

---

## 📦 Kullanılan Teknolojiler

| Katman          | Teknolojiler                                       |
|-----------------|----------------------------------------------------|
| Masaüstü        | Python 3.12, PyQt5, Firebase Admin SDK, Requests   |
| Android         | Kotlin, Jetpack Compose, Firebase Auth & Firestore |
| AI Backend      | FastAPI, Sentence‑Transformers, NumPy              |
| Veritabanı      | Firebase Firestore, Local JSON                     |
| Ek Kütüphaneler | Gson (Android), Uvicorn (Backend)                  |

---

## ⚙️ Kurulum

### 1. Depoyu Klonlayın
```bash
git clone https://github.com/kullanici/turk-dilleri-dil-sistemi.git
cd turk-dilleri-dil-sistemi
2. Masaüstü Uygulaması (Python)
bash
cd desktop
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
Firebase bağlantısı için:

Firebase Console → Proje Ayarları → Servis Hesapları → Yeni Özel Anahtar Oluştur.

İndirilen dosyayı desktop/firebase-key.json olarak kaydedin.

Aynı dizinde firebase_config.json oluşturup aşağıdaki içeriği yazın:

json
{
  "serviceAccountKeyPath": "firebase-key.json",
  "databaseURL": ""
}
Uygulamayı başlatın:

bash
python main.py
Uygulama her zaman koyu tema ile açılır. Görünüm menüsünden değiştirebilirsiniz.

3. AI Backend (Opsiyonel)
bash
cd backend
pip install -r requirements.txt
python main.py
Servis http://localhost:8000 adresinde çalışır. Masaüstü uygulaması otomatik bağlanır.

4. Android Uygulaması
Android Studio ile android/ klasörünü açın.

Firebase Console’dan indireceğiniz google-services.json dosyasını app/ dizinine koyun.

Build → Run (gerçek cihaz veya emülatör).

📖 Kullanım
Yeni Kayıt Ekle: Sağ paneldeki formu doldurun ve Kaydet butonuna tıklayın.

Arama / Filtreleme: Araç çubuğundaki arama kutusuna metin yazın, sol panelden dil/kategori seçin.

Firebase Senkronizasyonu:

☁️ Gönder: Yerel veriyi Firestore’a yollar.

☁️ Çek: Firestore’daki veriyi yerel JSON ile değiştirir.

🗑️ Firebase'den Sil: Seçili kayıt(ları) hem Firestore hem de (istenirse) yerel depodan siler.

AI Analizi: Bir kaydı seçin, Dil Bilgisi Analizi veya Otomatik Etiketle butonuna basın.

Semantik Arama: Semantik Arama butonuna tıklayıp bir sorgu girin; anlam benzerliğine göre sıralanmış sonuçları görün.

Tema Değiştirme: Görünüm menüsünden Açık/Koyu tema arasında geçiş yapın.
