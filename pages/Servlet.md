- [[Fri, 07-08-2026]]
  collapsed:: true
	- Servlet handles http's requests and responses.
	- to create servlet
	  collapsed:: true
		- extend this `javax.servlet.http.HttpServlet` class
	- also called as controller
	- # MVC architecture
	  collapsed:: true
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
			  collapsed:: true
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
- [[Tue, 18-08-2026]]
  collapsed:: true
	- in userregistration.ctl
	  collapsed:: true
		- when user submits doPost runs
			- request.getparameter takes all the parameters one by one from form.
			- set all in bean and pass to model
			- `request.setAttribute("successMsg", "user registration successfully");
				- request has this predefined method
				- has key named `successmsg` and value as `user registrat...`
					- value is string type.
				- `ServletUtility.forward("UserRegistrationView.jsp", request, response);`
					- forwards or sends the request, response to userreg....view
					- setAttribute -> sets key and value
					- getAttribute -> gets key only
						- as value of setAttribute is String type
						- request.getAttribute("successMsg") and return type of this is Object we need to typecast it to string and save in string obj
						- then in `userregistrationview.jsp`
							- ### Ternary operator
								- ternary operator `?`
									- `<h3 style="color: green"><%=succ != null ? succ : ""%></h3>`
										- if succ is not null and having msg then print it otherwise nothing will print.
								- if add's bean is null or login already exists then flow goes to catch and errormsg will print.
									- `style="color: green"` in heading tag to make it color red or green
							- So **whether registration succeeds or fails, the forward to view runs**.
							- `response` → gives the JSP the **response object** that it will use to send the final output to the browser.
	- `loginCtl`
		- once you entered login and password
		  collapsed:: true
			- check whether this login password has record in database.
			- if it is there then login and session should be generated.
			- And in that session store user information
			- The user will remain logged in as long as their information is stored in the session.
				- once the session gets destroyed the user will be logged out.
		- if user is logged in , its state will be stored in `session`
		- request, response and session are http
		- ### why http request is stateless.
		  collapsed:: true
			- when we signup and added the user, got message user register successfully , this we set in request, we forward the request and got in view .
			- similarly when we click on login page , request got changed and message got disappeared from previous request
			- not permanent because new request gets generated. when new one generated http forgets older ones. if it doesnt do that then no website will run because it gets billions of requests.
		- so this caused new problem for ex if user has logged in and accessed new page hence new request gets generated and forgots the previous request and he gets logged out.
		  collapsed:: true
			- for this issue http gave ~session~
			- ### Session
				- it is not stateless
				- gets stored in user's browser
					- user's state got stored in session
				- http go on checking if session is in browser or not, if session got removed from browser user gets logged out.
			- user messages like error or success or a temporary value is for a particular event so can be stored in request attribute. this is for certain amount of time once user gives new request the older one gets removed.
		- so when we use login and password , searched user record will be saved to session
			- submit the form with login and password in view and the request goes to its own controller.
			- action -> loginCtl, method -> post
			- now it gets the login and password and take it to doPost
			- create objects of bean,session and model
				- `HttpSession session = request.getSession();`
					- HttpSession is an interface.
					- request.getSession() gives HttpSession's object.
			- call model's authenticate method
				- checks if login exists and the database password and user input's password match then save it to bean
				- bean is not null if it is right
					- set the bean to session attribute using `setAtrribute` and key value pair of user and bean
					- else otherwise bean will be null then set attribute of request to errormsg.
						- forward to loginview
						- get it in loginview using
						  collapsed:: true
							- `<h3 style="color: red"><%=err != null ? err : ""%></h3>
							  			<h3 style="color: green"><%=succ != null ? succ : ""%></h3>`
								- as per the null values get the message if login or password is correct.
					- if we put login and password correct.
						- bean will store in session as this session is not stateless, No matter how many times you change on requests, session won't change.`
							- `session.getAtribute` gets the bean of type userbean.
							- whatever the value type is cast to that in getAttribute in header as it will be common to all.
								- `UserBean user = (UserBean) session.getAttribute("user");`
						- if user gets logged in then what we want it its firstname get displayed in welcome page in brackets.
							- include header.jsp in welcomeview.
							- `Welcome To Online Result System<%=user != null ? "(" + user.getFirstName() + ")" : ""%></h1>`
							- if you close the server. browser's session got expired and need to login again
								- to check if session expired or not or whether he is guest. in header.jsp
									- ```jsp
									  <%
									  	if (user != null) {
									  	%>
									  	<h2><%="Hii, " + user.getFirstName()%></h2>
									  	<a href="LoginCtl?operation=logout">logout</a> |
									  	<%
									  	} else {
									  	%>
									  	<h2>Hi, Guest</h2>
									  <a href="LoginCtl">Login</a> |
									  	<a href="UserRegistrationCtl">SignUp</a> |
									  	<%
									  	}
									  	%>
									  ```
									- after logging in we wont show in header the signup and login instead we will show `logout` link having following
										- ### Query String
										  collapsed:: true
											- `?` -> we can send parameters in url using this.
											- parameter=value.
										- session destroyer:
											- remove user from session
												- send it to loginctl and in query string use operation=logout.
												- loginCtl's do get will run because it is link.
												- in loginctl
													- `String op = request.getParameter("operation");`
													- if it is not null then invalidate the session
														- session.invalidate();// invalidate method use to destroy session attribute
															- destroys the session attributed named user.
															- then session where ever you used getsession it gets false
												- forward to loginview.jsp that user logged out successfully
									- is user is null then guest otherwise username.
									- if user clicked on `login` flow goes to LoginCtl but as we didnt pass parameter in url it doesnt get op and doesnot go to condition. only forwards to loginview.
									- after logout we will show
						-
						-
						- user gets logged in then redirect him to welcome page.
							- now the new request will be sent from login ctl to welcomectl which in turn goes to welcomeview using forward in doget.
							- `redirect`
								- when we send request from one controller to another.
			-
			- get the parameter from form in view to controller using `.getParameter`
			-
