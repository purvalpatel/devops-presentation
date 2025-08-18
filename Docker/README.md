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
### Task : Deploy application on nginx webserver with docker.

#### Devops plan:
1. Merge code in Github.
2. Jenkins take a pull from github.
3. Creates docker image and push on docker hub.
4. Ansible playbook will be executed for deployment of this image on live server.
5. Stop application on live server and deploy new one.

#### Prerequisites:
1. Create Git project with ( Application code, Dockerfile, Jenkinsfile, playbook )
    [Git project](https://github.com/purvalpatel/Sample_Nginx_Project_autodevops)
   
2. Jenkins account with all packages installed.
   If no, install below dependencies:
    ```bash
    sudo pip3 install docker
    apt install docker.io        ## on jenkins server
    ```
   
4. Setup Dockerhub account.
5. Store Dockerhub credentials into jenkins.
    a. Manage jenkins -> Credentials -> Global -> Add credentials
       > New Credentials -> Username with password
       username : DOCKERHUB_PASS
       password: xxxxx
       ID : dockerhub-pass

6. Verify the ansible inventory.
   
#### Jenkins job Setup:
1. Login jenkins
2. Create Job
   New Item -> Pipeline
3. check Discard old builds
4. pool SCM : * * * * *
5. Definition
   Pipeline script for SCM
   Git
   Repository URL: `https://github.com/purvalpatel/Sample_Nginx_Project_autodevops.git`
   Select Credentaials
   Select main
   Script path
