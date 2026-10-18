- `37:00` [[Thu, 16.07.2026]]
  collapsed:: true
	- This is java based web application.
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
				-
- [[Sat, 18.07.2026]]
  collapsed:: true
	- ## Commands to run webapp on AWS
		- ### Create Docker Image on Docker Desktop
		- ### Open Chrome Browser & log in to Docker Hub.
		- ### Open Command Prompt & log in to Docker: docker login
		- ### syntax of tagging
			- ```bash
			  docker tag <source-image>:<tag> <dockerhub-username>/<new-image>:<tag>
			  ```
		- ### Tag the Docker images
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
			  id:: 6a742931-8eee-4bc4-a74b-5f3cb16fb92c
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
- [[Thu, 13-08-2026]]
  collapsed:: true
	- maven using dependencies downloaded jars.
	  collapsed:: true
		- 14 dependencies will be on maven repo. written in pom.xml
		- maven projects downloads jar files on its own and configure.
	- the ready made `web.xml` has older versions so use following
		- ```xml
		  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
		  	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		  	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
		  	version="6.0">
		  ```
		- from server's `web.xml` it gets index.jsp and runs by default
			- ```xml
			  <!-- on line 4752--> 
			  <welcome-file-list>
			          <welcome-file>index.html</welcome-file>
			          <welcome-file>index.htm</welcome-file>
			          <welcome-file>index.jsp</welcome-file>
			      </welcome-file-list>
			  ```
		- put the following in WEB-INF's `web.xml`
			- ```xml
			  <welcome-file-list>
			  		<welcome-file>index.jsp</welcome-file>
			  	</welcome-file-list>
			  ```
			- then it will take `index.jsp` from there
	- in webapp create css, img and jsp folder.
	- you have two folders in Java Resources
	- src/main/java and src/main/resources
		- in src/main/java/
			- in/co/rays/proj4 same as package written in artifact id.
				- create bean package
					- `BaseBean.java`
						- `public abstract class BaseBean implements DropdownListBean interface,`
						- override getKey only
						- make basebean abstract
						- if basebean overrides both methods then no need to make BaseBean abstract, that is why it is abstract
					- `RollBean.java`
						- child of basebean that will override getvalue
					- Total 8 beans are there.
				- controller
					- create two controllers
						- `BaseCtl.java`
							- does not have wildcard mapping
							- extend httpServlet
							- provide doGet and doPOST
							-
						- `BaseListCtl.java`
						- `ORSView.java` -> Interface
				- model
					- `BaseModel.java`
						- has nextPk()
							- it autogen pk
								- search max(id) for ex. 10 and return pk +1 ie. 11.
								- no need to give id again and again
						- `public abstract class BaseModel<T extends BaseBean>`
							- whenever you extend this BaseModel in childBean of it , in that we need to pass a generic T type which must be child of BaseBean
								- if i remove `extends BaseBean` then T will be of any type
							- `public abstract long add(T bean) throws ApplicationException, DuplicateRecordException;`
								- need to create abstract method so that class too become abstract
								- when we add record , the id on which it will be added , we return that id.
									- first record will be added on id 1.
								- this will be used in child where we override it.
							- likewise update, getwhereclause, getTable
						- we need to override the abstract methods of Basemodel in every child.
					- `RoleModel.java`
						- `public class RoleModel extends BaseModel<RoleBean>`
							- generic will be child of BaseBean
							- override all abstract methods of BaseModel
							-
				- util
					- [[Tue, 18-08-2026]]
						- 10 utility classes.
						- `ServerUtility.java`
							- we make `rd` object again n again to forward , so not to make it everywhere we need to use it in util package.
						- `jdbcbdatasource`
							- it is an utility class as well as singleton class.
							- `resourceBundleNotFoundException` will come when system.properties not found or something is wrong
							-
				- exception
					- extend `runtimeException`
					-
					-
		- in src/main/resources
			- create in.co.rays.proj4.bundle
				- in that create `System.properties`
				-
