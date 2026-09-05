# 🚀 Jenkins Declarative CI/CD Pipeline for Node.js Todo Application

A **Node.js Todo List Application** integrated with a **Jenkins Declarative CI/CD Pipeline** to automate the process of testing, building, publishing, and deploying the application.

The goal of this project was to understand how an application moves from:

```text
👨‍💻 Source Code
      ↓
🐙 GitHub
      ↓
🔧 Jenkins
      ↓
🧪 Testing
      ↓
🐳 Docker Build
      ↓
🛡️ Security Analysis
      ↓
📦 Docker Hub
      ↓
🚀 Deployment
```

---

# 🚀 Features

* 📋 Todo listing
* ➕ Add Todo
* ✏️ Edit Todo
* 🗑️ Delete Todo
* 🧪 Automated testing
* 🐳 Dockerized Node.js application
* 🧩 Docker Compose deployment
* 🔧 Jenkins Declarative Pipeline
* 📦 Docker Hub image publishing

---

# 📊 Project by the Numbers

```text
🌐 5 Application Routes
🧪 Automated Test Suite
🔧 1 Basic Jenkins Declarative Pipeline
⚙️ 4 Basic CI/CD Stages
🐳 Dockerized Application
🧩 Docker Compose Deployment
📦 Docker Hub Integration
```

---

# 🛠️ Tech Stack

| Technology        | Purpose                      |
| ----------------- | ---------------------------- |
| 🟢 Node.js        | Runtime environment          |
| 🚂 Express.js     | Backend web framework        |
| 🧪 Mocha          | Testing framework            |
| ✅ Chai            | Assertions                   |
| 🔬 Supertest      | HTTP/API testing dependency  |
| 🐳 Docker         | Containerization             |
| 🧩 Docker Compose | Container deployment         |
| 🔧 Jenkins        | CI/CD automation             |
| 🐙 GitHub         | Source control               |
| 📦 Docker Hub     | Container image registry     |

---

# 🌐 Application Routes

The Node.js Todo application contains **5 main routes/endpoints**.

| Method | Endpoint           | Purpose               |
| ------ | ------------------ | --------------------- |
| `GET`  | `/todo`            | Display Todo list     |
| `POST` | `/todo/add/`       | Add a new Todo        |
| `GET`  | `/todo/delete/:id` | Delete a Todo         |
| `GET`  | `/todo/:id`        | Open Todo for editing |
| `PUT`  | `/todo/edit/:id`   | Update a Todo         |

> These are application routes rather than a pure REST API design.

---

# 🏗️ Application Architecture

```text
                 👤 User
                   │
                   ▼
             🌐 Browser
                   │
                   ▼
             🚂 Express.js
                   │
        ┌──────────┼──────────┐
        │          │          │
        ▼          ▼          ▼
      GET        POST         PUT
      Todo       Add          Edit
        │          │          │
        └──────────┼──────────┘
                   │
                   ▼
             📋 Todo List
              In Memory
```

The application stores the Todo list in memory for this project.

---

# 🧪 Testing

The project uses:

* **Mocha**
* **Chai**
* **Supertest**
* **Node.js assertions**

The `package.json` contains the test command:

```bash
npm test
```

The Dockerfile also runs the test suite during the Docker image build:

```bash
npm run test
```

This means the Docker image build can fail if the automated tests fail.

---

# 🐳 Docker

The application is containerized using Docker.

### Dockerfile

The Dockerfile:

```text
Node.js Base Image
       ↓
Copy Application
       ↓
Install Dependencies
       ↓
Run Tests
       ↓
Expose Port 8000
       ↓
Start Node.js Application
```

Build the image:

```bash
docker build -t note-app .
```

Run the application:

```bash
docker run -d -p 8000:8000 note-app
```

Application:

```text
http://localhost:8000/todo
```

---

# 🧩 Docker Compose

The project also includes a Docker Compose configuration.

```yaml
services:
  web:
    image: nilesh0203/note-app
    ports:
      - "8000:8000"
```

Start the application:

```bash
docker-compose up -d
```

Stop the application:

```bash
docker-compose down
```

---

# 🔧 Jenkins Declarative CI/CD

The basic Jenkinsfile contains **4 stages**.

```text
┌──────────────────────────────┐
│        Jenkins Pipeline      │
└──────────────┬───────────────┘
               │
               ▼
        📥 Clone Code
               │
               ▼
        🐳 Build Docker
               │
               ▼
        📦 Push Docker Hub
               │
               ▼
        🚀 Deploy
```

