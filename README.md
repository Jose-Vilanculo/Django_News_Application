# Django News Application

A Django-based news platform for independent journalism and curated publications. Supports **role-based permissions**, article and newsletter publishing, subscriptions, and integrations with **email** and **X (Twitter)**.

## 📌 Features

- **Custom user roles**: Reader, Journalist, Editor
- **Reader subscriptions** to journalists or publishers
- **Journalist publishing**: articles & newsletters (independent or under a publisher)
- **Editor review** & approval workflow
- **Automatic email & X (Twitter) posting** for approved articles
- **REST API** for article retrieval
- **Responsive frontend** (Bootstrap)
- **SQL** database backend
- **Unit tests** included

## 🚀 Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Jose-Vilanculo/News_Application_Consolidation.git.git
cd django-news-app
```

### 2. Create & Activate Virtual Environment
```bash
python -m venv vir-env
```
- **Windows**:  
  ```bash
  vir-env\Scripts\activate
  ```
- **macOS/Linux**:  
  ```bash
  source vir-env/bin/activate
  ```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

## 🗄️ MYSQL Setup

1. **Install MYSQL** → [Download](https://www.mysql.com/downloads/)  
2. **Create Database & User**:
   ```sql
   CREATE DATABASE news_app CHARACTER SET utf8mb4;
   CREATE USER 'your_user'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON news_app.* TO 'your_user'@'localhost';
   FLUSH PRIVILEGES;
   ```
**Create a .env file and add your DB Variables**
  DB_NAME=your_db_name
  DB_USER=your_db_user
  DB_PASSWORD=your_db_password
  DB_HOST=your_db_host
  DB_PORT=your_db_port
  --NB!! Add .env to your .gitignore

3. **Configure `settings.py`**:
   ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': os.environ.get('DB_NAME'),
          'USER': os.environ.get('DB_USER'),
          'PASSWORD': os.environ.get('DB_PASSWORD'),
          'HOST': os.environ.get('DB_HOST'),
          'PORT': os.environ.get('DB_PORT'),
          'OPTIONS': {
              'charset': 'utf8mb4',
          },
      }
  }
   ```
4. **Install MySQL client**:
   ```bash
   pip install mysqlclient
   ```

## 📧 Email Configuration

In `settings.py`:
```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.yourprovider.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'your_email@example.com'
EMAIL_HOST_PASSWORD = 'your_app_password'
DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
```
> ⚠️ Keep credentials out of version control. Use environment variables.

## 🐦 Twitter Integration

In `settings.py`:
```python
TWITTER_API_KEY = 'your-api-key'
TWITTER_API_SECRET = 'your-api-secret'
TWITTER_ACCESS_TOKEN = 'your-access-token'
TWITTER_ACCESS_SECRET = 'your-access-secret'
```
> Obtain keys from the [Twitter Developer Portal](https://developer.twitter.com/). Secrets must **never** be committed.

## 🐳 Docker Setup

**`Dockerfile`**
- Uses `python:3.11-slim`
- Installs dependencies + MYSQL client libs
- Copies code to `/app` and exposes port `8000`

**`docker-compose.yml`**
- **db** service → MYSQL
- **web** service → Django app
- Environment variables loaded from `.env`:
  ```env
  DB_NAME=your_db_name
  DB_USER=your_db_user
  DB_PASSWORD=your_db_password
  DB_HOST=your_db_host
  DB_PORT=your_db_port
  ```

Run:
```bash
docker-compose up --build
```
USE: 8000:8000 port

## ▶️ Running Locally (Non-Docker)
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```
Visit: **http://localhost:8000/**

## 🧪 Testing
```bash
python manage.py test
```

## 📡 REST API
- Get subscribed articles:  
  `GET /api/articles/`
- Use tools like Postman for authentication & queries.

## Live Site Link:
- **https://djangonewsapplication-production.up.railway.app/**

## 📝 Notes
- Journalists can select a publisher when creating content.
- Readers see **only approved** articles.
- `.gitignore` should exclude `.env` and other secret files.
