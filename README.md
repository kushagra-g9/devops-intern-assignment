# 🚀 DevOps Assignment – Nginx Reverse Proxy with Docker Compose

This project demonstrates containerization of two backend services (Golang & Python Flask) behind a single Nginx reverse proxy using Docker Compose. All services run on a single exposed port (`8080`) and include health checks and logging.

---

## 📁 Project Structure

.
├── docker-compose.yml
├── nginx
│ ├── Dockerfile
│ └── nginx.conf
├── service_1
│ ├── Dockerfile
├── service_2
│ ├── Dockerfile
└── README.md


---

## ⚙️ Technologies Used

- Golang
- Python (Flask)
- Nginx (Reverse Proxy)
- Docker & Docker Compose
- Custom logging
- Healthchecks

---

## 🛠️ Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/kushagra-g9/devops-intern-assignment.git
cd devops-intern-assignment
2. Run the system
bash
Copy
Edit
docker-compose up --build
This will build and start:

service1 (Golang app on port 8001)

service2 (Python Flask app on port 8002)

nginx (reverse proxy on port 8080)

🌐 Available Endpoints
Route	Description
/service1/ping	Health check for service 1
/service1/hello	Hello message from service 1
/service2/ping	Health check for service 2
/service2/hello	Hello message from service 2

Access them via:

http://localhost:8080/service1/ping

http://localhost:8080/service2/hello

🔀 Nginx Reverse Proxy
Nginx is configured to:

Listen on port 80 (mapped to 8080)

Forward /service1/* to the Golang backend

Forward /service2/* to the Flask backend

Log all incoming requests with timestamp and path

Example from nginx.conf:

nginx
Copy
Edit
location /service1/ {
    proxy_pass http://service1:8001/;
}

location /service2/ {
    proxy_pass http://service2:8002/;
}
❤️ Bonus Features
✅ Healthchecks for both services
✅ Custom access log format in Nginx
✅ Modular Dockerfile setup
✅ Single-command boot via docker-compose up --build