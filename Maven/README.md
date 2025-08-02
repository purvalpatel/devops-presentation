Maven installation:
-------------------
```
apt-get install maven

mvn --version
```
As it is Java application It requires Java:
```
apt-get install openjdk-21-jdk
java --version
```

Sample java app:
---------------
[Sample Code](https://github.com/jenkins-docs/simple-java-maven-app.git)

Commands:

Compile:    `mvn compile`

Run unit test:  `mvn test`

Make package(war,jar) : `mvn package`

Clean the old compilation: `mvn clean`

Fresh installation: `mvn clean install`


