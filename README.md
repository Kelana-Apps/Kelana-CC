
# Kelana ML API

This API is built using Flask to optimize travel itineraries by combining Collaborative-Based Filtering (CBF) and Traveling Salesman Problem (TSP) algorithms. The project also utilizes Docker for containerization and is deployed on Google Cloud Run.

---

## **Features**
1. Recommends tourist destinations based on location, price category, and time slots (morning, afternoon, evening).
2. Optimizes travel routes using the Traveling Salesman Problem (TSP).
3. Deployment using Docker and Google Cloud Run.

---

## **Folder Structure**
```
.
├── app
│   ├── cbf.py             # File for Collaborative-Based Filtering
│   ├── tsp.py             # File for Traveling Salesman Problem
│   ├── routes.py          # Flask API Endpoints
│   ├── __init__.py        # Flask application initialization
│   ├── model.h5           # Machine Learning Model (CBF)
├── dataset
│   ├── tourismkelana_fixed.csv           # Dataset for CBF
├── Dockerfile             # Dockerfile for containerization
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
├── .dockerignore          # Files ignored by Docker
```

---

## **How to Run the Project**

### **Prerequisites**
- Python 3.8 or later
- Docker
- Google Cloud Platform (GCP) account with Cloud Run enabled

### **Steps to Run Locally**

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Kelana-Apps/Kelana-CC-ML-APIs.git
   cd Kelana-CC-ML-APIs
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Application**
   ```bash
   gunicorn --bind 0.0.0.0:8080 app.main:app
   ```

4. **Test the API Using Postman**
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
     ## **Response Example**

- Here is an example of the API response for the endpoint `POST /recommend`:
  ```json
{
  "selected_places": [
    {
      "day": "Day 1",
      "places": {
        "afternoon": {
          "Category": "Budaya",
          "Closing_Time": 15,
          "Description": "Gedung Joang '45 atau Museum Joang 45 adalah salah satu museum yang berada di Jakarta. Saat ini pengelolaannya dilaksanakan oleh Dinas Pariwisata dan Kebudayaan Provinsi DKI Jakarta. Museum ini terletak di Jalan Menteng Raya 31, Kelurahan Kebon Sirih, Kecamatan Menteng, Jakarta Pusat. Museum ini diresmikan pada tahun 1974 oleh Presiden Soeharto, setelah dilakukan renovasi.",
          "Lat": -6.1861838,
          "Long": 106.8364761,
          "Opening_Time": 9,
          "Place_Name": "Museum Joang 45",
          "Price": 2000,
          "Rating": 4.0
        },
        "evening": {
          "Category": "Taman Hiburan",
          "Closing_Time": 21,
          "Description": "Lapangan Banteng, dulu bernama Waterlooplein (bahasa Belanda: plein = lapangan) yaitu suatu lapangan yang terletak di Weltevreden, Batavia; tidak jauh dari Gereja Katedral Jakarta. Pada masa itu, Lapangan Banteng dikenal dengan sebutan Lapangan Singa karena di tengahnya terpancang tugu peringatan kemenangan pertempuran di Waterloo, dengan patung singa di atasnya.",
          "Lat": -6.170555,
          "Long": 106.8350378,
          "Opening_Time": 6,
          "Place_Name": "Taman Lapangan Banteng",
          "Price": 0,
          "Rating": 4.7
        },
        "morning": {
          "Category": "Taman Hiburan",
          "Closing_Time": 23,
          "Description": "Taman Menteng adalah sebuah taman yang berlokasi di kawasan Menteng, Jakarta Pusat. Taman ini berdiri di atas lahan seluas 2,9 hektar, dan memiliki koleksi 30 spesies tanaman yang berbeda.",
          "Lat": -6.1964087,
          "Long": 106.8293106,
          "Opening_Time": 0,
          "Place_Name": "Taman Menteng",
          "Price": 0,
          "Rating": 4.5
        }
      }
    },
    {
      "day": "Day 2",
      "places": {
        "afternoon": {
          "Category": "Taman Hiburan",
          "Closing_Time": 18,
          "Description": "Taman Suropati (awalnya bernama Burgemeester Bisschopplein) adalah nama sebuah taman di Jakarta. Taman ini merupakan pusat kawasan Menteng, berada tepat di antara pertemuan tiga jalan utama.",
          "Lat": -6.1994034,
          "Long": 106.8326228,
          "Opening_Time": 6,
          "Place_Name": "Taman Suropati",
          "Price": 0,
          "Rating": 4.6
        },
        "evening": {
          "Category": "Pusat Perbelanjaan",
          "Closing_Time": 23,
          "Description": "Pecenongan merupakan salah satu surga kuliner di Jakarta Pusat yang dikenal sejak zaman Jakarta masih bernama kota Batavia.",
          "Lat": -6.1667887,
          "Long": 106.8265261,
          "Opening_Time": 6,
          "Place_Name": "Wisata Kuliner Pecenongan",
          "Price": 0,
          "Rating": 5.0
        },
        "morning": {
          "Category": "Budaya",
          "Closing_Time": 15,
          "Description": "Museum Seni Rupa dan Keramik adalah sebuah museum di Jakarta, Indonesia. Museum ini didedikasikan untuk menampilkan seni rupa tradisional dan keramik Indonesia.",
          "Lat": -6.1342598,
          "Long": 106.814552,
          "Opening_Time": 9,
          "Place_Name": "Museum Seni Rupa dan Kramik",
          "Price": 5000,
          "Rating": 4.4
        }
      }
    }
  ]
}
```


---

### **Steps to Deploy on Google Cloud Run**

1. **Clone the Git Repository**
   ```bash
   git clone https://github.com/Kelana-Apps/Kelana-CC-ML-APIs.git
   cd Kelana-CC-ML-APIs
   ```

2. **Build the Docker Image**
   ```bash
   docker build -t ml-api-kelana .
   ```

3. **Run Docker Locally (Optional)**
   ```bash
   docker run -p 8080:8080 ml-api-kelana
   ```

4. **Deploy to Cloud Run**
   Use the GCP Cloud Run GUI to deploy, linking the repository directly to Cloud Run.

5. **Access the API**
   The application URL will be displayed after the deployment process is completed, e.g.,
   ```
   https://ml-api-kelana-fixed-738667113944.asia-southeast2.run.app
   ```

---
