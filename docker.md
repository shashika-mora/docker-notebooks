# 🐳 Docker & Containerization Roadmap

This document is the **Master Guide** for the Docker learning path. [cite_start]It consolidates container standards, image optimization techniques, and the curriculum derived from the `roadmap.sh` Docker track.

---

## 🛠️ Part 1: Topic Standards & Instructions
**⚠️ CRITICAL:** The AI must strictly adhere to these rules when generating notebooks for this topic.

### 1. Content Philosophy
* [cite_start]**📦 Compose Standard:** While `docker run` is good for basics, all multi-container examples must use **Docker Compose** (`compose.yaml`) as it is the industry standard for local development[cite: 446].
* [cite_start]**🏗️ Multi-Stage Builds:** Always teach **Multi-Stage Builds** for compiled languages (Go, Java, Rust) to ensure small, secure production images[cite: 452].
* [cite_start]**🛡️ Non-Root Default:** Every `Dockerfile` example meant for production must include a user switch (e.g., `USER node`) to demonstrate security best practices[cite: 466].
* **🧹 Cleanup:** Include commands to clean up resources (`docker system prune`) to prevent disk bloat.

### 2. "Add These" Checklist (Verification)
*Ensure every relevant notebook addresses these specific details:*
* [ ] Visual comparison of **VMs** (Hypervisor) vs **Containers** (Shared Kernel/Daemon) .
* [cite_start][ ] Explain the difference between **Bind Mounts** (Host filesystem) and **Named Volumes** (Managed storage)[cite: 444, 445].
* [cite_start][ ] Detail the **Layer Caching** mechanism and how ordering commands in a Dockerfile affects build speed[cite: 451].
* [ ] Distinguish between **ENTRYPOINT** (Executable) and **CMD** (Arguments).

---

## 📚 Part 2: The Roadmap & Notebooks

### 🔹 Module 1: Concepts & Architecture

* **Notebook 01 - 📦 Introduction to Containers**
    * **Concept:** What are containers? [cite_start]Why do we need them?[cite: 420, 421].
    * [cite_start]**Comparison:** Bare Metal vs Virtual Machines vs Containers[cite: 422].
    * [cite_start]**Tech:** High-level overview of Namespaces (Isolation) and Cgroups (Resource Limiting)[cite: 424, 425, 426].

* **Notebook 02 - ⚙️ Installation & The CLI**
    * [cite_start]**Setup:** Docker Desktop (Mac/Win) vs Docker Engine (Linux)[cite: 432, 434, 435].
    * [cite_start]**CLI:** The `docker` command structure and interacting with the Daemon[cite: 458].
    * [cite_start]**Registry:** Pulling public images from Docker Hub[cite: 450].

### 🔹 Module 2: Working with Containers

* **Notebook 03 - 🏃 Running & Managing Containers**
    * [cite_start]**Lifecycle:** `run`, `stop`, `start`, `rm`, and `logs`[cite: 448].
    * **Mode:** Detached (`-d`) vs Interactive (`-it`).
    * [cite_start]**Networking:** Port mapping (`-p`) and Bridge networks[cite: 460].

* **Notebook 04 - 💾 Data Persistence**
    * [cite_start]**Problem:** The Ephemeral Container Filesystem (Data loss on stop)[cite: 443].
    * [cite_start]**Volumes:** Creating and mounting Named Volumes for databases[cite: 444, 459].
    * [cite_start]**Binds:** Using Bind Mounts for code syncing during development[cite: 445].

### 🔹 Module 3: Building Images

* **Notebook 05 - 📄 The Dockerfile**
    * [cite_start]**Syntax:** `FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`[cite: 449].
    * **Context:** Understanding the build context and `.dockerignore`.
    * [cite_start]**Build:** Using `docker build` and tagging images[cite: 441, 453].

* **Notebook 06 - 🚀 Optimization & Best Practices**
    * [cite_start]**Caching:** Leveraging Layer Caching to speed up builds[cite: 451].
    * [cite_start]**Size:** Choosing the right base image (Alpine vs Debian Slim)[cite: 452].
    * **Multi-Stage:** Building artifacts in one stage and copying to a lean runner stage.

### 🔹 Module 4: Orchestration & Dev Experience

* **Notebook 07 - 🐙 Docker Compose**
    * [cite_start]**Definition:** Defining services in `compose.yaml`[cite: 446].
    * **Networking:** How services talk to each other by name (Service Discovery).
    * **Workflow:** `docker compose up` and `down`.

* **Notebook 08 - 🛠️ Developer Experience (DX)**
    * [cite_start]**Hot Reload:** Configuring Bind Mounts for live code updates[cite: 461].
    * [cite_start]**Debugging:** Attaching debuggers to running containers[cite: 462].
    * [cite_start]**CI/CD:** Basics of building images in GitHub Actions/Jenkins[cite: 464].

### 🔹 Module 5: Security & Deployment

* **Notebook 09 - 🔐 Container Security**
    * [cite_start]**Scanning:** Using tools like Trivy or Docker Scout[cite: 454].
    * [cite_start]**Runtime:** Read-only filesystems and user permissions[cite: 455, 466].
    * **Secrets:** Handling sensitive data (ENV vars vs Docker Secrets).

* **Notebook 10 - 🚢 Deployment Strategies**
    * [cite_start]**Orchestration:** Introduction to Docker Swarm vs Kubernetes[cite: 468, 469].
    * [cite_start]**Registry:** Pushing to ECR, GCR, or Docker Hub[cite: 442, 453].
    * [cite_start]**Platform:** Deploying to PaaS (e.g., Heroku, Railway)[cite: 470, 471].

---

## 🛠️ Part 3: Projects & Implementation

### 🟢 Beginner Projects (Single Container)
1.  **B-01_Static_Site:** Host a custom HTML file using the official **Nginx** image. (Topics: Bind Mounts, Ports).
2.  **B-02_Python_Script:** Dockerize a Python script that requests an API and prints the result. (Topics: Dockerfile, PIP).
3.  **B-03_Node_Express:** Containerize a simple Express.js API with a `.dockerignore` file. (Topics: Optimization).

### 🟡 Intermediate Projects (Multi-Container)
1.  **I-01_LAMP_Stack:** Set up a Linux, Apache, MySQL, PHP stack using **Docker Compose**. (Topics: Networking, Persistence).
2.  **I-02_Postgres_Backup:** Create a container that runs on a cron schedule to dump a Postgres database to a Volume. (Topics: Utilities).
3.  **I-03_Dev_Env:** Build a unified dev environment for a Full Stack app (React Frontend + Node Backend + Mongo DB). (Topics: Hot Reload).

### 🔴 Advanced Projects (Ops & CI)
1.  [cite_start]**A-01_CI_Pipeline:** Create a GitHub Action that builds, tests, and pushes a Docker image to Docker Hub on commit[cite: 464].
2.  **A-02_Secure_Go_App:** Build a "Distroless" or Scratch image for a Go application using Multi-Stage builds. (Topics: Security, Size).
3.  **A-03_Load_Balancer:** Use Nginx as a reverse proxy/load balancer sitting in front of 3 API container replicas. (Topics: Networking, Scale).