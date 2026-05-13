# Jenkins CI/CD Pipeline Project 🚀

![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

A beginner-friendly DevOps project demonstrating a complete CI/CD pipeline using Jenkins for a Python Flask application.

## 📌 Project Overview

- Developer writes code in VS Code
- Code is pushed to GitHub
- Jenkins automatically detects the change
- Pipeline runs automated tests
- If tests pass → code is ready to deploy
- If tests fail → pipeline stops and alerts developer

## 🏗️ Architecture

\`\`\`
Developer (VS Code)
        ↓
   git push
        ↓
    GitHub
        ↓
   Jenkins detects change
        ↓
Stage 1: Checkout Code
Stage 2: Install Dependencies
Stage 3: Run Tests
        ↓
✅ PIPELINE SUCCESS!
\`\`\`

## 📁 Project Structure

\`\`\`
jenkins-cicd-project/
├── .github/workflows/cicd.yml
├── app/app.py
├── tests/test_app.py
├── Jenkinsfile
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
\`\`\`

## 🔧 Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.11 | Programming language |
| Flask | Web framework |
| Pytest | Automated testing |
| Jenkins | CI/CD server |
| Docker | Containerization |
| GitHub | Source code management |

## 📡 Flask API Endpoints

| Endpoint | Method | Response |
|----------|--------|----------|
| / | GET | App status and version |
| /health | GET | Health check |
| /add/a/b | GET | Sum of two numbers |

## 🧪 Automated Tests

| Test | What it checks |
|------|---------------|
| test_home | Home page returns 200 |
| test_health | Health endpoint returns healthy |
| test_add | 3 + 5 = 8 |
| test_add_zeros | 0 + 0 = 0 |

## 🚀 How to Run

### Step 1 - Clone the repo
\`\`\`bash
git clone https://github.com/neelk8s/jenkins-cicd-project.git
cd jenkins-cicd-project
\`\`\`

### Step 2 - Start Jenkins
\`\`\`bash
docker-compose up -d jenkins
\`\`\`

### Step 3 - Get admin password
\`\`\`bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
\`\`\`

### Step 4 - Open Jenkins
\`\`\`
http://localhost:8080
\`\`\`

### Step 5 - Install Python in Jenkins
\`\`\`bash
docker exec -u root jenkins apt-get update
docker exec -u root jenkins apt-get install -y python3 python3-pip
\`\`\`

### Step 6 - Create Pipeline Job
1. Click New Item
2. Name: flask-cicd-pipeline
3. Select Pipeline
4. Click OK
5. Set Definition to Pipeline script from SCM
6. Set SCM to Git
7. Set Repository URL to your GitHub repo
8. Set Branch to main
9. Set Script Path to Jenkinsfile
10. Click Save
11. Click Build Now

## ✅ Successful Pipeline Output

\`\`\`
Stage: Checkout          ✅
Stage: Install Deps      ✅
Stage: Run Tests         ✅
PIPELINE COMPLETED!
Finished: SUCCESS
\`\`\`

## 💡 Key Concepts Learned

- What Jenkins is and how it works
- How to write a Jenkinsfile
- How pipeline stages work
- How to write automated tests with pytest
- How Docker runs Jenkins and Flask
- How Jenkins integrates with GitHub

## 🔮 Future Improvements

- Add Docker build and deploy stages
- Add email notifications on failure
- Add code coverage reports
- Deploy to AWS EC2 automatically

## 👩‍💻 Author

**Neelam Roy**
DevOps Engineer (Transitioning) | AWS | CI/CD | Docker | Terraform | Jenkins
GitHub: https://github.com/neelk8s
