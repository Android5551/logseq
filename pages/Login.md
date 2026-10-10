# Buisness Validation
	- Common
	  id:: 6ac9d196-4ff9-4525-9a26-3761131ba7a1
		- LoginForm par Sign In button par click kiya.
		  collapsed:: true
			- ```jsp
			  <tr>
			  	<th></th>
			  	<td><input type="submit" name="operation"
			  	value="<%=LoginCtl.OP_SIGNIN%>"></td>
			    <!--  OP_SIGNIN = "SignIn"; -->
			  </tr>
			  ```
		- Form tag me:
		  collapsed:: true
		  `<form action="<%=ORSView.LOGIN_CTL%>" method="post">`
			- `String APP_CONTEXT = "/ORSProject-04";`
			- `String LOGIN_CTL = APP_CONTEXT + "/LoginCtl";`
			- LoginCtl ne baseCtl ko extend kiya hai ; basectl ki service method chalegi; if condition me `request.getMethod()` se method get karenge aur check karenge ki wo POST hai AND fir validate(request) method chalegi jise humne baseCtl me banaya h aur loginctl ne basectl ko extend kiya hai to loginctl ki validate chalegi ; humne pass ko true set kiya hai aur login password ko check karenge ki data null to nahi hai
				- hum utility class `DataValidator` ki `isnull` me `request.getParameter` ka use karke view se login check karenge ki data null hai kya aur request me message set kardenge `login, login is required`
				- aur pass ki value false
				- isi tarah password
				- fir `return` true hoga kyunki values null ni hain.
				- to `basectl` me service method me condition false ho jayegi
				- `super.service(request, response);` ye chalegi aur basectl ki doPost chalegi par humne loginctl pe override kiya h
		- `doPost()` method chali `doPost()` method me operation ko get kiya view se:
		  collapsed:: true
		  `String op = DataUtility.getString(request.getParameter("operation"));`
			- `DataUtility.getString()` check karegi ki `SignIn` `isnonull` using DataValidator uske bad wo whitespace trim karke return kar degi par agar null hui to wo operation as it is return kar degi.
		- `populateBean(request)` method call ki aur view se Login aur Password
		  collapsed:: true
		  get kiya or UserBean me set kiya. `request.getParameter()` method se
			- ```java
			  @Override
			  	protected UserBean populateBean(HttpServletRequest r) {
			  		UserBean b = new UserBean();
			  		b.setLogin(DataUtility.getString(r.getParameter("login")));
			  		b.setPassword(DataUtility.getString(r.getParameter("password")));
			  
			  		return b;
			  	}
			  ```
			- `populateBean(HttpServletRequest r)` ko basectl me banaya h aur loginctl me override kiya hai
				- populateBean me UserBean ka naya object banaya hai ; `request.getParameter`  se login ko view se get kiya hai Datautility ki `getString()` me pass kiya hai ye check karti hai ki login aur password null to ni hain agar ni hain to whitespaces trim karke return krti hai.
				- fir parameters ko get karke bean me se set kar dete hain.
				- fir bean ko return kar denge.
			- `UserModel`, `RoleModel` aur `Session` ka object banaya
				- `HttpSession s = req.getSession();`
				-
		- Condition check hui:
		  collapsed:: true
		  `if(OP_SIGN_IN.equalsIgnoreCase(op))`
			- `SignIn` op ke barabar hai ki ni.
			- `equalsIgnoreCase` case insensitive hota hai
		- UserModel ki `authenticate()` method call hui:
		  collapsed:: true
		  `bean = m.authenticate(bean.getLogin(), bean.getPassword());`
			- `bean.getLogin()` -> UserBean me `populateBean` se login aur password get kiya.
			- ```java
			  public UserBean authenticate(String login, String password) {
			  
			  		UserBean bean = findByLogin(login); //select * from st_user where login = "ram@gmail.com"
			  
			  		if (bean != null && bean.getPassword().equals(password)) {
			  			return bean;
			  		}
			  		return null;
			  
			  	}
			  ```
				- `findByLogin` me view se jo login ka data get kiya tha wo pass kiya jaise ki `ram@gmail.com`
				- fir `findByLogin` ki `findByUniqueColumn` chali usme (columnName , value) ke pair me arguments pass kiya for ex. "login", ram@gmail.com
				- `findByUniqueColumn` hmne BaseModel me banai hai
				- to usme query chalegi `select * from st_user where login = ram@gmail.com` usse pura data ram ka including `role_id` first last name etc. aa jayga aur UserBean k bean me set hoke `finByLogin` ko return hojayga jise hum `authenticate` ki bean me set kar denge.
				- fir check karenge if condition se ki bean null ni hona chaiye aur `bean.getPassword` jo ki humne st_user se liya tha aur `password` jo humne view se liya tha wo same hona chaiye to bean return kar lenge. ni to null return hoga.
				-
	- authenticate() method ne null bean return kiya login or password galat tha isliye.
	  condtion chek hui `bean == null`  hua to:
	  `ServletUtility.setErrorMessage("Invalid login or password", request)`
	  se error message request me set kiya.
		- ### ServletUtility
		  collapsed:: true
			- ```java
			  
			  	public static String getErrorMessage(HttpServletRequest request) {
			  
			  		String errorMsg = (String) request.getAttribute("errorMsg");
			  
			  		if (errorMsg != null) {
			  			return errorMsg;
			  		}
			  		return "";
			  	}
			  
			  	public static void setErrorMessage(String msg, HttpServletRequest request) {
			  		request.setAttribute("errorMsg", msg);
			  	}
			  
			  	public static String getSuccesMessage(HttpServletRequest request) {
			  
			  		String succMsg = (String) request.getAttribute("succMsg");
			  
			  		if (succMsg != null) {
			  			return succMsg;
			  		}
			  		return "";
			  	}
			  
			  	public static void setSuccMessage(String msg, HttpServletRequest request) {
			  		request.setAttribute("succMsg", msg);
			  	}
			  
			  ```
	- Uske baad:
	  collapsed:: true
	  `ServletUtility.forward(getView(), request, response)`
	  se Login view par forward kiya.
		- `getView()`
			- `ORSView.LOGIN_VIEW;`
			- `PAGE_FOLDER = "/jsp";`
			- `LOGIN_VIEW = PAGE_FOLDER + "/LoginView.jsp";`
	- View par:
	  collapsed:: true
	  `ServletUtility.getErrorMessage(request)`
	  se "Invalid login or password" message get kiya aur
	  expression tag me print kiya.
		- ```jsp
		  <h3 style="color:green"><%=succ %></h3>
		  <h3 style="color:red"><%=err %></h3>
		  ```
	- Isse "Invalid login or password" ka business validation
	  message show hota hai.
