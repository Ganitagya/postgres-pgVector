# 🚀 PostgreSQL 17 with pgvector - Docker Compose Setup  

This repository provides a **Docker Compose** setup for running **PostgreSQL 17 with the pgvector extension**.  
The setup ensures **persistent storage**, so your data is not lost even if the container restarts.

---

## 📌 Features  
✅ Runs **PostgreSQL 17** with **pgvector** for AI-powered search  
✅ Uses **Docker Compose** for easy deployment  
✅ Includes **persistent storage** using Docker volumes  
✅ Secure database setup with environment variables  

---

## 🛠 Setup & Installation  

### **1️⃣ Clone the Repository**  
```sh
git clone https://github.com/Ganitagya/postgres-pgVector.git
cd postgres-pgVector
```


### **2️⃣ Start the Container**  
Run the following command to start PostgreSQL with pgvector:

```sh
docker compose up -d
```

This will:

Start a PostgreSQL container with the pgvector extension.

Map PostgreSQL to port 5432 on your local machine.

Store all database data in a Docker volume (pgdata).


### **📡 Connecting to PostgreSQL**  
🖥️ Using psql (Command Line)

```sh
psql -h localhost -U postgres -d mydatabase
```
Password: mysecretpassword

If not installed psql, then:
```sh
sudo apt update
sudo apt install postgresql-client
```

🔧 Using pgAdmin (GUI Tool)
Open pgAdmin.

Click Add New Server.

Under Connection:

Host: localhost

Port: 5432

Username: postgres

Password: mysecretpassword

Click Save to connect.


🔄 Managing the Container

✅ Check Running Containers
```sh
docker ps
```

✅ Check Logs
```sh
docker compose logs -f
```

✅ Stop the Container
```sh
docker compose down
```

✅ Start the Container Again
```sh
docker compose up -d
```

✅ Restart the Container
```sh
docker compose restart
```

✅ Remove Everything (Including Data)
⚠️ WARNING: This will delete all stored data.

```sh
docker compose down -v
```


🗂 Persisting Data
This setup ensures data persistence using a Docker volume (pgdata).
Even if the container is stopped or removed, your data remains intact.

To verify the volume, run:

```sh
docker volume ls
```

volumes:
  - ./pgdata:/var/lib/postgresql/data

This stores PostgreSQL data in the pgdata directory inside your repository.


📌 Extending the Setup
Changing PostgreSQL Credentials
Modify docker-compose.yml and restart:

```yaml
environment:
  POSTGRES_USER: newuser
  POSTGRES_PASSWORD: newpassword
  POSTGRES_DB: newdatabase
  ```

Apply the changes:

```sh
docker compose down
docker compose up -d
```


Running SQL Scripts on Startup
To execute custom SQL commands when the database starts:

Create a init.sql file inside a new docker-entrypoint-initdb.d/ folder.

Mount it in docker-compose.yml:

```yaml
volumes:
  - ./docker-entrypoint-initdb.d:/docker-entrypoint-initdb.d
  ```


PostgreSQL will execute any .sql files in this directory when the container starts.