- [[Tue, 18-08-2026]]
  collapsed:: true
	- js folder will have a file that can have calendar function
	- jsp folder will have all the views.
	- BaseBean
	  collapsed:: true
		- it will have all the attributes which will be common to all 8 tables.
			- like id(Non Business primary key), createdby(Contains USER ID who created this database record), modifiedby(Contains Created Timestamp of database record), createddatetime, modifieddatetime. no need to make it in every table like college, student etc..
			  collapsed:: true
				- ```java
				  /**
				  	 * Non Business primary key इसमें नॉन बिज़नेस के स्टोर की जाती है
				  	 */
				  	protected long id;
				  
				  	/**
				  	 * Contains USER ID who created this database record. इसमें रिकॉर्ड क्रिएट करने
				  	 * वाले यूजर का ID स्टोर किया जाता है
				  	 */
				  	protected String createdBy;
				  
				  	/**
				  	 * Contains USER ID who modified this database record
				  	 */
				  	protected String modifiedBy;
				  
				  	/**
				  	 * Contains Created Timestamp of database record
				  	 */
				  	protected Timestamp createdDatetime;
				  
				  	/**
				  	 * Contains Modified Timestamp of database record
				  	 */
				  	protected Timestamp modifiedDatetime;
				  ```
				- ### Why we did that?
				  collapsed:: true
					- they store table's metadata
						- like who modified the table at what time
						- it's for developers.
						- timestamp has date time minutes seconds and milliseconds.
				- once these are created in parent no need to create in child, just make their getters setters.
				- `id` #[[Questions By sahu sir]]
					- non-business primary key
					- auto increment column
					- does not contain business information of user
					- just uniquely identify user.
				- to auto increment id use `nextPk()` , max id then return + 1
			- every table bean will be created but common ones will be created in basebean
		- it has one more method `public void setResultset(ResultSet rs) {`
			- when we search records and set in resultset and then we set to bean , no need to do it repeatedly.
			- so we use that method , just need to pass that resultset here and store in respective attributes using `this.setId(rs.getLong("ID"));`
			- now this method will be overridden by other child
		- create 8 tables from database.txt
	- RoleBean
	  collapsed:: true
		- only name and description will there and rest will come from BaseBean
		- override `setResultset` method
			- gets parent data from `super.setResultset(rs);`
			- rest will be set here.
			- column name must be same as tables like "NAME"
		-
	- Follow the sequence given in `database.txt`
	  collapsed:: true
		- st_role, st_user follow these sequence to make modules
		- database.txt is an ER diagram
	- ### Why we have created BaseModel
	  collapsed:: true
		- whichever model/table we create have add, update, delete, search, nextPk
			- so to avoid that create a baseModel once so no need to create that for child model
			- ==add and update are different for every model so we use abstract for them==; every model has different columns so that when child overrides it then they add or update their own columns or have their own special behavior.
			- #### Complete method
			  collapsed:: true
				- we make nextpk(searches max id) as complete method
				- we delete by id so make it here as complete method
				- search as complete method because we created `setResultset` method in bean so it will take values from there
				- these get fetched from base model.
			- #### Abstract method
			  collapsed:: true
				- add, update, getWhereClause, getTable, getBean
				- these will get overridden by children
	- RoleModel
		- getTable override it from BaseModel and return same model's table name which you want to get data.
			- we use getTable so that if spelling is wrong or not to see the table name again and again.
			- its project standard
	- BaseModel
		- `nextPk()`
			- having getTable() overridden by child class of basemodel
			- query will be run with current table
		- # Task
			- update method in rolebean
			- userbean extra attributes
				- extend basemodel generic userbean
				- code will auto generated
				- in add return bean.getid
