- `37:00` [[Thu, 16.07.2026]]
  collapsed:: true
	- This is java based web application.
	  collapsed:: true
		- Web apps -> can be accessed using web browsers.
		- runs on server apache tomcat
		- project will be in `webapps` as war file ==after creating project== and run on apache.
			- ### About project:
				- `Web archive or WAR` -> Its a project's compressed zip file
					- Web app where `JSP` -> View;  `servlets` -> controllers are used
				- The data we submit here will be stored in DB( MySQL)
					- When we create an app with a language there is
						- a view or display,
						- in backend there are controllers ( when we request data); controllers submit data to DB
						- DB.
				- dockerfile steps
					- pull tomcat
					- create WAR file
					- copy paste it in webapp
					- remove root after webapp
					  collapsed:: true
						- compose file
							- container name
							- image name
							- exposed ports
							- 2 services one container has project another has mySQL
								- need to configure mySQL image
									- db p04
									- tables st_college, st_subject etc.
										- columns
				- We are actors, use browser click button, request will be sent from JSP (view) to controllers; Controllers will call database.
					- database is a server; when we send request to server we use `URL`
						- Host -> localhost
						- Port -> 3306
					- Project details
						- /ORSProject04/src/main/resources/com/sunilos/p4/bundle/system.properties
							- url is defined here
						- Database connection Parameters
							- url=`jdbc:mysql://localhost:3306/p04` to connect to db
								- p04 name of db
								- send username and password
						- The project use this url to communicate with database and send request to this url internally
						- project established connection with db; then entered data in db
						- When we run this on docker in url we need to`write service name`
							- we need to remove localhost as it will be running on docker
								- project wont send request on localhost now ; it will send request on my sql container on docker
								- In docker there is container to container communication
							- ORSProject-04/Dockerfile
								- webapp container send request internally to mysql container
								- devopsproject04/ORSProject04/src/main/resources/in/co/rays/bundle
								  /system.properties
									- replace localhost with url=`jdbc:mysql://mysql:3306/advance_java`
										- port no. of localhost and docker container can be same but not ip address
								- We need to do all this before creating WAR file as WAR Files are static and cant be changed
		- DONE server
			-
			-
			-
			-
