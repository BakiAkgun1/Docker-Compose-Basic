# 🚀 Dockerized Multi-App Projects

This repository contains 4 different Docker Compose-powered applications:

1. **Simple Node.js Server**
2. **Todo App + MongoDB**
3. **WordPress Blog + MySQL**
4. **Flask File Uploader App**

Each app is located in its own directory and can be run independently.

---

## 📁 Project Structure

```
├── 1-docker-compose-app/  → Simple Node.js server
├── 2-todo-app/           → Todo app with MongoDB
├── 3-wordpress/          → WordPress blog system
└── 4-uploader-app/       → Flask-based file uploader
```

---

## 🧱 1. Simple Node.js Server (`1-docker-compose-app/`)

### 📄 Description
A basic Node.js HTTP server that returns a greeting message when accessed.

### 🐳 docker-compose.yml
```yaml
version: "3.4"
services:
  node-server:
    build: .
    ports:
      - "3001:3000"
```

### 🚀 Run
```bash
cd 1-docker-compose-app
docker-compose up --build
```

📍 **App runs at:** http://localhost:3001

---

## 📋 2. Todo App with MongoDB (`2-todo-app/`)

### 📄 Description
A todo application with MongoDB database backend for data persistence.

### 🐳 docker-compose.yml
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

### 🚀 Run
```bash
cd 2-todo-app
docker-compose up --build
```

📍 **App runs at:** http://localhost:3000

---

## 📝 3. WordPress Blog (`3-wordpress/`)

### 📄 Description
A complete WordPress blog setup with MySQL database backend.

### 🐳 docker-compose.yml
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

### 🚀 Run
```bash
cd 3-wordpress
docker-compose up -d
```

📍 **Access WordPress at:** http://localhost:8080

---

## 📤 4. Flask File Uploader App (`4-uploader-app/`)

### 📄 Description
A simple Flask web app that allows users to upload files, which are stored in a Docker volume (`uploads/`).

### 📦 Project Structure
```
4-uploader-app/
├── app/
│   ├── app.py
│   └── templates/
│       └── index.html
├── uploads/              # Volume-mounted directory
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

### 🐳 docker-compose.yml
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

### 🚀 Run
```bash
cd 4-uploader-app
docker-compose up --build
```

📍 **App runs at:** http://localhost:5000  
📁 **Uploaded files are saved to the `uploads/` directory.**

---

## ✅ Prerequisites

- Docker
- Docker Compose
- Git (optional)

## 📂 Getting Started

### Clone the Repository
```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### Running Applications
Each app can be launched from its folder using:

```bash
docker-compose up --build
```

### Common Commands
```bash
# Run in background (detached mode)
docker-compose up -d --build

# Stop running containers
docker-compose down

# Remove volumes and clean up
docker-compose down -v

# View logs
docker-compose logs -f
```



## 📝 License

This project is open source and available under the MIT License.