- [[Wed, 19-08-2026]]
  collapsed:: true
	- if i put existing user in signup page with all his details
	  collapsed:: true
		- this will throw`throw new RuntimeException("loginId already exists");`
		- then it will go to catch block of userregctl  and print error msg and forward it to view of userreg.
		- ### Execution Flow when user gives details in signup which already exists
		  collapsed:: true
			- doPost method will run of userregctl,
			- get all parameters from request.getparameter
			- set in bean
			- add bean in model's add method
			- in model's add method `findbylogin` will run and existbean != null throws error
			- then comes in controller userregctl goes to catch block and sets the attribute of error msg , forwards to userregview
			- gets on view using getAttribute and ternary operator print the error msg.
	- ## Business validation
	  collapsed:: true
		- checks if data exists or not in database.
		- Login already exists. this message is called validation message. comes from business logic this is called `business validation.`
		  collapsed:: true
			- can't give same login id.
			- checks in database whether loginId already exist running findbylogin()
				- Business logic checks whether data is already present or not
					- findbylogin
					- authenticate
					- findbypk
					- These are business validations.
			- if someone ask have you applied business validations in signup?
				- i have applied it on login field using findbylogin() if login details already exist then runtime exception otherwise adding the login details in db
				-
		- if i give wrong details in login then it checks from authenticate()
		  collapsed:: true
			- clicked on signin ; then flow goes to loginctl's dopost
			- `bean = model.authenticate(login, password);`
				- bean gets null because record not found then it goes to else and sets error msg
				- this is also a business validation
		- another example is once a role is added cant add same role again
			- findbyrolename()
		- marksheet cant add same rollno again.
			- findbyrollno()
	- ## Input validation
	  collapsed:: true
		- take right input from user.
			- for ex. i write integer in firstname lastname which is invalid.
		- input Data should be checked before going to doPost to check whether input given by user is correct or not before setting it to bean as it gets to add method.
			- Now we need `httpservlet's service()`
				- gets called in every request.
				- after that whether doget runs or dopost.
				- so here we can write out input validation logic
				- it is a lifecycle method , it gets called on its own once a request happens
		- `InputValidatorUtility`
			- checks input data
			- it will validate 2 parameters in login and 5 parameters in signup
			- returns true or false in boolean
			- default value in pass is true. and returning pass which will be boolean type
			- if a word is "" means length is 0 but if nothing taken in word its length is not defined. and gives null pointer exception
				- if login behaves like that then pass turns to false.
				- and set msg attribute to login is required.
			- we can go for same in password
			- can add same for password's length like not less than 8 and not more than 12; for or use || go to loginctl
		- `LoginCtl`
			- override service method
			- print method of request whether it is post or get
			- the following code should only run when `request.getMethod` is post i.e. ==`.equalsIgnoreCase("POST")` -> this is case insensitve whether its post or POST== or when user submits because when you submit then only data will be sent. if we click link then doGet runs then this should not run eg. if `request.getMethod` is GET. It should not run ie. the below code.
				- check if `InputValidatorUtility.loginValidator(request) == false` then forward the request to loginview
				- after that write return so code wont run after that.
				- when user submits after the usual flow it gets to service method if either of the login or password gets false then returns false
					- if false forward it to view and
						- `<td style="color: red"><%=request.getAttribute("login") != null ? request.getAttribute("login") : ""%></td>`
						- gives login is required.
						- request.getAttribute("login") prints directly in expression tag without typecasting it.
						-
			-
	- ## Task
		- create a class `UserValidator`
			- firstname, lastname, dob , login, password
				- userreg fname and lname give 2 validation one is null one and it should not have number. create a method in uservalidator
			- `userregctl` overrides service method
				- in forward userreg.
			- print attribute below firstname etc. in `userregview`
				-
				-