- # Successful Login
	- ((6ac9d196-4ff9-4525-9a26-3761131ba7a1))
	- `authenticate()` method ne bean return kiya.
	- Agar `bean != null` hua to
	  User session me set kiya. `session.setAttribute("user", bean)`
	- RoleModel se user ka role nikala.
		- `RoleBean rb = rolemodel.findByPk(b.getRoleId());`
			- `findByPk` hmne BaseModel me banai hai.
			- query chalegi `select * from st_role where id=?` role_id jo humne userbean se li thi wo `?` me daal di. jo bhi role_id ho uski.
				- to hume `id`, `name` aur `description` mil jayenge.
	- Role bhi session me set kiya.`session.setAttribute("role", rbean.getName())`
	- `ServletUtility.redirect(ORSView.WELCOME_CTL, request, response)` se Welcome page par redirect kiya.
		- `WELCOME_CTL = APP_CONTEXT + "/WelcomeCtl";`
		- `APP_CONTEXT = "/ORSProject-04";`
		- `Header.jsp` pe `UserBean user = (UserBean) session.getAttribute("user");` session me get kiya `user` key ko aur value ko UserBean me typecast kar ke user me hold kiya
			- `String role = (String) session.getAttribute("role");` session me role ki value ko jo ki `role.getName()` tha use String me typecast kar ke role me hold kiya
			- `boolean isLogin = user != null;` isLogin me user not null hona chaiye.
			- agar user login hai ya user null  ni hai to `<%=welcomeMsg + user.getFirstName() + " (" + role + ")"%>` expression tag me user ka firstname aur role bracket me display ho jayga
			- aur logout ke liye `<a href="<%=ORSView.LOGIN_CTL + "?operation=logout"%>">Logout</a> |`
				- anchor tag ke href attribute me `query string` me operation logout diya hai
				- jise humne loginctl ke doget me iss operation ko `request.getparameter()` se get kiya `op ` me
				- condition di ki agar op null ni hai to session ka object bana ke session ki invalidate method call kiya jisse session destroy ho gya
				- `ServletUtility.forward()` se login view pe forward kar diya
				-
- # Input Validation
	- LoginForm par Sign In button par click kiya.
	  collapsed:: true
		- ```jsp
		  <tr>
		  	<th></th>
		  	<td><input type="submit" name="operation"
		  	value="<%=LoginCtl.OP_SIGNIN%>"></td>
		    <!--  OP_SIGNIN = "SignIn"; -->
		  </tr>
		  ```
	- Form tag me:
	  collapsed:: true
	  `<form action="<%=ORSView.LOGIN_CTL%>" method="post">`
		- `String APP_CONTEXT = "/ORSProject-04";`
		- `String LOGIN_CTL = APP_CONTEXT + "/LoginCtl";`
		- LoginCtl ne baseCtl ko extend kiya hai ; basectl ki service method chalegi; if condition me `request.getMethod()` se method get karenge aur check karenge ki wo POST hai AND fir validate(request) method chalegi jise humne baseCtl me banaya h aur loginctl ne basectl ko extend kiya hai to loginctl ki validate chalegi ; humne pass ko true set kiya hai aur login password ko check karenge ki data null to nahi hai
			- hum utility class `DataValidator` ki `isnull` me `request.getParameter` ka use karke view se login check karenge ki data null hai kya aur request me message set kardenge `login, login is required`
			- aur pass ki value false
			- isi tarah password
			- fir `return` true hoga kyunki values null ni hain.
			- to `basectl` me service method me condition false ho jayegi
			- `super.service(request, response);` ye chalegi aur basectl ki doPost chalegi par humne loginctl pe override kiya h
	- Request `LoginCtl` par gayi aur sabse pehle `BaseCtl` ki `service()` method call hui.
	  Condition di:
	- Agar`if("POST".equals(request.getMethod()))`  hai,
	  to `validate(request)` method call hui.
	  `validate()` method child class (LoginCtl) ki call hui
	  (method overriding).
	- validate() method (LoginCtl me) me Login aur Password ko
	  DataValidator ki methods se check kiya.
	- Login ko check kiya:
	  `if(DataValidator.isNull(request.getParameter("login")))` hai, to
	  `pass = false` kiya aur request attribute me key aur value ke
	  saath error message set kiya.
	- Same process Password ke liye bhi hua.
	- service() method me validate() wali condition true hui
	  aur view par forward kiya:
	  `ServletUtility.forward(getView(), request, response)`
	- View par `ServletUtility.getErrorMessage()` se key aur request ke
	  through message get kiya aur expression tag me print kiya:
	  `ServletUtility.getErrorMessage("key", request)`
	- Isse error messages show hote hain.