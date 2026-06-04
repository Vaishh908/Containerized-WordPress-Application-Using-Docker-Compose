# Containerized WordPress Application using Docker Compose

## Introduction

Setting up WordPress traditionally requires installing and configuring Apache/Nginx, PHP, and MySQL manually. This process can be time-consuming and prone to configuration errors.

With Docker Compose, you can deploy a complete WordPress environment in just a few minutes using containers. This project demonstrates how to run WordPress and MySQL as separate services while ensuring persistent data storage and easy management.


<img width="1100" height="733" alt="image" src="https://github.com/user-attachments/assets/67cf0bea-b2bf-4651-98b9-a956e6dab79d" />


## Project Objective

The objective of this project is to:

* Deploy WordPress using Docker containers
* Configure a MySQL database container
* Enable communication between WordPress and MySQL
* Use Docker Volumes for persistent storage
* Simplify deployment with Docker Compose


##  Prerequisites

Before starting, ensure the following are installed:

* Docker
* Docker Compose (v2 recommended)

Verify installation:

```bash
docker --version
docker compose version
```


## Project Structure

```text
wordpress-docker/
│
├── docker-compose.yml
└── README.md
```


##  Docker Compose Configuration

Create a file named `docker-compose.yml` and add the following content:

```yaml
version: '3.8'

services:
  myweb:
    image: wordpress:latest
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root
      WORDPRESS_DB_NAME: wordpressdb
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: wordpressdb
    volumes:
      - myvol:/var/lib/mysql

volumes:
  myvol:
```


##  Architecture Overview

### WordPress Container

**Image:** `wordpress:latest`

Responsibilities:

* Hosts the WordPress website
* Provides the user interface
* Manages themes and plugins
* Communicates with MySQL database

Port Mapping:

```text
Host Port 80 → Container Port 80
```


### MySQL Container

**Image:** `mysql:5.7`

Responsibilities:

* Stores WordPress content
* Maintains user accounts
* Saves site configurations
* Handles database queries

Persistent Storage:

```text
myvol:/var/lib/mysql
```

This ensures data remains intact even if the container is stopped or recreated.

---

##  Service Communication

Docker Compose automatically creates a private network.

WordPress connects to MySQL using:

```text
db:3306
```

Flow:

```text
Browser
   │
   ▼
WordPress Container
   │
   ▼
MySQL Container
   │
   ▼
Database Response
   │
   ▼
Website Displayed
```


##  Deploy the Application

Navigate to the project directory:

```bash
cd wordpress-docker
```

Start the containers:

```bash
docker compose up -d
```

Check running containers:

```bash
docker ps
```

---

## Access WordPress

Open your browser and visit:

```text
http://localhost
```

Or if deployed on AWS EC2:

```text
http://<EC2-Public-IP>
```

You will see the WordPress installation screen.


##  Complete WordPress Setup

1. Select your preferred language.
2. Enter Site Title.
3. Create an Admin Username.
4. Set an Admin Password.
5. Enter Email Address.
6. Click **Install WordPress**.

Login to the WordPress dashboard and start building your website.

---

##  Docker Commands

### Start Containers

```bash
docker compose up -d
```

### Stop Containers

```bash
docker compose down
```

### View Running Containers

```bash
docker ps
```

### View Logs

```bash
docker compose logs
```

### Restart Services

```bash
docker compose restart
```


## Real-World Use Cases

* Local WordPress Development
* Plugin Testing
* Theme Development
* DevOps Learning Projects
* Containerization Practice
* Cloud Deployments (AWS, Azure, GCP)


##  Key Learning Outcomes

By completing this project, you will learn:

* Docker Fundamentals
* Docker Compose Basics
* Multi-Container Applications
* Container Networking
* Persistent Storage with Volumes
* WordPress & MySQL Integration


##  Benefits of Docker Compose

- Quick Deployment

- Environment Consistency

- Easy Service Management

- Scalable Architecture

- Portable Across Systems

- Simplified Configuration


##  Conclusion

Docker Compose simplifies WordPress deployment by running WordPress and MySQL in separate containers while managing networking and storage automatically.

This project demonstrates modern DevOps practices and provides a practical introduction to containerized application deployment. Using a single Docker Compose file, you can quickly launch, manage, and scale a complete WordPress environment with minimal configuration effort.

---
