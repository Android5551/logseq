- [[Wed, 08.07.2026]]
	- ## Development and Operations (DevOps)
		- Daily updates of projects to client ==15:04==
		- To run a project with configs on one machine it must be done on another machine too.
		  collapsed:: true
			- make project live, so that accessed by client if it is made on local machine
				- **Problem**
					- if client need some changes:
						- in local m/c change in project
						- need to do steps again for creating live server.
						- things needed to be changed in live server too
				- **Solution**:
					- DevOps engg.  ==21:00==
						- Automates code deployment
							- Manual steps to automation for local machine project to live server
						- Writes a CI/CD ((6a4e16b1-a383-4bda-bbb6-8a6a5abeb541)) for automation
							- Scripts which needs to be done manually now done automatically -> pipeline
							- pipeline executes when a button is pressed or using event listeners
						- Steps to live the code:
							- shift code on Local machine of different location to global repo -> github
								- Store code to github
								- Send it to ((6a4e196b-bd06-4f87-9619-895395dffc95))
									-
		- Live Environment or Live Server -> AWS (Amazon web services), Azure
		- ### Git #git
			- local on machine
			- `ReadMe.md` connects local repo a.k.a. to github
			- ```
			  git init  // initialize git add .git
			  git clone https://github.com/Android5551/CoreJava.git
			  
			  git add .
			  git commit -am "ok" //m -> merge ; a -> add
			  git push // to github
			  ```
			-
			- ### Github
			  collapsed:: true
				- global or cloud repository
				- #### Uses
					- multi users can access at same time.
					- store data in cloud
					- version control
						- saves version history
				- check-in
				- check-out
		- ### Pipeline
		  id:: 6a4e16b1-a383-4bda-bbb6-8a6a5abeb541
		  collapsed:: true
			- A sequence of automated tasks that code goes through after you make changes.
				- #### CI
					- Continuous Integration
					- Automatically build and test code when changes are made.
				- #### CD
					- Continuous Delivery/Deployment
					- Automatically deliver/deploy that code.
					- Common tools:
						- Jenkins
						- GitHub Actions
		- ### Docker #docker
		  id:: 6a4e196b-bd06-4f87-9619-895395dffc95
			- virtual container
			- lessen installation of software's like java, python and configuration
			- wraps or encapsulate all applications and requirements into one container.
				- no need to do configs and installations again
				- container turn to images aka docker images
					- images are true copy of project
					  id:: 6a4e19f9-c8b5-48fb-b3ff-e5a9595d2a5e
				- #### Encapsulation
				  collapsed:: true
					- Gathering all related things to single entity
				- docker on one machine and docker on another machine to run that image
			- #### Types
				- ##### Docker Desktop
					- local machine
					- used for testing container if they are running or not
					- now it goes to hub
				- ##### Docker Hubs
					- Global
					- get tested image and run
		- ### AWS
		  collapsed:: true
			- Live server
			  collapsed:: true
				- #### Networking
					- ##### server ==35:39==
						- provides service
						- gives response to client (phone apps)
						- accessed by url
						- it has unique IP address
							- IP address uniquely identify globally; where it exists globally
					- ##### client
						- consumes service
						- client send request to server to ip and port
					- ##### Network
						- is medium of communication.( wired / wireless)
			- `URL`
			  collapsed:: true
				- Uniform Resource Locator -> locates resources
				- It consists of:
					- `http`
						- stateless protocol
							- every user request is new request
							- no sharing of data with the requests made
						- `s`
							- for security
					- `127.0.0.1`
						- IP address ( 82, jaora compound )
						- globally uniquely identify
					- `8080`
						- port (room no. A)
						- uniquely identified on IP address
						- all ports provide different services like on 8083 etc.
					- `127.0.0.1:8080`
						- called as socket
					- `URI`
						- /folder1/nested-folder1-1/page.html
						- identifies resources on that port number
				-
		- Developer work is to store code on github
		- after that all work is done by Jenkins
		- ### Jenkins ==46:50==
		  collapsed:: true
			- It integrates with code, docker, git, AWS
				- It takes code from git
				- it creates docker images of code after building the code
				- sends docker image to docker hub
				- from docker hub to aws
				- run the images to make container after pulling images on aws
				- container gives project which we wrapped and sent
			- Nowadays, Event listeners automatically start pipelines whenever you check in check out on github
				- git actions are like Jenkins
- [[Thu, 16.07.2026]]
	- [[Project-04]]
	-