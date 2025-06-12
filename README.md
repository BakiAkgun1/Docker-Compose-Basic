# Docker Compose Applications Collection

A collection of ready-to-use Docker Compose applications for learning and development purposes.

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Applications](#applications)
  - [1. Basic Web App](#1-basic-web-app)
  - [2. Todo App with MongoDB](#2-todo-app-with-mongodb)
  - [3. WordPress Blog](#3-wordpress-blog)
  - [4. Flask File Uploader](#4-flask-file-uploader)
- [Getting Started](#getting-started)
- [Usage](#usage)

## ✅ Prerequisites

Before running these applications, make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Git (optional, for cloning the repository)

## 🚀 Applications

### 1. Basic Web App (`1-docker-compose-app/`)

A simple web application demonstrating basic Docker Compose setup.

**Docker Compose Configuration:**
```yaml
version: "3.4"
services:
  web-app:
    container_name: dc-web-app
    build: .
    ports:
      - "3001:3001"
```

**Run the application:**
```bash
cd 1-docker-compose-app
docker-compose up --build
```

📍 **Access:** http://localhost:3001

---

### 2. Todo App with MongoDB (`2-todo-app/`)

A todo application with MongoDB database backend.

**Docker Compose Configuration:**
```yaml
version: "3.4"
services:
  todo-app:
    container_name: dc-todo-app
    build: .
    ports:
      - "3000:3000"
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - todo-app-data:/data/db

volumes:
  todo-app-data:
```

**Run the application:**
```bash
cd 2-todo-app
docker-compose up --build
```

📍 **Access:** http://localhost:3000

---

### 3. WordPress Blog (`3-wordpress/`)

A complete WordPress blog setup with MySQL database.

**Docker Compose Configuration:**
```yaml
version: "3.8"
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: blogdb
      MYSQL_USER: bloguser
      MYSQL_PASSWORD: test123
      MYSQL_RANDOM_ROOT_PASSWORD: "1"
    volumes:
      - db:/var/lib/mysql
  
  wordpress:
    image: wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: bloguser
      WORDPRESS_DB_PASSWORD: test123
      WORDPRESS_DB_NAME: blogdb
    volumes:
      - wordpress:/var/www/html

volumes:
  db:
  wordpress:
```

**Run the application:**
```bash
cd 3-wordpress
docker-compose up -d
```

📍 **Access:** http://localhost:8080

---

### 4. Flask File Uploader (`4-uploader-app/`)

A Flask web application that allows users to upload files, stored in a Docker volume.

**Project Structure:**
```
4-uploader-app/
├── app/
│   ├── app.py
│   └── templates/
│       └── index.html
├── uploads/          # Volume-mounted directory
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

**Docker Compose Configuration:**
```yaml
version: '3.8'
services:
  uploader:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./uploads:/uploads
```

**Run the application:**
```bash
cd 4-uploader-app
docker-compose up --build
```

📍 **Access:** http://localhost:5000  
📁 **File Storage:** Uploaded files are saved to the `uploads/` directory

## 🏁 Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/docker-compose-apps.git
   cd docker-compose-apps
   ```

2. **Navigate to any application directory:**
   ```bash
   cd [app-directory-name]
   ```

3. **Run the application:**
   ```bash
   docker-compose up --build
   ```

## 💡 Usage

Each application can be launched independently from its respective folder using:

```bash
docker-compose up --build
```

To run applications in the background (detached mode):
```bash
docker-compose up -d --build
```

To stop running applications:
```bash
docker-compose down
```

To remove volumes and clean up:
```bash
docker-compose down -v
```



## 📝 License

This project is open source and available under the [MIT License](LICENSE).

