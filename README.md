# docker_multi_container
# Hands-On L3: Installing Docker & Building a Multi-Container Microservice  
**Course:** ITCS 6190/8190 – Fall 2025  
**Instructor:** Marco Vieira  
**Student:** Atluri Sasi Vadana

# 🚀 Docker Multi-Container Project

This project demonstrates running a simple **Flask application** with a **Redis counter** and a **Postgres database** using **Docker Compose**.

---

## 📂 Project Structure

├── app.py              # Flask app (with Redis counter + /health endpoint)
├── requirements.txt    # Python dependencies
├── Dockerfile          # Flask service image (using Gunicorn in production)
├── compose.yaml        # Docker Compose for web + Redis + Postgres
├── .dockerignore       # Files ignored in Docker builds
├── README.md           # Project documentation
└── screenshots/        # Screenshots of setup and output

---

## 🛠️ Prerequisites

- Docker Desktop (with WSL2 backend on Windows if applicable)
- Git

---

## ⚡ Quick Start

### Using Docker Compose (recommended)

1. Clone the repository:
   git clone https://github.com/sasi703/docker_multi_container.git
   cd docker_multi_container

2. Create .env file with Postgres password:
   echo "POSTGRES_PASSWORD=pass12345" > .env

3. Build and start all containers:
   docker compose up --build

4. Access the application in the browser:
   http://localhost:8000

5. Check service health:
   curl http://localhost:8000/health

---

### Using Docker Run (manual alternative)

If you prefer not to use Docker Compose, you can run the containers individually:

#### Run Redis
```
docker run -d --name redis -p 6379:6379 redis:7-alpine
```

#### Run Postgres
```
docker run -d --name postgres -e POSTGRES_PASSWORD=pass12345 -p 5432:5432 postgres:16-alpine
```

#### Build Flask App
```
docker build -t flask-app .
```

#### Run Flask App (linking to Redis & Postgres)
```
docker run -d --name web -p 8000:8000 --env REDIS_HOST=redis --env REDIS_PORT=6379 --link redis:redis --link postgres:postgres flask-app
```

Now open your browser at:
http://localhost:8000

---

## 🔧 Services & Ports

| Service  | Port (Host) | Description           |
|----------|-------------|-----------------------|
| web      | 8000        | Flask app (Gunicorn) |
| redis    | 6379        | Redis server          |
| db       | 5432        | Postgres database     |

---

## 🌱 Environment Variables

These are stored in `.env`:

- POSTGRES_PASSWORD → Postgres root password
- REDIS_HOST → defaults to redis (service name)
- REDIS_PORT → defaults to 6379

---

## 📸 Screenshots

1. Docker Desktop showing containers
2. Application running in browser
3. Container logs
4. docker ps output
5. PostgreSQL connection
6. Additional

---

## 🐞 Issues Faced During Execution

We logged issues in the GitHub Issues tab. Each problem has been documented with steps, logs, and fixes. Examples include:

- Flask app fails if Redis not ready → Fixed using healthchecks and depends_on.
- Port conflicts on 5432/8000 → Documented troubleshooting + option to remap ports.
- Counter reset after restart → Fixed by adding Redis volume with appendonly yes.
- ModuleNotFoundError for gunicorn/redis → Fixed by pinning dependencies in requirements.txt.
- Docker Desktop WSL2 not started → Added troubleshooting note.

See the Issues section for full details.

---

## 🛡️ Troubleshooting

- Ensure Docker Desktop is running.
- Free up ports 5432 and 8000 if already in use.
- Run docker compose down -v to remove volumes if data persistence causes errors.
- Check logs with docker compose logs -f web.

---

## ✅ Improvements Implemented

- Gunicorn as production WSGI server
- Healthchecks for web, redis, db
- .dockerignore for smaller images
- Persistent volumes for Redis and Postgres
- .env file support for secrets

---

## 📌 License

This project is for educational/demo purposes.