- [[Wed, 26-08-2026]]
  collapsed:: true
	- Business validations in code
		- `findByLogin` -> in UserModel
		- `Authenticate` -> in UserModel
		  id:: 6a94c315-2fa6-41f8-a067-81dbd08ac75d
			- authenticate(String password, String login)
			- call findByLogin to get bean
			- bean != null and bean.getPassword.equal(password)
		- `findByPk` -> in all TestModels, searches record based on primary key.; made only once in BaseModel.
			- all models have primary key common
				- so `findByPk` will be created in basemodel
			- `findByPk` having argument `long pk`
				- return type `bean` for `Authenticate` too
				- `long pk` send as an argument from `TestRoleModel`
				- `pstmt.setLong(1, pk);` here pk contains the argument passed from test class.
				- in while loop bean's object will be formed from
					- ```java
					  @Override
					  	public RoleBean getBean() {
					  		return new RoleBean();
					  	}
					  ```
					- here child has overridden `getBean()` that returns new RoleBean object.
					- `bean.setResultset(rs);`
						- in BaseBean we had created:
							- ```java
							  public void setResultset(ResultSet rs) {
							  		try {
							  			this.setId(rs.getLong("ID"));
							  			this.setCreatedBy(rs.getString("CREATED_BY"));
							  			this.setModifiedBy(rs.getString("MODIFIED_BY"));
							  			this.setCreatedDatetime(rs.getTimestamp("CREATED_DATETIME"));
							  			this.setModifiedDatetime(rs.getTimestamp("MODIFIED_DATETIME"));
							  		} catch (SQLException e) {
							  			e.printStackTrace();
							  		}
							  	}
							  // rolebean has overridden it
							  
							  	@Override
							  	public void setResultset(ResultSet rs) {
							  		super.setResultset(rs);
							  		try {
							  			this.setName(rs.getString("NAME"));
							  			this.setDescription(rs.getString("DESCRIPTION"));
							  		} catch (SQLException e) {
							  			e.printStackTrace();
							  		}
							  	}
							  ```
							- When data comes in resultset it will be set to current bean `this`
							-
						- setResultSet will get all values from `rs` and set it to bean.
						- return the bean.
						-
			- T -> bean type
				- `userModel` has UserBean type
				- `roleModel` has RoleBean type
			-
		- `findByUniqueColumn`
			- pass column like `login` and value like `ram@gmail.com`
		- `findByName`
			- made only in RoleModel
				- if student name is already added in `st_role` so new student role should not be added again.
			- make an object of `RoleBean`
			- call method of BaseModel named as `findByUniqueColumn`
				- `	RoleBean bean = findByUniqueColumn("name", name);` name value can be `admin`
				- `"select * from " + getTable() + " where " + column + "='" + value + "'");`
					- `select * from st_role where name = student;`
					- if student record is there then bean gets returned. that means student already exists.
						- otherwise null pointer exception
					-
		- `findByLogin` -> UserModel
		  id:: 6a94dde3-7a01-4e21-9ab7-b1ae2ad84150
			- String login
			- call findByUniqueColumn having attribute login and its value
		- similarly `findByLoginId`
		- call `findByName` in add method of RoleModel.
			- if for ex. searched admin and it gets the admin then the record already exists so no need to add again. as it will throw duplicate record exception
		- call `findByName` in update method
			- if for ex. you are trying to update admin to student and student role already exists with id 2, throws exception. here existing id will be 1 and input id will be 2. Trying to make admin as student.
			- student can update student, existing id should be equal to input id otherwise record / role name already exists.
		-
	- ## Task
		- `findByPk`
			- test in every model
		- `findByUniqueColumn`
			- test in every model
		- `findByLogin`
			- can be made using ((6a94dde3-7a01-4e21-9ab7-b1ae2ad84150))
			- in add and update of UserModel use concept of RoleModel to throw duplicate record exception.
			- similarly for `findByCollegeName` in college
			- `findByRollNo` in student
			- `findBySubjectName`
		- `authenticate`
			- ((6a94c315-2fa6-41f8-a067-81dbd08ac75d))
			-