- [[Fri, 17.07.2026]]
  collapsed:: true
	- java project sends request to db; url is in `system.properties`
		- its in /ORSProject04/src/main/resources/com/sunilos/p4/bundle/system.properties
		- replace
		- `#url=jdbc:mysql://localhost:3306/p04` -> this is for running on localhost
			- `url=jdbc:mysql://db:3306/p04` -> this is for docker
			- Whenever you made changes here update the project
	- ## Steps to run
		- right click on project in `eclipse`
			- go to `Maven`
				- `Update Project...`
					- Force update of Snapshots/Releases -> to update project
					- Press Ok
				- Refresh
			- Run as
				- `Maven build...`
					- Goals : clean install
					- skip test
					- apply and run
					- _creates `WAR` file_
					- ==Before running this all server should be off==
					- build success
				- target has `ORSProject04.war` file
				  collapsed:: true
					- if want to run on local apache 11 then copy and paste in webapp and run server (use localhost url here)
						- right click -> run as -> `maven  clean` to remove `WAR` file
				- refresh to see.
			- Use system explorer to see location of project
				-
		- open the project now on vscode
			- go to `C:\Users\Piyush\Documents\Project04\Mission_ORSProject4\New Project\ORSProject04`
			  collapsed:: true
				- Create `Dockerfile`: wherever dockerfile exists there is a target folder
				  collapsed:: true
					- ```shell
					  FROM tomcat:11
					  
					  COPY target/ORSProject04.war /usr/local/tomcat/webapps/ORSProject04.war
					  ```
				- Create `docker-compose.yml`
				  collapsed:: true
					- ```shell
					  version: '3'
					  services:
					    db:
					      image: mysql:8.0
					      container_name: ors-mysql
					      environment:
					        MYSQL_ROOT_PASSWORD: root
					        MYSQL_DATABASE: p04
					      ports:
					        - "3308:3306"
					      volumes:
					        - mysql_data:/var/lib/mysql 
					    webapp:
					      build: .
					      container_name: ors-webapp
					      ports:
					        - "8080:8080"
					      depends_on:
					        - db
					      
					  volumes:
					    mysql_data:
					  ```
					- build reads `Dockerfile`
					- p04 database will be created on its own; with its password; actually runs on `3306`
					  collapsed:: true
						- outside docker `3308`
						- network it will create itself
						- whatever you entering data in mysql will be stored in `/var/lib/mysql ` in docker
							- if you don't give that -> in next run it will be disappeared;
								- a new folder will be created `mysql` whenever you enter data and gets stored.
								-
				- find default terminal profile and choose cmd
				- `docker-compose build` -> builds webapp image
					- from `Dockerfile` it will pull image tomcat and copy to webapp of tomcat
				- `docker-compose up -d` -> runs both images and make containers
				- LATER `.project` is image file just confirm later
			- ==57==
				- Go to docker-desktop
					- in `ors-mysql` container
						- go to `exec`
							- run `mysql -u root -p` -> username root
							- write password `root` but it won't show
							- mysql> `show databases;`
								- database `p04` already created
								- but no tables.
									- `show tables;` to see tables.
									- database should have 8 tables named `p04`
								- Go to `mysql workbench`
									- Local
										- `Servers` menu
											- `Data Export`
											- select `p04`
											- Export to `Self-contained file`
											- `Start Export` in `Export Progress` Tab
											- Open this file `C:\Users\Piyush\Documents\dumps\Dump20260718.sql`
											  on vs code.
												- before `DROP TABLE IF EXISTS `st_college`;`
													- write
														- ```
														  USE `p04`
														  ```
											- copy it and write `drop database p04` in docker
												- paste the copied content in docker `exec`
												- in `exec`
													- `show databases;` to check if it's there
													- `create database p04`
													- `show databases`
													- paste the copied content in docker `exec`
													- `show tables`
												-
					- in `ors-webapp` container
						- go to localhost:8080 in browser
							- run `localhost:8080/ORSProject04`
							- Login using username password
								- ### Troubleshooting
									- Docker is case_sensitive
										- in sql query tables are written in CAPS
										  collapsed:: true
											- In docker its in small hence the error
												- go to `/ORSProject04/src/main/java/com/sunilos/p4/model/RoleModel.java`
													- change the caps to small
										- For outside docker port of sql is `3308`
										  collapsed:: true
											- so sqlworkbench is outside docker ; its a client
												- one server is running on local machine at 3306 with that workbench is connected
													- create another in workbench named `docker` with port 3308; username root ; test connection
													  connects with docker
													  now it will show the db present in docker
														- Now change the name of tables using wrench icon; apply and execute
												- another one on docker at same port
									- Now run on `exec`
										- `show databases;`
										- `use p04;`
										- `show tables;`
											- now all the tables are in CAPS.
											- Sign in, now everything works.
												- for admin access in ST_ROLES change to 1.
				-
