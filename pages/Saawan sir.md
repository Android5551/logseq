- [[Mon, 28-09-2026]]
  collapsed:: true
	- On clicking the link, how is this form came?
	  collapsed:: true
		- The link of `SignUp` is on `Header.jsp`
		- On clicking it the request goes to `UserRegistrationCtl`
			- there `doGet()` get called and forwarded to `UserRegistrationView.jsp`
	- How did you make this form?
	  collapsed:: true
		- We have used `form tag` and in method we wrote `POST`
	- How did you make the input fields?
	  collapsed:: true
		- We have written `input type` as text and in `name` its field name.
	- How did you make password fields?
		- `input` type as password and `name` as password
	- How many dropdowns are here and which one?
		- One dropdown and type is static.
	- How did you apply this dropdown? (Gender)
		- In `UserRegistationView.jsp` we have used `Script let` tag
			- we have created `Map's` object in following way:
				- `HashMap map = new HashMap`
			- we have passed Female, Female as key value pair in `map.put`
				- `map.put("Female", "Female");`
				  `map.put("Male", "Male");` and so on.
			- using expression tag we have called `HtmlUtility's``getList()` and passed 3 arguments
				- `String htmlList = HTMLUtility.getList("gender", bean.getGender(), map);`
				  `%> <%=htmlList%>`
					- in name -> gender
					- in selected value -> `bean.getGender()`
					- in value -> passed the map's object.
	- How did you make DOB field?
		- `input` type as date and `name` as DOB
	- How did you make the button?
		- In `UserregistrationView.jsp` i have given input type -> `Submit` , name -> operation and in value  we have used expression tag and written `UserRegistrationCtl.OP_SignUp`
		-
	- Perform the Input Validations
		- When the form's fields are empty click on `Signup`
	- Why its color is red?
		- We have defined red color for error message.
	- Why you have chosen red color for it?
		- It is standard
	- Which scope does this belong to?
		- Request's scope
	- How do you know it is in request's scope?
		- We have set it in request using `request.setAttribute()`
	- How many scopes are there
		- 4 ; request, application, page and session and by default it is page.
	- When does the request's scope ends?
		- When generating new request the older one's scope get destroyed. OR when generating the response the older one get destroyed
	- which type of messages are these?
		- Input error's messages
	- How did you set/get these input messages
		- in Userregistrationctl we have set as `request.setAttribute` in form of key and value pair; and on view using `ServletUtility.getErrorMessage` we get it in form of key and request
		- key has value which we type casted.
	- How did you perform the input validations
		- We have overridden validate method of BaseCtl in Userregistrationctl
	- How did you make this box in userregistrationview.jsp
		- using bootstrap
	- What are these red star(asterisk)
		- These are mandatory fields
	-
- [[Thu, 29-10-2026]]
	- On `Welcome.jsp` we made link of `Users`
	- on clicking that link request goes to `userlistctl`
	- `doGet()` gets called; as user list will be displayed we make `UserModel`'s object
	- to filter the data or getting the data we use Usermodel's search method
	- we will pass 3 arguments in search -> bean , pageNo and pageSize.
		- here bean is null and user's bean, pageNo->1 and pageSize->5
		- when we need to search or filter the data we set some data in bean for now we don't want that
	- search method returns list; so we hold returned list in list type variable.
		- ```java
		  public static void setList(List list, HttpServletRequest request) {
		  		request.setAttribute("list", list);
		  	}
		  
		  public static List getList(HttpServletRequest request) {
		  		return (List) request.getAttribute("list");
		  	}
		  
		  // userlistCtl
		  ServletUtility.setList(list, request);
		  // userlistview
		  int pageNo = ServletUtility.getPageNo(request);
		  int pageSize = ServletUtility.getPageSize(request);
		  int index = ((pageNo - 1) * pageSize) + 1;
		  List list = ServletUtility.getList(request);
		  Iterator<UserBean> it = list.iterator();
		  String _err = ServletUtility.getErrorMessage(request);
		  ```
		- we are doing hard-coding like in both set/get need to give its key
		- request is implicit object in jsp ; no need to create request object in jsp
			- 9 objects which are implicit in jsp
	- we pass list and request in `ServletUtility.setList(list, request)`
	- similarly for pageNo and pageSize
	- we forward the list on userlistview.jsp
	- we get the list using `ServletUtility.getList(request)` similarly all 3
	- On list we apply iterator ; use while loop iterate data using iterator; in expression tag `bean.getFirstName()` .. we print it
		- for each loop one row gets printed
	-