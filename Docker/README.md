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
1. Create Git project with ( Application code, Dockerfile, Jenkinsfile, playbook )
    (Git project)[https://github.com/purvalpatel/Sample_Nginx_Project_autodevops]
2. 
