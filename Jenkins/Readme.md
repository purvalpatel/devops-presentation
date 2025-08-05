Installation:
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

