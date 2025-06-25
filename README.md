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

# LOGS
PS C:\Users\gupta\Downloads\Assignment> docker-compose logs
service2-1  | Downloading cpython-3.13.5-linux-x86_64-gnu (download) (33.8MiB)
service2-1  |  Downloading cpython-3.13.5-linux-x86_64-gnu (download)
service2-1  | Using CPython 3.13.5
service2-1  | Creating virtual environment at: .venv
service2-1  | Installed 7 packages in 5ms
service2-1  |  * Serving Flask app 'app'
service2-1  |  * Debug mode: off
service2-1  | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead. 
service2-1  |  * Running on all addresses (0.0.0.0)
service2-1  |  * Running on http://127.0.0.1:8002
service2-1  |  * Running on http://172.18.0.3:8002
service2-1  | Press CTRL+C to quit
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:54:34] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:54:44] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:54:54] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:05] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:15] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:25] "GET /ping HTTP/1.1" 200 -
service2-1  | 172.18.0.4 - - [25/Jun/2025 12:55:30] "GET /hello HTTP/1.0" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:36] "GET /ping HTTP/1.1" 200 -
service2-1  | 172.18.0.4 - - [25/Jun/2025 12:55:37] "GET /ping HTTP/1.0" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:46] "GET /ping HTTP/1.1" 200 -
service1-1  | 2025/06/25 12:54:13 Service 1 listening on port 8001...
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:55:56] "GET /ping HTTP/1.1" 200 -
service2-1  | 127.0.0.1 - - [25/Jun/2025 12:56:09] "GET /ping HTTP/1.1" 200 -
nginx-1     | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
nginx-1     | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
nginx-1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
nginx-1     | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
nginx-1     | 10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
nginx-1     | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
nginx-1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
nginx-1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
nginx-1     | /docker-entrypoint.sh: Configuration complete; ready for start up
nginx-1     | 2025-06-25T12:55:16+00:00 [172.18.0.1] "GET /service1/ping HTTP/1.1"
nginx-1     | 2025-06-25T12:55:25+00:00 [172.18.0.1] "GET /service1/hello HTTP/1.1"
nginx-1     | 2025-06-25T12:55:30+00:00 [172.18.0.1] "GET /service2/hello HTTP/1.1"
nginx-1     | 2025-06-25T12:55:37+00:00 [172.18.0.1] "GET /service2/ping HTTP/1.1"
PS C:\Users\gupta\Downloads\Assignment> docker-compose down
❤️ Bonus Features
✅ Healthchecks for both services
✅ Custom access log format in Nginx
✅ Modular Dockerfile setup
✅ Single-command boot via docker-compose up --build
