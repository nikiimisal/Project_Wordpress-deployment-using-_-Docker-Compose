# 🐳 WordPress Deployment Using Docker Compose



> Two-Tier Architecture | Docker Mini Project

This project demonstrates how to deploy WordPress with MySQL using Docker Compose on an AWS EC2 instance.<br>
It simplifies multi-container management using a single `docker-compose.yml` file.

---

## 🎯 Project Objective

- Deploy WordPress and MySQL using Docker Compose<br>
- Use Docker volumes for database persistence<br>
- Understand service-to-service communication<br>
- Learn container auto-networking in Docker Compose

<p align="center">
  <img src="https://github.com/nikiimisal/Project_Wordpress-deployment-using-_-Docker-Compose/blob/main/img/docr_composer.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>

---

## Architecture Overview (Two-Tier)

```java
User (Browser)
     |
     v
WordPress Container (App Service)
     |
     v
MySQL Container (DB Service)
```

---

## ⚙️ Prerequisites

- AWS EC2 (Amazon Linux 2)  👉[click here](https://github.com/nikiimisal/3-tier_Architecture_Related)<br>
- Docker installed & running  👉[click here](https://github.com/nikiimisal/Docker_info-and-setup)<br>
- Docker Compose v2+  👉[click here](https://github.com/nikiimisal/Docker-Examples-and-Concepts)<br>


---

##  🐳 Step 1: Install Docker Compose


```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.29.7/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Verify:

```bash
docker-compose version
```

---

##  Step 2: Project Directory Setup

```bash
cd /home/ec2-user
mkdir wordpress
cd wordpress
```


<p align="center">
  <img src="https://github.com/nikiimisal/Project_Wordpress-deployment-using-_-Docker-Compose/blob/main/img/Screenshot%202026-01-16%20071108.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

##  📝 Step 3: Create `docker-compose.yml`

```yaml
services:        # Defines all application services (containers)

  app:           # WordPress application container
    image: wordpress        # WordPress image from Docker Hub
    ports:
      - "80:80"             # Expose WordPress on port 80
    environment:            # Environment variables for DB connection
      WORDPRESS_DB_HOST: db # MySQL service name (acts as hostname)
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root
      WORDPRESS_DB_NAME: wordpressdb
    depends_on:             # Start DB container before app
      - db

  db:            # MySQL database container
    image: mysql             # MySQL image
    environment:             # MySQL initial configuration
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: wordpressdb
    volumes:
      - vol1:/var/lib/mysql  # Persist database data

volumes:         # Define Docker volumes
  vol1:          # Named volume for MySQL data
```

🧠 Easy Understanding (One Shot)

- `services` → What containers to run<br>
- `app` → WordPress container<br>
- `db` → MySQL container<br>
- `environment` → Configuration values<br>
- `depends_on` → Start DB first<br>
- `volumes` → Save data permanently<br>
- `ports` → Access app from browser


To view environment variables, you can check the official MySQL Docker repository.<br>
👉[click here](https://hub.docker.com/_/mysql)

---


---

##  ▶️ Step 4: Start Application

```
docker-compose up -d
```

Output (Expected)

```css
Network wordpress_default  Created
Volume "wordpress_vol1"   Created
Container wordpress-db-1  Started
Container wordpress-app-1 Started
```

<p align="center">
  <img src="https://github.com/nikiimisal/Project_Wordpress-deployment-using-_-Docker-Compose/blob/main/img/Screenshot%202026-01-16%20071256.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>

---

## 🔍 Step 5: Verify Running Containers

```
docker ps
```

---

##  🔐 Step 6: Verify MySQL Database & Tables


```bash
docker exec -it wordpress-db-1 /bin/bash
mysql -u root -p
```

```sql
use wordpressdb;
show tables;
```

✅ WordPress tables are now created automatically:

* wp_posts<br>
* wp_users<br>
* wp_options<br>
* wp_comments<br>
* etc.

This confirms **successful application–database integration**.



<p align="center">
  <img src="https://github.com/nikiimisal/Project_Wordpress-deployment-using-_-Docker-Compose/blob/main/img/Screenshot%202026-01-16%20071330.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>



---

##  🌍 Step 7: Access WordPress

Open browser:

```cpp
http://<EC2-PUBLIC-IP>
```

You will see the WordPress installation screen 🎉



<p align="center">
  <img src="https://github.com/nikiimisal/Project_Wordpress-deployment-using-_-Docker-Compose/blob/main/img/Screenshot%202026-01-16%20054155.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>




---


##  🧪 What Happens Internally?

- Docker Compose creates:<br>
   - One network<br>
   - Two containers<br>
   - One volume<br>
- WordPress connects to MySQL using:<br>
    - Service name `(db)`<br>
- WordPress automatically creates tables in DB




---

## 🧠 Key Docker Concepts Used


- Docker Compose<br>
- Multi-container application<br>
- Docker volumes<br>
- Auto-created Docker networks<br>
- Environment variables<br>
- Two-Tier architecture<br>

---

## 👨‍💻 Author

Nikhil Misal<br>
DevOps | Docker | AWS | Ansible | Terraform


---
---
---
















































































