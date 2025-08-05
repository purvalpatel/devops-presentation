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




