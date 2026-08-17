- [[Wed, 05-08-2026]]
  collapsed:: true
	- java server page
	  collapsed:: true
		- can write `html` as well as `java` code in .jsp
			- html has tags
		- it can be seen on server
		- to make ui we use `HTML`
	- why we use JSP and Servlet
	  collapsed:: true
		- to make web application in java
			- web application
				- application which can be accessed by web
				- can be accessed by browser
				- web pages are accessed by URLs
					- URI identifies which web page you have accessed.
						- `https://www.raystec.com/tutorials.html`
							- tutorials.html -> uri
							- www.raystec.com -> domain name can have hostname or ipaddress can have port no. of server.
								- These are called socket
									- domain name
									- hostname
									- ip address
									- port no
							- Socket + URI -> URL
				- when web client a.k.a. browser communicates with web server like tomcat is called networking
					- runs on server
						- if server is not working then web app won't work
					- browser sends request to web application
						- like searching for a certain product in amazon
						- the request goes to web server then goes to jsp/servlet
						- then response goes to browser whether its available or not
							- the response we get is dynamic
								- like 404 when page not found
								- if found that page can be displayed
					- HTTP
						- request sent from browser is http request
						- response from server is http response
	- servlet handles http request and response
		- servlets are java classes
		- when we create web application we need to integrate server like tomcat
		-
	- in jsp we make views
	- Servers developed and maintained by java from oracle
		- Ex
			- wild-fly previously called JBOSE
			- Apache tomcat
	- ### Steps to create webProject
		- File
		  collapsed:: true
			-
			- New
				- Dynamic Web Project
					- give project name
					- Target Runtime
						- v9
					- Dynamic web module version
						- 3.0 for tomcat 9 otherwise if using tomcat 9+ go for whatever comes
				- Next
				- `src/main/java` -> here servlets will be created.
				- Next
				- Web Module
					- `src/main/webapp` -> here jsp will be created
					- Must click checkbox `Generate web.xml deployment descriptor`
						- *web app won't run without this*
						- Finish
			-
			-
	- After creating project
		- go to webapp
			- WEB-INF
			  collapsed:: true
				- lib
					- in normal java project we add jar files in classpath
					- but in web project we add jar files in lib folder
					-
				- web.xml
					- web.xml is generated from the step where we had clicked the checkbox
					- go to `/tesst/src/main/webapp/WEB-INF/web.xml`
					- XML -> xtensible markup language
					- it has some default configuration
					- delete everything except
						- ```jsp
						  <welcome-file-list>
						    
						      <welcome-file>index.jsp</welcome-file>
						     
						    </welcome-file-list>
						  ```
		- right click on webapp
			- create new jsp page called index.jsp
			- run on server
		- index.jsp will be opened by default because
			- in welcome file we have given
			- and this file runs whenever we run this app
			-
		-
	-
- [[Fri, 07-08-2026]]
  collapsed:: true
	- if you run from project root folder it will run index.jsp on server
		- because it is said so in ` <welcome-file>index.jsp</welcome-file>`
	- to run new_page.jsp
		- just run the server and after root-folder name use /file_name.jsp to view
	- we can write html as well as java code in jsp
		- can print java variable or java object
		- to use java code we need to use
			- `script let` tag , use it inside `body` tag
			  collapsed:: true
				- ```jsp
				  <%
				      // Java code
				  %>
				  ```
				- ex.
					- ```jsp
					  <%for(int i=0;i<=10;i++) {%> // must stop here to write html code
					  <h1><%=i%> hello world</h1>
					  
					  <%} %>
					  ```
						- here `for` is inside script let
						- and its closing bracket is inside script let
							- as we can't put html code in script let tag
						- `i` using expression tag prints 0 to 10
						- in between we use html
			- `expression tag`
			  collapsed:: true
				- ```jsp
				  <%= ... %> 
				  ```
				- to print variable or object in jsp.
				-
			- `Ctrl+Shift+/` for commenting
				- `<!--  -- >`
		-
			-