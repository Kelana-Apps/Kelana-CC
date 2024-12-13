# Kelana ML API

API ini dibuat menggunakan Flask untuk mengoptimalkan itinerary perjalanan, mengombinasikan algoritma Collaborative-Based Filtering (CBF) dan Traveling Salesman Problem (TSP). Proyek ini juga menggunakan Docker untuk containerization dan dideploy di Google Cloud Run.

---

## **Fitur**
1. Rekomendasi tempat wisata berdasarkan lokasi, kategori harga, dan slot waktu (morning, afternoon, evening).
2. Optimasi rute perjalanan menggunakan TSP.
3. Deployment menggunakan Docker dan Google Cloud Run.

---

## **Folder Structure**
```
.
├── app
│   ├── cbf.py             # File untuk Collaborative-Based Filtering
│   ├── tsp.py             # File untuk Traveling Salesman Problem
│   ├── routes.py          # Endpoint Flask API
│   ├── __init__.py        # Inisialisasi aplikasi Flask
│   ├── model.h5           # Model Machine Learning (CBF)
├── dataset
│   ├── tourismkelana_fixed.csv           # Dataset untuk CBF
├── Dockerfile             # Dockerfile untuk containerization
├── requirements.txt       # Dependencies Python
├── README.md              # Dokumentasi proyek
├── .dockerignore          # File yang diabaikan oleh Docker
```

---

## **Cara Menjalankan Proyek**

### **Prasyarat**
- Python 3.8 atau lebih baru
- Docker
- Akun Google Cloud Platform (GCP) dengan Cloud Run diaktifkan

### **Langkah-langkah Menjalankan Lokally**

1. **Clone Repositori**
   ```bash
   git clone https://github.com/username/repo-name.git
   cd repo-name
   ```

2. **Setup Lingkungan Virtual**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate   # Windows
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Jalankan Aplikasi**
   ```bash
   export FLASK_APP=app  # Linux/Mac
   set FLASK_APP=app     # Windows
   flask run
   ```
   Aplikasi akan berjalan di `http://127.0.0.1:5000`.

5. **Uji API Menggunakan Postman**
   - Endpoint: `POST /recommend`
   - Payload:
     ```json
     {
       "city": "Jakarta",
       "start_date": "01-01-2024",
       "end_date": "03-01-2024",
       "price_category": "Medium"
     }
     ```

---

### **Langkah-langkah Deploy ke Google Cloud Run**

1. **Build Docker Image**
   ```bash
   docker build -t itinerary-optimization-api .
   ```

2. **Run Docker Secara Lokal (Opsional)**
   ```bash
   docker run -p 8080:8080 itinerary-optimization-api
   ```
   Aplikasi dapat diakses di `http://127.0.0.1:8080`.

3. **Tag dan Push Docker Image ke Google Container Registry (GCR)**
   ```bash
   docker tag itinerary-optimization-api gcr.io/<PROJECT_ID>/itinerary-optimization-api
   docker push gcr.io/<PROJECT_ID>/itinerary-optimization-api
   ```

4. **Deploy ke Cloud Run**
   ```bash
   gcloud run deploy itinerary-optimization-api \
       --image gcr.io/<PROJECT_ID>/itinerary-optimization-api \
       --platform managed \
       --region <REGION> \
       --allow-unauthenticated
   ```
   Replace `<PROJECT_ID>` dengan ID Proyek Google Cloud Anda dan `<REGION>` dengan wilayah Cloud Run (misalnya `us-west1`).

5. **Akses API**
   URL aplikasi akan ditampilkan setelah proses deployment selesai, misalnya:
   ```
   https://ml-api-kelana-fixed-738667113944.asia-southeast2.run.app 
   ```

---
