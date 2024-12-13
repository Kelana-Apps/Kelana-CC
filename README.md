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
   git clone https://github.com/Kelana-Apps/Kelana-CC-ML-APIs.git
   cd Kelana-CC-ML-APIs
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Jalankan Aplikasi**
   ```bash
   gunicorn --bind  0.0.0.0:8080  app.main:app
   ```

4. **Uji API Menggunakan Postman**
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

1. **Clone Git Repository**
   ```bash
   git clone https://github.com/Kelana-Apps/Kelana-CC-ML-APIs.git
   cd Kelana-CC-ML-APIs
   ```
   
1. **Build Docker Image**
   ```bash
   docker build -t ml-api kelana .
   ```

2. **Run Docker Secara Lokal (Opsional)**
   ```bash
   docker run -p 8080:8080 ml-api-kelana
   ```
   ```

4. **Deploy ke Cloud Run**
   Deploy menggunakan GUI Cloud Run di GCP, menyambungkan langsung repository github dengan cloud run

5. **Akses API**
   URL aplikasi akan ditampilkan setelah proses deployment selesai, misalnya:
   ```
   https://ml-api-kelana-fixed-738667113944.asia-southeast2.run.app 
   ```

---
