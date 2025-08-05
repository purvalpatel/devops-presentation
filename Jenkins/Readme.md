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

4.2 Jenkins for continuous integration:
----------------------------------
### 4.2.1 Creating and running jobs:

Task 1: Build python app manually after changes done in git repository.

4.3 CICD Pipeline concepts:
--------------------------
Goal : Merge code changes frequently (daily) with automated testing.

### 4.3.1 Continuous Integration


### 4.3.2 Delivery and Deployment


4.4 Pipeline Security Basics:
----------------------------


### 4.5 Building a CI/CD Pipeline using Jenkins:




