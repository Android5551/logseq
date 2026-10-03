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
  collapsed:: true
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
- [[Thu, 01-10-2026]]
	- # next
		- ## UserListCtl
			- if page no. is 1 then limit will be (0,10) initially 10 records will be shown( 0 to 9)
			- similarly following the formula `(pageNo - 1) * pageSize`
				- | Page | Limit |
				  |------|-------|
				  | 1    | `limit(0,10)` |
				  | 2    | `limit(10,10)` |
				  | 3    | `limit(20,10)` |
				  | 4    | `limit(30,10)` |
			- On clicking `next` it should display next 10 records.
			- so it should be like , on clicking `next` the pageNo should increase from 1 to 2
			- ### Why we have sent pageNo and pageSize on view from UserListCtl
				- PageSize is needed to disable `Next`
				- PageNo is needed to get  current pageNo's value on controller.
				- Suppose we have clicked `Next` button and we didn't sent pageNo and pageSize from UserCtl
					- Method `doPOST` will be called; operation is `next` then we increment pageNo by 1 and we get next 10 records; currently pageNo is 2
					- on clicking next button again the pageNo should change to 3 but if we don't exchange the pageNo values among controller and view the pageNo will remain 2
						- the controller don't know what was the last pageNo ; it knows only about the pageNo value is 1
						- so we need to exchange the pageNo from Controller to view then View to Controller.
							- ### How it can be done
								- When we clicked `Next` first time ; 1 will be stored in pageNo
								- when we clicked `Next` again ; we get the older 1 and increment it.
								- take the updated value and store
						-
				-
				-
			- We need current pageNo to do both `previous` and `next`
			- when we send the request it gets the pageNo. and updated one we get on controller.
			- ### Use of PageNo
				- to get current page no.
					- page no. exchange
				- for serial no.
					- index = (pageNo -1 )* pageSize +1
				- To disable/enable previous
					- we applied condition if pageNo = = 1 to disable previous
				- To disable next
					- if list size < page size
				-
			- ### Flow
				- **We have passed the page number and page size to the view**
				- We made a hidden field and in that we stored/hold pageNo in expression tag
				  collapsed:: true
					- `ServletUtility.getPageNo` from this we stored in hidden field
					- How we made hidden field ( don't tell in flow)
						- By giving input type as hidden; name -> pageNo, value=`<%=PageNo%>`
						- Similarly for pageSize(but don't tell in flow)
				- We made a button for `next` and clicked it.
					- If asked How we have made it
						- input type = submit, name = operation , value= `<%=UserListCtl.OP_Next%>`
				- Request goes to `UserListCtl`, method will be Post. hence `UserListCtl`'s doPost will be called
				- get operation in `UserListCtl` ; the operation is `Next`
				- get pageNo
				- increment the pageNo or ++
				- Same for Previous. just decrement the pageNo and operation is `Previous`
					- Sql query `SELECT st_user WHERE 1=1 LIMIT(0,10)` on clicking next limit will be (10,10) -> 10 to 19
					- for page 4 limit(30,10) record displayed 30 to 39
			- ### When next and previous got disabled
			  collapsed:: true
				- Previous -> pageNo == 1
				- Next -> Size of List < PageSize
					- | List |<| Pg |T/F
					  |------|----|----|
					  | 6 |<    |10|   T    |
					  | 10 | <  |10|  F     |
					- if 6 < 10 then next will be disabled.
					- if 10 records are there on page 1 and no 11th one on the next page. Then 10<10 is false. Next will be enabled.
						- To fix this bug
							- we used nextListSize
							- For that we need to search the current page records as well as next page record and find its size ; if it's size is 0 it means no records on the next page.
								- In first search we used `model.search(bean, 1, 10)`
								- use one more search below that add pageNo+1 and name it nextList and get its size; if size is 0; then no record is on page 2 and forward it to view if nextListSize is 0 then make `Next` disable
					-
			- Populate
			  id:: 6abf2f50-99b1-470a-ad24-538055a6b39c
			  collapsed:: true
				- getting the data from the request and setting it  to the bean.
				- ```java
				  @Override
				  	protected UserBean populateBean(HttpServletRequest request) {
				  
				  		UserBean bean = new UserBean();
				  
				  		bean.setId(DataUtility.getLong(request.getParameter("id")));
				        return bean;
				  	}
				  ```
				- bean.setFirstName(DataUtility.getString(request.getParameter("firstName")));`
			- ### How have you applied these search filters / How can we add a new search filter?
			  collapsed:: true
				- Flow Hinglish
				  collapsed:: true
					- ```
					  1. User List View me input field banai, jisme `input` type `text` aur `name="firstName"` diya.
					  
					  2. Ek `input` type me `submit` banaya jiska `name="operation"` rakha aur `value="UserListCtl.OP_SEARCH"` diya.
					  
					  3. Request `UserListCtl` ki `doPost` method pr gai.
					  
					  4. Request parameters ko UserBean me `populateBean` method se populate karwaya.
					  
					  5. `operation` ko get kiya, aur `operation` mila `search`.
					  
					  6. Agar `operation == search` ho, to `pageNo` ko 1 set kiya.
					  
					  7. User Model ka object banaya.
					  
					  8. Model ki `search` method ko call kiya, jisme `UserBean`, `pageNo`, aur `pageSize` ko pass kiya.
					  
					  9. `search` method ne list return ki, jise list object me hold kiya.
					  
					  10. Servlet utility ki `setList` method ka use karke list ko request object me set kiya.
					  
					  11. Servlet utility ki `setPageNo` method se `pageNo` ko request object me set kiya.
					  
					  12. Servlet utility ki `setPageSize` method ka use karke `pageSize` ko request object me set kiya.
					  
					  13. Finally, Servlet utility ki `forward` method ka use karke request aur response ko `UserListView` pr forward kiya.
					  ```
				- ---
				- We made a field on view.
				- We made a search button; clicked on it ; the request goes to Controller (UserListCtl) ; doPost() will run; we ((6abf2f50-99b1-470a-ad24-538055a6b39c)) the data on controller
				  collapsed:: true
					- get request' data ; set in bean; make object's model; call add method in model; pass the bean in add. in Model we get bean's data and pass in `preparedStatement` and data goes to db.
				- In Model we give condition in `getwhereClause` for Strings only 2 conditions: bean.getFirstName()!=null && bean.getFirstName().length>0 *for dob it is `bean.getDob().getTime()>0`*
					- why !null must be before length
					  collapsed:: true
						- if the bean.getFirstName is null and we checked it's length first then we can get `NullPointerException`
				- `Sql.append(" and FirstName like '"+bean.getFirstName"+"%');`
				-
				- For Gender we can't make input field ; need to make preload for that
				-
				-
-