- [[Mon, 07-09-2026]]
  collapsed:: true
	- new Project > database.txt for tables in project 04
	- `Index.jsp`
	  collapsed:: true
		- now we don't give path instead `ORSView.WELCOME_CTL` where ORSView is interface and having attributes like `public String ***APP_CONTEXT*** = "/ORSProject-04";` and `public String ***WELCOME_CTL*** = ***APP_CONTEXT*** + "/WelcomeCtl";`
		- for paths; declare it in *ORSView*
		- On clicking *Online Result System* request goes to *WelcomeCtl*
			- *WelcomeCtl* extends *BaseCtl*
			- *BaseCtl*'s `doGet()` will run; `service` will run too but as method is not post (since we clicked a link.)
			- forwards to `getView()`
				- `getView()` is in BaseCtl and method is abstract
				- `BaseCtl` child is `WelcomeCtl`
					- `WelcomeCtl` returns `ORSView.***WELCOME_VIEW***`;
					- `public String ***WELCOME_VIEW*** = ***PAGE_FOLDER*** + "/Welcome.jsp";`
					  `***PAGE_FOLDER*** = "/jsp";`
					- Welcome.jsp will be displayed.
		- `BaseCtl`
		  collapsed:: true
			- `protected abstract String getView();`
				- returns view of all the controllers in children of BaseCtl. for example if request goes from `WelcomeCtl` then `ServletUtility` forwards to WelcomeView.
				- return type is String.
			- `protected abstract M getModel();`
				- returns object of models of all the controllers.
		- `Header.jsp`
		  collapsed:: true
			- `boolean isLogin = userBean != null;` if userBean is not null that means `True`
			- `<**h3**><**b**><%=welcomeMsg + userBean.getFirst_name() + "(" + roleName + ")"%></**b**></**h3**>` in header it will show user's first name as well as role name.
			- When we click on Login ; request goes to `LoginCtl`
				- `BaseCtl`'s `doGet` won't run as it is overridden by `LoginCtl` and forwards to getView() (LoginView); service method of `BaseCtl`will run first but as it is get method then validate won't run.
				-
		- `LoginCtl`
		  collapsed:: true
			- here BaseCtl's doGet wont run.
				- because user gets logged out so need to override the default doGet of parent.
				- if it gets operation, then session will invalidate and user gets logged out. Otherwise it forwards to view
			- ==This is the only Ctl where doGet will be overridden.==
		- `UserRegistrationCtl`
		  collapsed:: true
			- won't have `doGet` but has `doPost`
			- here `BaseCtl`'s doGet will run and forward to view.
			- because we won't do any new operation just forward to view.
			- ==This is the only Ctl where doPost will be overridden==
				- Here we register the user; in other places message is record added succesfully
				- and we don't update too when user gets signed up. User only gets added here.
				- parent's doPost have both add and update.
		- `Welcome.jsp`
		  collapsed:: true
			- if `isLogin` True then show first name otherwise blank
		- Why have you called from `ORSView` #buildQ
		  collapsed:: true
			- Because this is project standard
			- all paths are set in the interface named `ORSView`
			- Due to this View and Controller are loosely-coupled so that no need to write the path repeatedly.
		-
		-
	- ## Login's flow
		- ### Input Validation #buildQ
		  collapsed:: true
			- Click on `SignIn` no inputs in login and password
			- request goes to **Following guideline 4: submitting from view(LoginView) ; request goes to its own controller(LoginCtl).** LoginCtl
			- method will be "post" ( in form)
			- now in loginCtl ; baseCtl has service method and getMethod is post hence `validate()` will run; which is defined in baseCtl ;by default return type true
			- loginCtl has overridden validate
			- datavalidator's `isNull()` will check login value is null ; as we didn't give any input in login hence it is true.  pass value is false ; in request set error message `login is required`
			- same in password ; return false ; hence this condition of `service` of baseCtl `if (validate(request) == false) {` is true. hence it forwards to view and doPost won't run
			- getView is overridden by child "jsp/LoginView.jsp"
				- in loginView we have `ServletUtility.getErrorMessage` with which we print error message using `key` and `request`
			- ---
			- Summary:
			  collapsed:: true
				- **Input validation flow:** ( common to all only  child class will change)
					- Clicked on SignIn with no inputs in login and password
					- request goes to LoginCtl
					- method will be post
					- baseCtl service method will run; condition will be true [ request.getMethod is post]
					- in another condition inside that validate method will run but of LoginCtl.
					- LoginCtl's validate method has DataValidator.isNull with which we check whether login and password are null and if yes pass value will be null; in request.setAttribute we set error message in form of key value pair
					- in baseCtl `if (validate(request) == false) {` condition will be true from there it forwards to view.
					- In view using `ServletUtility.getErrorMessage` we print the errror message using key and request
			-
			-
		- ### Business Validation
		  collapsed:: true
			- don't go in input validation flow when explaining this one.
			- give wrong login and password
			- click on SignIn
			- request will go to LoginCtl
			- Service method of baseCtl will run
			- method is post ; validate will run but pass value is True hence condition gets false
			- doPost will run of Child ie. LoginCtl not BaseCtl because it has authenticate method
			- using `request.getParameter` we get login and password and will send it to authenticate method.
			- in baseCtl we made `populateBean()`
				- it gets request parameter from view or gets data from view and set it to bean
				- To get data from view we use `request.getParameter()` and set using bean.set
					- `request.getParameter("login")`
					- `bean.setLogin(DataUtility.*getString*(request.getParameter("login")));`
				- in baseCtl populateBean return type will be `B` -> generic Bean
					- when `populateBean` gets overridden by child then return type will be `UserBean`
					- it gets login and password using request.getParameter ;using bean.setlogin and bean.setpassword set those in bean.
					- and returns bean as now it has both login and password we will send it to authenticate method of model
					- DataUtility.*getString* -> will trim loginid whitespaces when it gets set in bean.
					- we gave wrong login password hence bean will be null ; else's `setErrorMessage` will run
					- `ServletUtility.*setErrorMessage*("Invalid login or password", request);`
						- it already has key named error in baseCtl
						- `*setMessage*(BaseCtl.***MSG_ERROR***, msg, request);`
						- ```java
						  public static void setMessage(String key, String msg, HttpServletRequest request) {
						  		if (DataValidator.isNotNull(key) && DataValidator.isNotNull(msg)) {
						  			request.setAttribute(key, msg); // key is error and msg is Invalid login pass
						  		}
						  	}
						  ```
						- The error message will be set to request Attribute.
						- forwards to loginview
						- in loginview `String _err = ServletUtility.getErrorMessage(request);` this will get error key usng `request.getAttribute` having message ` msg is Invalid login pass` it will be stored in geterrormessage and return
		- ### When user gets logged in successfully
			- in loginctl if bean is correct then it will set in session;
				- the user who gets searched with his role id search the role as given in `RoleBean rbean = rmodel.findByPk(bean.getRole_id());`
				- and made key in session named role as given in `session.setAttribute("role", rbean.getName());` and get the role name
					- for ex. the user who gets searched is `admin` and his role id is 1 and ` rmodel.findByPk(bean.getRole_id());` the id will be 1 and it searched admin
					- and admin's name will be set here `session.setAttribute("role", rbean.getName());` in role named key.
					- now role has user as well as role name. and redirect it to welcomectl
						- response's sendredirect method will get called.
						- redirected to WelcomeCtl; doget will run and welcomeview get displayed
						- `header.jsp` condition gets true that is isLogin will be true hence firstname and rolename can be displayed
						- `welcome.jsp` condition get true too. ==36:08==
						-
					-
				-
		-
	-