- [[Sat, 18.07.2026]]
	- ## Commands to run webapp on AWS
		- ### Create Docker Image on Docker Desktop
		- ### Open Chrome Browser & log in to Docker Hub.
		- ### Open Command Prompt & log in to Docker: docker login
		- ### syntax of tagging
		  collapsed:: true
			- ```bash
			  docker tag <source-image>:<tag> <dockerhub-username>/<new-image>:<tag>
			  ```
		- ### Tag the Docker images
		  collapsed:: true
			- ```bash
			  docker tag orsproject04-webapp:latest abhaymalve09/orsproject04-webapp:latest
			  
			  docker tag mysql:8.0 abhaymalve09/mysql:8.0
			  ```
		- ### Push the Docker images to Docker Hub
		  collapsed:: true
			- ```bash
			  push image => docker push abhaymalve09/orsproject04-webapp:latest
			  
			  push image => docker push abhaymalve09/mysql:8.0
			  ```
		- ### Connect to AWS EC2 Instance via SSH
		  collapsed:: true
			- ```bash
			  ssh -i "C:\Users\Dell\Downloads\firstKeyPair.pem" ubuntu@13.50.111.244
			  ```
		- ### Install Docker on AWS EC2 Instance
		  collapsed:: true
			- ```bash
			  ubuntu@ip-172-31-4-220:~$ nano filename.sh # esse likhenge fir ek khali blank page ayga fir usme "ctl+v" kr denge
			  ```
			- `Code:`
			  collapsed:: true
				- ```bash
				  ###!/bin/bash
				  
				  echo "=== Stopping apt processes ==="
				  sudo kill -9 1962 2>/dev/null
				  sudo killall apt apt-get 2>/dev/null
				  
				  echo "=== Updating package list ==="
				  sudo apt-get update
				  
				  echo "=== Installing required packages ==="
				  sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
				  
				  echo "=== Adding Docker GPG Key ==="
				  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
				  
				  echo "=== Adding Docker Repository ==="
				  sudo add-apt-repository -y \
				  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
				  $(lsb_release -cs) \
				  stable"
				  
				  echo "=== Updating package list again ==="
				  sudo apt-get update
				  
				  echo "=== Installing Docker ==="
				  sudo apt-get install -y docker-ce
				  
				  echo "=== Starting and Enabling Docker ==="
				  sudo systemctl start docker
				  sudo systemctl enable docker
				  
				  echo "=== Adding current user to Docker group ==="
				  sudo usermod -aG docker $USER
				  
				  echo "=== Checking Docker Version ==="
				  docker --version
				  
				  echo "=== Granting Docker Socket Permission ==="
				  sudo systemctl restart docker
				  ls -l /var/run/docker.sock
				  sudo chmod 666 /var/run/docker.sock
				  
				  echo "=== User Groups ==="
				  groups $USER
				  
				  echo "=== Restarting Docker ==="
				  sudo systemctl restart docker
				  
				  echo "========================================="
				  echo "Docker installation completed successfully."
				  echo "IMPORTANT: Logout and login again (or run 'newgrp docker')"
				  echo "before using Docker without sudo."
				  echo "========================================="
				  ```
				- `bash filename.sh #to run bash file`
		- ### Log in to Docker on the EC2 Instance
		  collapsed:: true
			- ```bash
			  docker login
			  ```
		- ### Pull the Docker images from Docker Hub
		  collapsed:: true
			- ```bash
			  docker pull abhaymalve09/orsproject04-webapp:latest
			  
			  docker pull abhaymalve09/mysql:8.0
			  ```
		- ### Create a Network on AWS
		  collapsed:: true
			- ```bash
			  docker network create my-network
			  ```
		- ### Run Web Application Container
		  collapsed:: true
			- ```bash
			  docker run -d --name ors --network my-network -p 8080:8080 -e DB_URL="jdbc:mysql://db:3306/p-04" -e DB_USERNAME="root" -e DB_PASSWORD="root" abhaymalve09/orsproject04-webapp:latest
			  
			  docker run -d --name db --network my-network -p 3307:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=p-04 abhaymalve09/mysql:8.0
			  
			  docker run -d --name db --network my-network -p 3307:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=p04 askew8151/mysql:8.0
			  
			  docker run -d --name ors --network my-network -p 8080:8080 -e DB_URL="jdbc:mysql://db:3306/p04" -e DB_USERNAME="root" -e DB_PASSWORD="root" askew8151/orsproject04-webapp:latest
			  ```
		- ### View Docker Containers
		  collapsed:: true
			- ```bash
			  docker ps
			  ```
		- ### To test the webapp
		  collapsed:: true
			- `http://13.50.111.244:8080/ORSProject04/LoginCtl`
			- #### Troubleshooting
			  collapsed:: true
				- Expose the port of sql container
					- Edit inbound rules par click karo.
					- Add Rule.
					- Fill the following:
						- | Type       | Protocol | Port | Source                      |
						  |------------|----------|------|-----------------------------|
						  | Custom TCP | TCP      | 3307 | `0.0.0.0/0`  |
					- Save Rules.
					- ---
					- In sql workbench create an instance
						- Name : `Aws`
						- IP : `13.50.111.244`
						- Port: `3307`
						- create tables using p04 code and execute
						- 90+ rows created
						- Capitalize table names
		- ---
		- ### Stop and Remove Specific Docker Container
		  collapsed:: true
			- ```bash
			  docker stop tomcat-container
			  docker rm tomcat-container
			  ```
		- ### View Logs of Docker Container
		  collapsed:: true
			- ```bash
			  docker logs tomcat-container
			  ```
		- ### Remove Docker Images
		  collapsed:: true
			- ```bash
			  docker rmi username/tomcat:latest
			  ```
		- ### Stop Instance