---

## 1️⃣ Clone Code

Jenkins checks out the application source code from GitHub.

```groovy
git url:"<repository>", branch:"master"
```

---

## 2️⃣ Build Code

Jenkins builds the Docker image:

```bash
docker build -t note-app .
```

During the Docker build, the application dependencies are installed and tests are executed.

---

## 3️⃣ Push to Docker Hub

Jenkins uses stored credentials to authenticate with Docker Hub.

The image is tagged and pushed:

```text
note-app
   ↓
Docker Hub
   ↓
nilesh0203/note-app:latest
```

---

## 4️⃣ Deploy

The deployment uses Docker Compose:

```bash
docker-compose down
docker-compose up -d
```

This ensures the latest container image is used for deployment.

---

# 🔐 Jenkins Credentials

Docker Hub credentials are stored inside Jenkins rather than hard-coded into the pipeline.

The pipeline retrieves them using:

```groovy
withCredentials(...)
```

This is an important CI/CD security practice.

> Secrets should never be committed directly into source code or Jenkinsfiles.

---

# 🛡️ DevSecOps Pipeline

The project also contains a more advanced Jenkinsfile under:

```text
DevSecOps/Jenkinsfile
```

This pipeline expands the basic CI/CD process into a **10-stage DevSecOps workflow**.

```text
🧹 Clean Workspace
        ↓
📥 Git Checkout
        ↓
📊 SonarQube Analysis
        ↓
🚦 Quality Gate
        ↓
🔍 OWASP Dependency Check
        ↓
🐳 Docker Build
        ↓
🛡️ Trivy Scan
        ↓
📤 Docker Hub Push
        ↓
🧹 Docker Cleanup
        ↓
🚀 Docker Compose Deploy
```

# 🔄 Complete CI/CD Flow

```text
                  👨‍💻 Developer
                       │
                       ▼
                    GitHub
                       │
                       ▼
                  🔧 Jenkins
                       │
                       ▼
                📥 Checkout
                       │
                       ▼
                 🧪 Testing
                       │
                       ▼
              📊 Code Analysis
                       │
                       ▼
                🐳 Docker Build
                       │
                       ▼
               📦 Docker Hub
                       │
                       ▼
              🧩 Docker Compose
                       │
                       ▼
                  🚀 Deploy
```

---

# 🧠 What I Learned

Through this project, I practiced:

### Jenkins

* Jenkins Declarative Pipeline
* Agents
* Pipeline stages
* Jenkins credentials
* Automated build workflows
* Deployment automation

### Docker

* Dockerfiles
* Docker image creation
* Image tagging
* Docker Hub
* Docker Compose
* Container deployment
* Docker cleanup

---

# 🎯 Project Goal

The goal was to move from manually executing commands such as:

```text
git pull
npm install
npm test
docker build
docker login
docker push
docker-compose up
```

to an automated workflow managed by Jenkins.

Instead of:

```text
👨‍💻 Developer
   ↓
Manually execute commands
   ↓
Build
   ↓
Test
   ↓
Push
   ↓
Deploy
```

The goal is:

```text
👨‍💻 Developer
      ↓
🐙 GitHub
      ↓
🔧 Jenkins
      ↓
⚙️ Automated Pipeline
      ↓
🚀 Deployment
```

---

# 💡 Key Learning

> **CI/CD is about turning a sequence of manual commands into a repeatable automated process.**

---

# 🔮 Future Improvements

Possible improvements include:

* 🔄 GitHub Webhook-triggered Jenkins builds
* 🧪 Increase automated test coverage
* 📊 Better SonarQube quality rules
* 🛡️ Container image vulnerability scanning
* 🔐 Better secret management
* 🐳 Multi-stage Docker builds
* ☁️ AWS deployment
* ☸️ Kubernetes deployment
* 📈 Prometheus + Grafana monitoring
* 🔔 Slack/Email deployment notifications
* 🔵🟢 Blue-Green Deployment
* 🚀 Zero-downtime deployment

---

# 👨‍💻 Author

**Nilesh Kudale**

Java | Spring Boot | Node.js | Docker | Jenkins | AWS | DevOps | DevSecOps

---

# ⭐ Support

If you find this project useful or interesting, consider giving the repository a ⭐.

**Still learning. Still building. Still automating. 🚀**