- [[P04Questions]]
- [[Tue, 08-09-2026]]
  collapsed:: true
	- When user clicked `SignUp` the method which gets the data from view and sets it to bean -> populateBean (BaseModel)
	- In view
		- `<select>` and `<options>` give dropdown
	- when we click Admin in dropdown , role id will be 1
- ### Foreign key relations to access common columns in another table
  collapsed:: true
	- ```
	  college studetn
	  college facutly
	  faculty ke college name me set
	  
	  
	  college id se college ko search karega agar ni hogi to nullpointer exception aaygi; id ke bhejne se college ka name v leke aata h aur khud set kar leta h
	  pehle college id v de rhe aur college name ab college name ni dena padega apne aap lelega testAdd aur testUpdate me
	  replace collegeName with cbean.name
	  ```
- [[Fri, 09-10-2026]]
  collapsed:: true
	- # Front Controller
	  collapsed:: true
		- ### Definition
		  collapsed:: true
			- User mustn't access the controllers without login except those 4.
			- otherwise user can access the user list
			- we use it in between the controllers ; checks if user is set in session if yes then can access controllers otherwise send it to loginview.jsp
			- It acts as interceptor.
			- ---
			- It used to prevent any user to access application without login.
		- Implement Filter Interface to create front controller
		- `@WebFilter("/ctl/*")`
			- * means all
			- means the filter applies to all matching URL paths in the application.
		- 3 life cycle methods
		  collapsed:: true
			- init
			- doFilter
				- doFilter runs on every request just like servlet's service method runs on every request
				- runs when a matching request passes through the filter.
				- need to typecast `ServletRequest` to `HttpServletRequest` similarly with response
			- destroy
		- `chain.doFilter(arg1, arg2);`
		  collapsed:: true
			- calls next config filter or controller in chain
			- chain means whatever the controller is there in place of * in `/ctl/` it calls that.
			-
		- whenever "user" gets set in session user gets logged in.
			- what if user is not logged in and we try to open UserList then doFilter() we made it to run , checks if `session.getAttribute("user") == null` if true sets error and forward to loginview.jsp
			- if user is logged in and `session.getAttribute("user") != null` then `chain.doFilter()` calls the controller.
		- To apply the filter use `/ctl` before controller.
		- Whenever you change the pattern of a ctl or rename the name of certain file ; clean the server and project. to re-configure.
		- ### Where not to apply
		  collapsed:: true
			- `LoginCtl`
			- `WelcomeCtl`
			- `ForgetPasswordCtl`
			- `UserRegistrationCtl`
			- ---
			- because we can access these without log in
			-
		- ### Flow
			- On clicking `UserListCtl` request goes to `@WebFilter("/ctl/*")` and doFilter gets called.
			- session user is null if we got logged out and try to access userlistctl
			- forwarded to loginview.jsp and error will get printed.
			- else if user is logged in then
				- `chain.doFilter()` will run and call its next ctl here it is `userlistctl`
	- # Factory design pattern
	  collapsed:: true
		- Connection is an interface but follows this design pattern
		- it provides statement's object using the createStatement() method.
		- `Statement stmt = con.createStatement();`
		- JDBCDataSource provides a Connection object.
		- Connection provides a Statement object using con.createStatement().
		- Connection provides a PreparedStatement object using con.prepareStatement(sql).
		- DriverManager.getConnection()
		-
	- # Edit
		- we need id and the record we want to edit for that we need entire data.
		  collapsed:: true
			- because `update table set f=?, l=? ... where id=?`
			- if we update a table we need its id and whole data.
		- we don't need to print id but for demo purpose and clarity we are doing it.
		  collapsed:: true
			- on view add bean.getId() in while loop
			- we need to update one at a time so we don't use update instead we use `findByPk` method; search the record which you want to update using `findByPk`
			- `select * from st_user where id = ?` searches for record and return as bean.
			- we create a `<td><a href="UserCtl.do?id=<%=b.getId()%>">Edit</a></td>` in userlistview.jsp [Actually this is for jsp/servlet]
				- `<td><a href="<%=ORSView.USER_CTL+"?id="+b.getId()%>">Edit</a>`
					- this if for project
			- in link we are giving id  in `doGet` get the id; run findByPk() searches the record of this id; set in the request and forward to view.
				- userctl par baseCtl ko extend kiya hai basectl ki service chalegi ;
				- request method `get` hai. to post ki condition ni chalegi aur super.service chalegi aur doGet chaljaygi basectl ki.
				- get id from query string from `UserListCtl` view using `request.getparameter(id)` pass it in Datautility.getLong.
					- `DataUtility.getLong` parses the String to long.
					- `M model = getModel();`
						- M generic can have rolemodel, usermodel etc.
					- `ServletUtility.forward(getView(), request, response);` in request it has bean.
					- get the bean on `userview` using `UserBean bean = (UserBean) request.getAttribute("bean"); ` or `ServletUtility.getBean(request)`
						- OR using `jsp:usebean` tag on view.
							- request me jo v attribute hota hai use direct nikal leta hi without typecasting
							- `<jsp:useBean id="obj" class="packageName.ClassName" scope="request" />`
								- `<jsp:useBean id="bean" class="in.co.rays.proj4.bean.UserBean" scope="request"></jsp:useBean>`
								- it finds key from request; id me key -> bean
					-
			- in `userView`
				- fill the fields' empty value using
					- `value="<%=DataUtility.getStringData(bean.getName())%>"></td>`
					- if bean.getName is empty then blank otherwise in value it gets name.
			- with this id we call doGet's UserModel's findbypk search record using this id; set in request and forward to view. and show on view as form with data filled. change the form field and save.
		- Flow
			- we made a link of edit in user list.
			- clicked on edit link
			- we are sending id using query string on `userCtl`
			- request goes to `userctl` basectl's Doget will run
				- get the id from query string
				- if (id >0)
					- use `findByPk` search the record using id
					- set the bean in request and forward to view.
					- get the bean on jsp.
					- and in fields show the filled data.
					- click the save button to save the updated fields.
					  collapsed:: true
						- but for that we need `id` because without that how it will update.
						- so in hidden field we need to provide id
							- `<input type="hidden" name="id" value="<%=DataUtility.getStringData(bean.getId())%>">`
							-
					- basectl's do post will run
					- call the method `populateBean()`
						- get the id from view's hidden input field `bean.setId(DataUtility.getLong(request.getParameter("id")));`
					- in try catch
						- ```java
						  if (bean.getId() > 0) {
						  	model.update(bean);
						  	ServletUtility.setSuccessMessage("record updated successfully", request);
						  } else {
						  	model.add(bean);
						  	ServletUtility.setSuccessMessage("record saved successfully", request);
						  }
						  ```
						- in update we are passing bean which has id as well as whole data.
						- the query will be `update st_user set firstname=?... where id=?`
						- set success message using servlet utility's set success in form of message and request.
						- *else*
							- if bean does not have that id then add the record.
							- `record saved successfully`
					- One more thing you can do is on `UserView`
						- ```jsp
						  <h1>Add Role</h1> // replace this line with following.
						  <h1><%=bean != null && bean.getId() > 0 ? 
						    "Update Role" : "Add Role"%></h1>
						  ```
						- In add role we don't send id in query string ; doGet will run but `findByPk` won't ; so bean won't set the data... so bean will be empty then Add role will be shown.
						-
	- ## updated JDBCDataSource
	  collapsed:: true
		- don't make the static variable final
		- JDBCDataSource instance was getting created every time.
		- earlier we had a code
			- ```java
			  if (jdbc == null) {
			  	return new JDBCDataSource();
			  }
			  ```
				- we didn't store instance in jdbc attribute.
				- the attribute's value is null here.
				- when `getInstance()` ran again it gets jdbc = null then it created instance again. that created multiple connections.
			- we need to store the `new JDBCDataSource()` into jdbc.
				- ```java
				  //updated code
				  private static JDBCDataSource getInstance() {
				  		if (jdbc == null) {
				  			jdbc = new JDBCDataSource();
				  			return jdbc;
				  		}
				  		return jdbc;
				  	}
				  
				  	public static Connection getConnection() { // factory design pattern
				  		try {
				  			return getInstance().c.getConnection();
				  		} catch (Exception e) {
				  			// TODO Auto-generated catch block
				  			e.printStackTrace();
				  		}
				  
				  		return null;
				  	}
				  ```
				- if `getInstance()` runs next time then it gets the value in jdbc. and it returns that and won't go inside if. and won't create new instance. thereby failing singleton design pattern.
				-
