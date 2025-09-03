# docker_multi_container
# Hands-On L3: Installing Docker & Building a Multi-Container Microservice  
**Course:** ITCS 6190/8190 – Fall 2025  
**Instructor:** Marco Vieira  
**Student:** Atluri Sasi Vadana

---

## 🚀 Project Overview
This project demonstrates how to containerize and orchestrate a Python Flask web app with a Redis cache, and run a PostgreSQL database using Docker and Docker Compose.  

---

## 📂 Project Structure

```bash
├── app.py             # Flask app using Redis counter
├── requirements.txt   # Python dependencies
├── Dockerfile         # Flask service image
├── compose.yaml       # Docker Compose for web + redis
├── README.md          # Instructions
└── screenshots/       # (add your screenshots here)



---

## ⚙️ Setup & Execution Steps

### 1. Verify Docker Installation
```bash
docker -v

#2. Start PostgreSQL Container
docker pull postgres
docker run -d -p 5432:5432 --name postgres1 -e POSTGRES_PASSWORD=pass12345 postgres
docker exec -it postgres1 bash
psql -d postgres -U postgres
\l   # list databases
\q   # quit
exit # leave container

#3. Build and Run Flask + Redis

From the project folder:
docker compose up --build
4. Test in Browser

Open: http://localhost:8000

Refresh several times to see the counter increase.

5. Stop and Clean Up

# Stop running services
CTRL+C

# Remove containers
docker compose down





