# 🚀 Node.js App with Jenkins CI/CD Pipeline

This project demonstrates a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline using **Jenkins** and **Docker** for a simple **Node.js** application.

---

## 🎯 Objective

To automate the process of building, testing, and deploying a Node.js application using Jenkins.

---

## 🧰 Tools Used

- **Node.js**
- **Jenkins**
- **Docker**
- **GitHub**

---

## 📁 Folder Structure

```
node-app-jenkins-cicd/
├── app.js          # Node.js app entry point
├── Dockerfile      # Docker image configuration
├── Jenkinsfile     # Jenkins pipeline script
└── README.md       # Documentation
```

---

## 🔧 Prerequisites

Ensure the following are installed:

- Jenkins
- Docker
- Git
- Node.js (on your local machine for development)
- GitHub account

---

## 🛠️ Step-by-Step Workflow

### 1️⃣ Clone the Project

```bash
git clone https://github.com/<your-username>/node-app-jenkins-cicd.git
cd node-app-jenkins-cicd
```

---

### 2️⃣ Review the Application Code

#### `app.js`
```js
const http = require("http");
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.end("Hello from Jenkins CI/CD Pipeline!");
});

server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
```

---

### 3️⃣ Create the Dockerfile

#### `Dockerfile`
```Dockerfile
FROM node:14
WORKDIR /app
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

---

### 4️⃣ Create the Jenkins Pipeline Script

#### `Jenkinsfile`
```groovy
pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo '🔧 Building the Docker image...'
                sh 'docker build -t my-node-app .'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests (placeholder)...'
                sh 'echo "Tests passed!"'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo '🚀 Deploying the Docker container...'
                sh '''
                docker stop my-node-app || true
                docker rm my-node-app || true
                docker run -d -p 3000:3000 --name my-node-app my-node-app
                '''
            }
        }
    }
}
```

---

### 5️⃣ Configure Jenkins

1. Go to Jenkins Dashboard → **New Item**
2. Enter item name → Select **Pipeline**
3. In the Pipeline configuration:
   - Choose **Pipeline script from SCM**
   - SCM: **Git**
   - Enter your GitHub repo URL
   - Script Path: `Jenkinsfile`

---

### 6️⃣ Optional: Configure GitHub Webhook

To trigger builds automatically on push:

- Go to GitHub Repo → Settings → Webhooks
- Payload URL: `http://<your-jenkins-ip>:8080/github-webhook/`
- Content type: `application/json`
- Select: **Just the push event**

---

### 7️⃣ Trigger the Pipeline

Make a change and push to GitHub:

```bash
echo "// trigger build" >> app.js
git add .
git commit -m "Trigger Jenkins pipeline"
git push
```

Check Jenkins dashboard for job execution.

---

### 8️⃣ Access the Running App

Open in your browser:

```
http://<your-jenkins-ip>:3000
```

Expected output:

```
Hello from Jenkins CI/CD Pipeline!
```

---

## ✅ Conclusion

You’ve successfully set up a Jenkins CI/CD pipeline for a Node.js app using Docker. This setup automatically builds, tests, and deploys your app on every code push.

---
