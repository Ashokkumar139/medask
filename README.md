# Medask

Medask is a Django-based medical document processing and query system. Users can **upload medical-related documents** and **ask queries** in various medical categories such as **Cardiology, Respiratory, and Diabetes**. The application integrates **Celery** for background processing and **WebSockets** for real-time chat.

---

## 🚀 Features
- **Medical Document Upload** (PDF, Word, Images, etc.)
- **Query Processing on Uploaded Documents**
- **Categorized Medical Queries** (Cardiology, Respiratory, Diabetes)
- **Background Task Processing** using Celery
- **Real-time WebSocket Chat** for Query Handling
- **PostgreSQL Database** for Data Storage
- **AWS S3 for File Storage (Production)**
- **JWT-based Authentication**
- **Redis for Message Queue & Caching**

---

## 🛠️ Tech Stack
- **Programming Language**: Python 3.10
- **Backend**: Django, Django REST Framework (DRF)
- **Database**: PostgreSQL
- **Storage**: AWS S3 (Production), Local File System (Development)
- **Task Queue**: Celery + Redis
- **Real-time Communication**: Django Channels & WebSockets
- **AI Query Processing**: OpenAI Integration
- **SMS Services**: Fast2SMS, MSG91, Twilio

---

## 📂 Project Structure
```
Medask/
│── accounts/          # User authentication & management
│── chats/             # WebSocket real-time chat handling
│── documents/         # Document management & processing
│── templates/         # HTML templates (if applicable)
│── static/            # Static files (CSS, JS, Images)
│── media/             # Uploaded documents (local storage for development)
│── .env               # Environment variables
│── manage.py          # Django entry point
│── requirements.txt   # Project dependencies
│── README.md          # Project documentation

```

---

## 📌 Installation & Setup

## 🔗 API Documentation
[Postman API Documentation](https://documenter.getpostman.com/view/39925071/2sAYdio9jF)

### **1️⃣ Clone the Repository**

```
git@github.com:MindMapInnovation-Projects/MedAsk.git
cd medask
```


### **1️⃣ Create a Virtual Environment**
```
python3 -m venv venv
source venv/bin/activate
```


### ** 3️⃣ Install Dependencies **
```
pip install -r requirements.txt
```

### ** 4️⃣ Configure Environment Variables **
Create a .env file and add the following:

```
SECRET_KEY="your-secret-key"
DEBUG=True
DB_ENGINE=django.db.backends.postgresql
DB_NAME=medask_db 
DB_USER=postgres 
DB_PASSWORD=root
DB_HOST=localhost
DB_PORT=5432  

# AWS Configuration (For production storage)
AWS_ACCESS_KEY_ID = 'your-access-key'
AWS_SECRET_ACCESS_KEY = 'your-secret-key'
AWS_STORAGE_BUCKET_NAME = 'your-bucket-name'
AWS_S3_REGION_NAME = 'your-region'

# Redis & Celery Configuration
CELERY_BROKER_URL = 'redis://localhost:6379/0'
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'

# ==== QUADRENT CONFIGURATION ====

docker pull qdrant/qdrant

docker run -p 6333:6333 -p 6334:6334 \
    -v "$(pwd)/qdrant_storage:/qdrant/storage:z" \
    qdrant/qdrant


QUADRENT_HOST="http://localhost"
QUADRENT_PORT="6333"
VECTOR_ROOT_DIR = "vectors/"

# ==== IMAGE URL CONFIG ======
DOMAIN="http://127.0.0.1:8000"

# ==== Cache CONFIGURATION =====
LOCATION="redis://localhost:6379/1"



```

### ** 5️⃣ Apply Database Migrations **
```
python manage.py makemigrations
python manage.py migrate
```

### ** 6️⃣ Create a Superuser (For Admin Access) **
```
python manage.py createsuperuser
```

---

### ** 7️⃣ Run the Development Server **
```
python manage.py runserver
```

### *** 8️⃣ Start Celery Worker **
```
celery -A Medask worker --loglevel=info
```

### *** 9 Setup vectors and media directories**
```
Medask/
│── media/ 
      │── cardiology
      │── diabetes
      │── respiratory           
│── vectors/
      │── cardiology
      │── diabetes
      │── respiratory  
``` 


### *** 10 Setup Quadrent vector DB **

```
docker pull qdrant/qdrant

```

``` 
docker run -d -p 6333:6333 \
    -v $(pwd)/path/to/data:/qdrant/storage \
    qdrant/qdrant
```

```
python manage.py quadrentdb --mode=create
```

### *** 11 Setup Image reference **
```
python manage.py loadpdfs
```

## 🗂️ Dependencies (requirements.txt)
```
aiofiles==24.1.0
aiohttp==3.9.2
asgiref==3.8.1
anyio==4.8.0
boto3==1.36.24
bs4==0.0.2
celery==5.4.0
channels==4.2.0
channels_redis==4.2.1
daphne==4.1.2
Django==5.0.1
django-cors-headers==4.3.0
django-redis==5.4.0
djangorestframework==3.14.0
djangorestframework-simplejwt==5.2.1
django-storages==1.14.5
groq==0.18.0
python-decouple==3.7
python-docx== 1.1.2
pymupdf==1.24.11
pymupdf4llm==0.0.17
pdf2image==1.17.0
openai==1.58.1
psycopg2-binary==2.9.10
python-magic==0.4.27
phonenumbers==8.13.55
qdrant-client==1.13.2
redis==5.2.1
requests==2.32.3
twilio==9.4.6

```
