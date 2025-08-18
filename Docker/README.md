Installation:
-------------

`apt-get install docker.io`

Commands:
---------
```bash
docker pull nginx    ## pull image from dockerhub

docker images        ## list images

docker run nginx    ## Attached mode

docker run -d nginx    ## run in detached mode

docker ps             ## lits running containers

sudo docker run -p 80:80 -d nginx    ## Expose port

docker stop <id>        ## stop container.
```
Git + Jenkins + Docker + Ansible:
---------------------------------
##### Deploy one application 

##### Prerequisites:
1. Create Dockerhub account.
2. Add Docker hub credentails to jenkins:
    a. Manage jenkins -> Credentials -> Global -> Add credentials
       Username with password
       username : dockerhub-creds (purval1992)
       username: DOCKERHUB_PASS
   
##### Deppendencies:
1. Below packages need to install on jenkins server.
```
apt install docker.io
```

2. Create Git project with ( Application code, Dockerfile, Jenkinsfile, playbook )
    (Git project)[https://github.com/purvalpatel/Sample_Nginx_Project_autodevops]

3. Create Jenkins job.
   Create Item -> Select pipeline
   
   Select pooling
   
   For automatic build start we can achive this by two ways.
    1. webhook         ( this requires live jenkins URL)
    2. pooling
  
    So we are going with pooling.
