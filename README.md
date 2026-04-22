📤 Push to GitHub
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/flask-docker-app.git
git branch -M master
git push -u origin master
✅ STEP 2: Start Jenkins

Run:

docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins-data:/var/jenkins_home jenkins/jenkins:lts
🔐 Get password
docker logs jenkins

👉 Copy password

🌐 Open Jenkins
http://localhost:8080
⚙️ Setup
Paste password
Install suggested plugins
Create admin user
Click Start using Jenkins
✅ STEP 3: Create Pipeline Job

In Jenkins:

Click New Item
Name:
final-pipeline
Select Pipeline
Click OK
Add Pipeline Script

Paste this:

pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/YOUR_USERNAME/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5002:5000 flask-app'
            }
        }
    }
}

👉 Replace:

YOUR_USERNAME
✅ STEP 5: Run Pipeline
Click Save
Click Build Now
Open Console Output