- [[Thu, 20-08-2026]]
  collapsed:: true
	- when we click login without filling anything
	  collapsed:: true
		- in `LoginView.jsp`
		  collapsed:: true
			- according to guideline 4 the request will go to view's own controller after submitting form
			- action -> its own controller, method -> post
		- in `LoginCtl`
		  collapsed:: true
			- in loginctl we have overridden `service` method , whatever the request is first of all service method will run;
			- 3 life-cycle methods
			  collapsed:: true
				- init -> when httpservlet made then it runs
				- service method keep on running whatever the request type is.
				- destroy -> when server gets stopped.
			- request having login and password parameters.
			  collapsed:: true
				- as request method is post this condition gets true
					- `if (request.getMethod().equalsIgnoreCase("POST")) {`
						- `loginValidator` has same request i.e. login and password parameters.
						- it checks whether login and password is correct or not.
						- in `InputValidatorUtility`
							- empty login and password saved in String login and password
							- as for login the condition is true
								- pass gets false
								- and we set attribute of login to `login is required.`
								- we did not permit it to go to `doPost` instead we forward it from here to View.
							- similarly for password
						- if not correct return false then it forwards to view and the code ends.
					- if returns true then doPost will run and data gets checked from database using `authenticate`
		- in `LoginView`
		  collapsed:: true
			- `<td style="color: red"><%=request.getAttribute("login") != null ? request.getAttribute("login") : ""%></td>`
				- using this in view we can print the value of login and similarly for password that *login is required*
				- we can shorten the above command too so that no need to type cast if we use a variable etc.
					- go to `ServletUtility`
					  collapsed:: true
						- create `getErrorMessage()`
							- 2 parameters -> String key and HttpservletGetRequest request
							- `String val = (String) request.getAttribute(key);`
								- gets the key from login or password from `setAttribute`
								- we need to typecast here because `request.getAttribute(key)` returns Object type value
								- if value is not null return val otherwise "" string.
					- and in Loginview inside `<%=ServletUtility.getErrorMessage(key,request)%>`
					- this will be stored in util package to centralise the code, no need to run it repeatedly.
				-
					-
	- ## User List
	  collapsed:: true
		-
		- if i am admin and want to see `UserList` how many users we have in our webapp
		  collapsed:: true
			- in header we should have a User list link on clicking it , searches the database and prints the list in admin's login
			- need to create view and controller.
		- the code
			- can create servlet directly
				- new > Servlet > Next x2 > checkboxes inheritance, doget and dopost
			- in `UserListCtl`
			  collapsed:: true
				- no need to override service method
					- because we get list ; we are not sending the data so no need to check or use input validation
				- call doget
					- create objects of model and bean
					- call model object's search method with parameters bean object as search filter, page no. and no. of rows
						- search gives a list of bean objects store it in List of type userbean
						- total records or rows according to parameter set in no. of rows
						- send it to view and using iterator display on view
						- use `setAttribute` to send values of key from controller to view.
							- key is "list" and value is List object having search records in list form
							- set the list in request.
						- get from view and iterate
					- forward to `UserListView.jsp`
				-
			- In `header.jsp`
			  collapsed:: true
				- if `user` is not null or logged in
				- add userListctl link in header. named as User List
				- if we click it userlistctl will run and using doget forwards to userlistview i.e. on userlist page
			- in `UserListView`
			  collapsed:: true
				- using include directory in header and footer.
				- when using `request.getAttribute` to get the key we need to typecast it to list
				- use iterator object to display list one by one.
				- in table tag use border to give border to table like 1px and width to enlarge or increase width of the table in %
					- use table row 1
					- with style tag for giving bgcolor of table's heading
						- a table heading like as per table's column name
					- use table row 2 inside while loop
						- use while loop like we do in iterator, while loop will run as per no. of rows given in model's search parameter.
						- table row use properties like `align=center` to get contents aligned at center and `background-color` . the heading comes at center by default.
							- tr with td will be inside while loop
							- in td use `bean.usegettermethodofallcolumnname`
							- one by one for each row.
							- here we have use expression tag instead of `syso`
							-
							-
				-
			- later we will create
			  collapsed:: true
				- following in doPost()
					- next/previous button
						- if page is 1 then changed to 2 once we use next button
						- (2 - 1) * 5 = 5 -> 5,5 limit
						- click on next and it gives value page no. and increment the page value.
					- checkbox to delete a row.
						- in delete we give id.
			-
		-
		-
		-
	- ## Add user
	  collapsed:: true
		- using signup user gets added but the user who wants to be added to get to use login
		- admin can add new user on this view. Only admin can do this so set the role if you want.(Optional for now)
		- `UserView`
			- userview.jsp will be same as userregistration just change the userctl i.e. controller name
			- button value save from signup
			- change heading to add user.
			- add a header page link
		- `UserCtl`
			- change forward to `userview.jsp` in both dopost and doGet
		- `header.jsp`
			- after logging in
				- `<a href="UserCtl">Add User</a> |`
		-
			-
	- **Task**
	  collapsed:: true
		- for ex. Product module follow the following
			- create bean, add update delete etc.
			- create product list and add product for admin after logging in only
				- while adding the product do both *business validation* and *input validation*
					- business validation
						- same product id should not be added in database. use `findbyproductid`
					- input validation
						- when user don't give input ; error msg should print like `this field required`
				- add the product from view
				- view to controller
				- set in controller as bean and send to model and added to product list.
			- instead of creating test for testing methods of model.
				- use controller and jsp