- [[Mon, 12-10-2026]]
	- which query will run when model's add method runs
	  collapsed:: true
		- `insert into st_user value()`
	- Method when insert query runs
	  collapsed:: true
		- `executeUpdate`
		-
	- SMTP
		- Use it to add mail functionality in application
		- for this we need to use 3 utility class
			- `Email Message class`
				- attributes to send email -> to, subject, message, message type
			- `Email Builder`
				- contains messages to send
				- 3 types of messages you can send in email
					- `UserRegistrationMessage()`
					- `ForgetPasswordMessage()`
					- `ChangePasswordMessage()`
			- `Email Utility`
				- It uses SMTP's 6 pre defined classes to send mail
				  id:: 6ad0248f-836e-44a5-97c5-ab7c2cd9e567
					- Session
					  id:: 6ad0253c-0e7c-4e84-9cab-942fce43b6df
					- Authenticator
					  id:: 6ad0253c-799a-4864-aaa4-b3244c1afe42
					- PasswordAuthentication
					  id:: 6ad0253c-b5c9-46f2-a560-b2b2449fb978
					- Message
					  id:: 6ad0253c-3771-4919-8e21-085cee823cae
					- MimeMessage (Multipart Internal Mail Extension)
					  id:: 6ad0253c-3823-441d-b299-94b9f78411fb
						- Used to send attachments.
					- Transport
					  id:: 6ad0253c-37d6-47fc-907e-d87b186d436a
		- use these to send mail
			- go to system.properties
				- 4 parameters of smtp
					- ### Email Server Parameters
						- smtp.server=smtp.gmail.com
						- smtp.port=465
						- email.login=webmaster@sunrays.co.in ->gmail id
						- email.pwd=PA$$1234 -> app password
					-
