4.1 Features:
---------
1. Continuous Integration/Continuous Delivery (CI/CD)
2. Extensibility - 1800+ plugins
3. Pipeline-as-Code: Jenkinsfile
4. Distributed builds: Scale workloads accross agents
5. Security: Role based access control


4.1.1 Installation:
--------------
[Official document link](https://www.jenkins.io/doc/book/installing/)

OR below are the installation steps for ubuntu:

Install java:
```
apt-get install openjdk-21-jdk
```

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

Restart jenkins:
```
/etc/init.d/jenkins restart

/etc/init.d/jenkins status
```

#### Open link in browser: 
http://server-ip:8080

<img width="992" height="885" alt="image" src="https://github.com/user-attachments/assets/35b93a3b-7c90-49b7-950f-35e7414454b2" />

The one time admin password is stored in,

```
cat /var/lib/jenkins/secrets/initialAdminPassword
```
Let the plugins installed:

<img width="992" height="885" alt="image" src="https://github.com/user-attachments/assets/81c81ef7-0820-402d-8a68-6724e5f373cc" />

#### Install plugins:
Maven Integration

Git server

4.2 Jenkins for continuous integration:
----------------------------------
### 4.2.1 Creating and running jobs:

Task 1: Build python app manually after changes done in git repository.

4.3 CICD Pipeline concepts:
--------------------------

### 4.3.1 Continuous Integration
Integration - Merging and testing
Goal : Merge code changes frequently (daily) with automated testing.

- Developers commit to shared repo (e.g., GitHub) multiple times/day.
- Automated builds + tests trigger on each commit.
- Fast feedback on failures 

### 4.3.2 Delivery and Deployment
- Deployment should done on dev, prod or test server.

4.4 Pipeline Security Basics:
----------------------------
- Authentication & Authorization
    - RBAC (Role-Based Access Control):
- Secrets Management
- Restrict script execution in Pipelines

4.5 Building a CI/CD Pipeline using Jenkins:
-------------------------------------------

jenkinsfile
```
pipeline {
    agent any

    environment {
        // Credentials (configure in Jenkins Credentials Manager)
        SSH_CREDS = credentials('ssh-server-creds') // ID of SSH username/password or key
        REMOTE_DIR = '/var/www/myapp'
        REMOTE_HOST = 'your-server-ip-or-domain.com'
    }

    stages {
        // Stage 1: Checkout code from Git
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/yourusername/your-repo.git'
            }
        }

        // Stage 2: Build the application (example: Node.js)
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        // Stage 3: Package artifacts (e.g., compress build files)
        stage('Package') {
            steps {
                sh 'tar -czvf app-build.tar.gz ./dist/*'  // Example for a frontend app
            }
        }

        // Stage 4: Manual approval before deployment
        stage('Approve Deployment') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    input message: "Deploy to ${REMOTE_HOST}?", ok: "Confirm"
                }
            }
        }

        // Stage 5: Deploy via SCP + SSH
        stage('Deploy') {
            steps {
                script {
                    // Copy files using SCP
                    sh """
                        scp -o StrictHostKeyChecking=no \
                            app-build.tar.gz \
                            ${SSH_CREDS_USR}@${REMOTE_HOST}:${REMOTE_DIR}/
                    """

                    // SSH into server to extract and restart services
                    sh """
                        ssh -o StrictHostKeyChecking=no \
                            ${SSH_CREDS_USR}@${REMOTE_HOST} \
                            "cd ${REMOTE_DIR} && tar -xzvf app-build.tar.gz && systemctl restart nginx"
                    """
                }
            }
        }
    }

    post {
        success {
            slackSend channel: '#deployments',
                     message: "✅ Successfully deployed ${env.JOB_NAME} to ${REMOTE_HOST}"
        }
        failure {
            slackSend channel: '#alerts',
                     message: "❌ Deployment failed: ${env.JOB_NAME} (Build ${env.BUILD_NUMBER})"
        }
    }
}
```




