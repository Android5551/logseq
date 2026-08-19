- [[Fri, 07-08-2026]]
	- Servlet handles http's requests and responses.
	- to create servlet
	  collapsed:: true
		- extend this `javax.servlet.http.HttpServlet` class
	- also called as controller
	- # MVC architecture
		- To create web application we need to understand an architecture called MVC
		  collapsed:: true
			- It divides application into 3 parts:
			  collapsed:: true
				- Model
					- We write following logic in model:
						- Data Access Logic
						- Business Logic
						- Use Integration logic (we don't write it)
							- like integrating google's sign in in a website where website wanted to sign up or register the user using their google account, then they take information from google and save it to their database.
					-
				- View
					- JSP
					- Presentation logic
						-
				- Controller
					- Control logic
						- Taking data from database and give it to view; take data from view and give it to database
					- Navigation logic
						-
			- Use of MVC
			  collapsed:: true
				- divides app into 3 parts.
					- no code conflict
					- less complexity
					-
				-
		- ## Flow
			- Model
				- communicates with database
			- Bean
				- for setting and getting
				- set something in bean and send it to model method
				- In test class we create bean object and set it in bean and send it to model
			- Controller
				- in controller create bean object and model's object , set the values in bean object and send it to model
				- model goes to database after that
				- if you search in model , after getting data from result set need to set in bean
					- that bean can be found in controller
			- ### The flow from view to database
				- for ex. i send `firstName` from view
					- that data or request will go to Controller, Controller set that data to bean, bean send it to model and model send it to database.
					- ### the flow from database to view
						- then the data should be viewed in view after searching first name.
							- view goes to controller for taking `firstName` data we searched for.
							- controller goes to model
							- Model sets it into bean
							- then that goes to controller.
							- controller sends that to view
							-
				- for ex. i searched `dell laptop` from view
					- that request will go to controller
					- controller knows data access logic is in model and user is asking for `dell laptop` , then controller goes to model
					- model will then take data from database and set it to bean and then send the bean to controller
					- controller sends it to view
					- View will display it.
					-
			-
		- ## 4 Guidelines
		  collapsed:: true
			- One screen has one view
				- Index page, IndexView.jsp
			- One view has one controller
				- LoginView.jsp then LoginCtl.jsp
			- View can not be accessed directly. Only accessed by its own controller
				- because we can't view a feature which comes after logging in that web application.
				- we first request from view and controller checks whether user has authorisation to do so
				- **Pages that can be accessed directly**
					- index page or welcome page can be accessed always.
					- forget password page can be accessed directly
					- header footer pages.
					- sign up page
					- login page
			- View always submit request to its own controller
				- for ex. in sign up view the data will be added.
					- because in signUpCtl  we have called model's add method.
					- in loginView we have Authenticate method for login and password to search whether user is found or not. as we need to follow mvc so all should be separated , we cant do things like in single controller we used add, authenticate etc. then it gets complicated.
					-
				-
			-
		- In advance java book
		  collapsed:: true
			- pg 169 to 173 #imp
			- project 4 follows this architecture.
		- Later we will read:
		  collapsed:: true
			- based on `Http's session`
				- Front controller -> if user hasn't login can't edit his data then the logic for that will be written here. To add security
				- Http Session -> when we visit a site and get logged in for ex. irctc after a while of idleness it often says your session has expired please login again
					- when you had login a session had generated now after sometime the session got expired, so we need login again.
					- authentications done by session
				- Managing Cookies
				- etc.
				-
		- [[Mon, 10-08-2026]]
			- Following 4 guidelines we will make a webapp
				- One screen has one view.
				  collapsed:: true
					- welcome screen
						- need one view for that like `welcomeView.jsp`
							- following is the presentation logic
								- in `welcomeView.jsp` we use `<div align="center">` to make the content inside at center otherwise it will be on left.
							- first landing page for user is welcome page
						- when some one visits our website a welcome page will open.
					- sign up screen
					  collapsed:: true
						- `userRegistration.jsp`
							- `<form>` to create form
							- to create rows for firstname , lastname , password we need to provide
								- `<table>` and `<tr>` represents table row, `<td>` represents table data where we put input data by user using `<input>`
									- `<input>` can have type of data named as `type` like text,password(which shows **)
										- input type of ~date~ has calendar so no need to have a placeholder.
										- input type of `submit`, creates button as well as we can submit the form does not have any heading as need to give a space at left
									- identification to tell what to fill here in the input field using `name` attribute.
										- this will be form's parameter name. and we use this to get value using parameter
										- we put `firstname` as parameter name for the form's heading like firstname, lastname etc. and later we can get the parameter's value using servlet's `request.getParameter("firstname")`
										- `<value>` tag where values will be stored but we give it empty because user will give as input
										- `<placeholder>` tag have a value which will be shown to user as greyed out.
										-
										-
								- `<th>` is heading of the table row
					- login screen
					  collapsed:: true
						- `LoginView.jsp`
							-
					- can run the viewjsp directly but according to protocol or guidelines it shouldn't be done.
				- One view has one controller
				  collapsed:: true
					- following will be made in `src/main/java` package `com.rays.ctl`, need to follow a standard like LoginView LoginCtl
						- `LoginCtl.java`
						- `UserRegistrationCtl.java`
						- `WelcomeCtl.java`
							- To create servlet
								- Pre-Requisites
									- We do *wildcard mapping* of servlet to access servlet.
										- by using annotation `@WebServlet` and under that we write controller's name`/WelcomeCtl`
										- Request will go from view to controller and request will only be sent when this controller has wildcard mapping. If the mapping is done then only server can access this controller otherwise gets 404 error
										-
									- `WelcomeCtl extends HttpServlet`
									  collapsed:: true
										- it needs jar file which we will place in `lib` folder named `javax.servlet-api-3.1.0.jar` you need to add it externally.
											- it will provide `javax.servlet` package.
									- override `doGet()` and `doPost()`
									  collapsed:: true
										- http's default method is GET.
											- by default request is GET. so to handle GET Request HTTP servlet gave doGet() method
											- doPost() do not run by default it runs only when we submit using view. to handle post we use doPost()
										- remove the code under the overridden methods
										  collapsed:: true
											- complete the req and resp to request and response respectively.
												- These 2 are objects.
												-
									- there is one more method named `service` but it is a lifecycle method but we dont override it. whenever request goes to server this method runs that many times.
									  collapsed:: true
										-
											-
								-
							-
				- View can only be accessed using its own controller by using `RequestDispatcher` forward()
				  collapsed:: true
					- Request comes on controller and controller forwards to view for that we need a method named as `forward()` predefined.
					  collapsed:: true
						- It is a method of `RequestDispatcher` Interface.(predefined)
							- we can make object for this interface using object of `HttpServletRequest` which returns this interface object further can be stored here.
							- pass a String type value where you want to forward i.e. the view
					- if user is not authenticated certain views can't be accessed directly. like if i want to see photos on instagram i need to login first
					  collapsed:: true
						- some views can be accessed directly like footer , header etc. are common jsp.
						- this logic will be written on controller that's why before opening view if any logic is there can be run on controller then we can display the view securely.
					- in home page , there is a controller for ex. on amazon there are products which can be seen but cant purchase without login , search method gets data from the logic written on controller. then view opens.
					- on browser instead of writing `http://localhost:8080/ORSProject-04/WelcomeView.jsp` we will write the wildcard mapping `http://localhost:8080/ORSProject-04/WelcomeCtl` exactly as written there otherwise 404
						- to not to repeat and write that again and again we use a common jsp like header.jsp and put that as link there.
							- `<a href="LoginCtl">Login</a> |`
								- after this use `<hr>` for horizontal rule.
								- we will write controllers here which we get from wildcard mapping.
								- To go to loginview we use loginctl first to get to loginview.
							- and in view.jsp except indexview use `<%@ include file="Header.jsp"%>` inside body. it is just like script let tag after that we use `@`
								- include is property and file is attribute.
								- one jsp can include another common jsp using this tag called `include directive tag`
						- to open `loginview` send request to loginctl , http request will be sent to loginctl from browser and doGet runs and forward to loginview
				- 4th guideline will only be used when we use all 3
					- when we click on submit button , all the form will be submitted on request; if we put it outside form tag then no request will be sent. so it should be under form and under table tags.
						- when we click on button from `userregistration.jsp` the form will be submitted but where should the request be sent , to its own controller.
							- for that we need to use in form tag `action` attribute having value as `userregistrationctl` its own controller, another attribute `method` having value as `post`
								- we are sending this forcefully because `post` is not default method
									- if we dont do this the request will be sent to get not post.
									- this sends `http's post` method which will be handled by doPost() when we click submit button controller's doPost() will run.
									- form is submitting 5 parameters and `doPost` will get all these 5. all these are coming in request and request is having parameter of form. so request has method called `.getParameter()` get the data from form. returns String only
										- this returns anything to string
										- getParameter() will have parameters like firstname lastname etc. then store in string object.
										- print those parameters and after printing to remain the userregistrationview to open we use this line again
										  ```java
										  RequestDispatcher rd = request.
										    getRequestDispatcher("UserRegistrationView.jsp");
										  rd.forward(request, response);
										  ```
										- In doPost() you can create userbean object
											- bean.setFirstName(firstName) and model's add method send the bean object. then db got entry