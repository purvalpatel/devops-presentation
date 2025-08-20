Installation:
-------------

```bash
apt-get install docker.io

docker --version
docker info
```

Commands:
---------
```bash

docker search ubuntu       ## get list of available images
docker pull nginx    ## pull image from dockerhub

docker images        ## list images
    
docker run hello-world    ## run first container
docker run nginx    ## Attached mode

docker run -d nginx    ## run in detached mode

docker ps             ## lits running containers
docker ps -a            ## all containers

docker run -p 80:80 -d nginx    ## Expose port

docker run -v mysql_data:/var/lib/mysql -d nginx        ## mount volume

docker stop <id>        ## stop container.
dokcer start <id>        ## start container
docker rm <id>            ## remove container

docker network        ## docker network commands
```

Git + Jenkins + Docker + Ansible:
---------------------------------
#### Task : Deploy application on nginx webserver with docker.

### Devops plan:
1. Merge code in Github.
2. Jenkins take a pull from github.
3. Creates docker image and push on docker hub.
4. Ansible playbook will be executed for deployment of this image on live server.
5. Stop application on live server and deploy new one.

### Prerequisites:
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
    1. Go to **Manage Jenkins** → **Credentials**.
    2. Select **Global** → **Add Credentials**.
    3. Choose **Kind** → **Username with password**.
    4. Fill in the details:
       - **Username**: `DOCKERHUB_PASS`
       - **Password**: `xxxxx`
       - **ID**: `dockerhub-pass`
    5. Click **OK** to save.

6. Verify the ansible inventory.
   
### Jenkins job Setup:
1. **Login to Jenkins**  
   Open your Jenkins dashboard.

2. **Create a New Pipeline Job**  
   - Click on **New Item**  
   - Enter a job name  
   - Select **Pipeline**  
   - Click **OK**

3. **Configure Build Settings**  
   - Check **Discard old builds** (to save space and keep build history clean).

4. **Set SCM Polling**  
   - In **Build Triggers**, check **Poll SCM**  
   - Enter the schedule:  
     ```
     * * * * *
     ```
     (This polls the repository every minute. Adjust if needed.)

5. **Pipeline Definition**  
   - Under **Pipeline**, set:
     - **Definition**: *Pipeline script from SCM*  
     - **SCM**: *Git*  
     - **Repository URL**:  
       ```
       https://github.com/purvalpatel/Sample_Nginx_Project_autodevops.git
       ```
     - **Credentials**: Select the saved credentials (if required for private repos).  
     - **Branch Specifier**: `main`  
     - **Script Path**: Path to your `Jenkinsfile` (example: `Jenkinsfile` at repo root).

6. **Save and Build**  
   - Click **Save**  
   - Trigger **Build Now** or wait for SCM polling to detect changes.