- [[Wed, 14-10-2026]]
	- ## Mail
		- In `usermodel`
			- `register()`
				- instead of calling add method we now use `register` method to add user in db and send registration mail.
					- ```java
					  public long register(UserBean bean) {
					  		long pk = add(bean);
					  ```
					- passing bean in add ; adds in database.
				- code to send email for new registration which we had used in testSmtp.java
					- ```java
					  HashMap<String, String> map = new HashMap<String, String>();
					  		EmailMessage msg = new EmailMessage();
					  
					  		map.put("login", bean.getLogin());
					  		map.put("password", bean.getPassword());
					  
					  		msg.setTo(map.get("login"));
					  		msg.setSubject("User Rgistration Information");
					  		msg.setMessage(EmailBuilder.getUserRegistrationMessage(map));
					  		msg.setMessageType(EmailMessage.HTML_MSG);
					  		// as messages in EmailBuilder are html type so we give html_msg 
					  		EmailUtility.sendMail(msg); //to send email
					  		System.out.println("mail send successfully");
					  
					  ```
					-
			- `forgetPassword()`
				- we need a mail id for forgot password to work.
				- `UserBean bean = findByLogin(login);`
					- searches user using `findByLogin()`
				- user gave `loginId` ; password gets searched using findByLogin and his data gets stored in bean.
				- that password along with login, first name, last name  put it in map object.
				- `EmailBuilder.getForgetPasswordMessage(map)` get the password from map object and creates a message using `msg.setMessageType(EmailMessage.HTML_MSG);` and sends the mail `EmailUtility.sendMail(msg);`
			- `changePassword()`
				- searches the database using login sets in bean
				- checks bean !=null and bean's password must be equal to old password.
					- set new password in bean `bean.setPassword(newPassword);`
					- update the bean -> this will update the record and it sets new password.
				- When we change password we must give old password; as it checks whether the old password exists in database.
					- so that it searches whether the user is valid one or not.
					-
		- ctl for all  3
		  collapsed:: true
			- forget password view before login.
				- it has only one input field `login` and a button
				- validate has login.
				- forgetPassword(bean.getLogin()
				- if bean !=null forget else.
				- get in doPost; send in model's `forgetPassword()`
			- change password view after login. in header.
				- password can only be changed when you know older password. so for that we need to log in
				- It has 3 fields `Login` , `old password`, `new password`
					- `bean = model.changePassword(request.getParameter("newPassword"), bean.getPassword(), bean.getLogin());`
						- here `bean.getPassword()` is old password.
						-
				-
		- Mail send Flow
		  collapsed:: true
			- we have used SMTP
			- added dependency jakarta mail
			- 3 custom and 6 predefined class
			  id:: 6ad065c5-a002-46fc-8ea1-5cc33833d6ab
			  collapsed:: true
				- 3 custom
					- In `EmailMessage` to whomsoever the mail need to be sent ; need to make *to*, *subject* and other fields.
					- `emailBuilder` generates messages
						- has 3 methods ->change, register, forget password
						- contains message to send in 3 ways using those 3 methods.
						- used simple `StringBuilder` `msg` object keep on appending the messages step by step. finally return the build msg. in form of String. follows #builderDesignPattern
					- send the mail using `EmailUtility.sendMail()` and in that method we used `Transport.send(msg);` to send email.
						- ((6ad0248f-836e-44a5-97c5-ab7c2cd9e567))
							-
			- We send mail in 3 cases: change password, user registration, forget password
		- ### Integration logic
		  collapsed:: true
			- we have used `smtp.server=smtp.gmail.com` service to integrate email in our application. we have used it in model and made in utility class.
		- we didn't receive emails
		  collapsed:: true
			- for receiving there are 2 protocols
				- IMAP
				- POP3
	- ---
	- ## Search filters
		- `UserListCtl` search by firstname
		  collapsed:: true
			- we clicked on search button
			- request goes to `userListCtl` extends `BaseListCtl` extends `BaseCtl`
				- `BaseCtl's` service method will run and its validate will run and returns true because we have not overridden `validate` in `BaseListCtl`
				- `doPost` will run.
					- `populateBean` gets overridden by `UserListCtl`
					- `b.setFirstName(DataUtility.getString(request.getParameter("firstName")));` gives `C`
					- send this returned bean in model's search method.
						- query `select * from "+st_user+" where 1=1`
						- `s.append(" limit "+pageNo+","+pageSize);`
						- `s.append(getWhereClause(bean));` overridden by `userModel`
						- `s.append(" and first_name like '"+b.getFirstName()+"%'");`
					- if op is search
						- by default page No = 1
							- we are giving pageNo = 1 for ex. if searched by firstName and we get 6 person named Rahul then 6th rahul will be on next page; but for ex in role admin is only 1 so it will be shown on 1 pg.
							- if we set pageNo=2 so according to formula `(pageNo - 1) * pageSize` > 5,5 but the record of admin is on 0,5 so it won't be shown
								- `sql -->select * from st_user where 1=1 and first_name like 'Rahul%' limit 5,5` returns empty list as rahul was on 0,5
									-
						- apply in all the tables.
						-
		- ==50:29==