- [[Mon, 07-09-2026]] (kanak)
  collapsed:: true
	- ## Two Types of Validations
		- ### Server side
			- #### Programmative
				- We use this
				- Because we are doing programs
				- Ex
				  collapsed:: true
					- ```java
					  if (age < 18) {
					      throw new Error("Must be 18+");
					  }
					  ```
				- 2 Types:
					- ##### Input Validation
						-
					- ##### Business Validation
				-
			- #### Declarative
				- We define the rules, and the  ((6aa0ad47-4309-4c5f-8b5d-e265769c54d4)) checks them automatically.
				- Framework
				  id:: 6aa0ad47-4309-4c5f-8b5d-e265769c54d4
					- a ready-made structure/tool that helps you build programs.
					  id:: 6aa0ad0c-e0a5-42e6-af22-7bbd67cb08a5
				- Ex
					- ```html
					  <input type="email" required>
					  // required -> this field can't be empty
					  // the value must look like an email
					  ```
				-
			-
		- ### Client Side
			- having javascript
			- not stable
	- ## Why GET runs on clicking link
		- #+BEGIN_NOTE
		  clicking on link -> View Logic
		  #+END_NOTE
		- by default get runs
	- ## Input Validation and Business Validation
		- when we click on a button ; views own controller will run and `baseCtl's` `service` method runs
		- for the rest follow the input validation flow.
		- #+BEGIN_NOTE
		  - null sign in -> input validation
		  - communicating with database -> business validation
		  #+END_NOTE
		- ### Input
			- when user inputs the data , input validation checks for that;
			- setting key , value of error using `request.setAttribute` getting error message on view using `ServletUtility.setErrorMsg` in the form of message in key, request.
		- ### Business
			- checks the data when there is communication with database.
			- when input validations conditions are true then only business validation runs
			- when `doPost()` runs then only business validation runs
			- set error using `ServletUtility.setErrorMsg` and get using `ServletUtility.getErrorMsg` in form of request
		-
	- ## 4 Scopes
		- #### Application
		- #### Session
		- #### Request
		- #### Page
	- ## while doing input validations the message shown on login page are in which scope
		- it is in request scope because when we set the messages it was like `request.setAttribute`
		- if we refresh the page then request gets changed and messages will be removed
	- ## Why Service method Runs?
	  collapsed:: true
		- Runs on every user request.
	- #+BEGIN_TIP
	  - the validate method and its conditions in `loginCtl` only say it when input validations message coming on `loginView`
	  - when we are saying login flow then we won't say this one. we say `doPost` one
	  #+END_TIP
	- ## How to get Data from view to controller
		- `request.getParameter`
	- ## Query for Authenticate
		- ```sql
		  SELECT * FROM st_user WHERE login='<login_value>'
		  ```
	- ## Flow of successful login
		- **Why we set bean in  session?**
		  logseq.order-list-type:: number
			- the user data we need to set in session's scope like if session got expired then user gets logged out.
		- **What does forward() do**
		  logseq.order-list-type:: number
			- carries the same request to view.
		- **What does redirect do**
		  logseq.order-list-type:: number
			- generates new request. does not carry older data.
			- here we want is if login and password are correct and gets logged in redirect to `WelcomeCtl`
			- to go from one controller to another.
- [[Tue, 08-09-2026]] (K)
	- Localhost
	  logseq.order-list-type:: number
		- your computer acting as a server.
	- When we click on login button which logic we used?
	  logseq.order-list-type:: number
		- Submit Logic
	- logseq.order-list-type:: number
-