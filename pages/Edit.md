- User List View par edit ki link banai.
	- ```jsp
	  <td><a href="<%=ORSView.USER_CTL +"?id="+bean.getId()%>"></a></td
	  ```
- Request `UserCtl` par gayi jaha humne `BaseCtl` ko extend kiya hai , BaseCtl ki service method chali aur POST wali condition false hogi to super.service() se doGet method call hui.
- `BaseCtl` par request parameter se id get ki aur `DataUtility.getLong()` me pass kar diya aur id me store kiya.
- Agar id > 0 ho to UserModel ki findByPk method ko call kiya, jisne UserBean return kiya, aur use UserBean ke object bean mein hold kiya.
	- `M model = getModel()`
	- `BaseBean b = model.findByPk(id)`
	- in `BaseModel` we made `findByPk` where query is `select * from getTable() where id=?`
- `ServletUtility.setBean(bean, request)`; ko call kiya taaki bean ko request mein set kiya ja sake.
  `ServletUtility.forward(getView(), request, response);` se `UserView.jsp` par forward kiya.
- UserView par `<jsp:useBean id="bean" class="in.co.rays.bean.UserBean" scope="request"></jsp:useBean>` se bean ko get kiya.
- ek hidden input field banayi id ki
	- `<input type="hidden" name="id" value="<%=DataUtility.getStringData(bean.getId())%>">`
- aur condition di ternary operator me ki agar bean null nahi hota hai aur bean ki id > 0 to Update user likho ni to Add user
	- `<h1><%=bean != null && bean.getId() > 0 ? "Update User" : "Add User"%></h1>`
- input fields me value attribute me `DataUtility.getStringData()` me ye sab pass kiya `<%=bean.getFirstName()%>`,`<%=bean.getLastName()%>`....
- ---
- Save button pe click kiya
- Request gyi `ORSView.USER_CTL` pe aur basectl ki doPost chali Service method me jake validations check karne ke baad.
	- `M model = getModel()` model ka object banaya
	- `populateBean` `UserCtl` ne override ki hai
	- populateBean me `DataUtility.getLong()` me `request.getParameter("id")`, `bean.setRoleId(2)` pass karenge isi tarah baki fields ko pass karenge aur bean return kar lenge.
	- returned Bean ko `B bean` me store kiya.
	- try block me check kiya agar `bean.getId()>0` hai  to model ki update method me bean pass kar do ni to add method me bean pass kar do aur dono pe hi `ServletUtility.setSuccessMessage()` me `record updated/added successfully` set kiya msg, req ke form me.
	- catch me `ServletUtility` se error set kardiya `record already exists.`
	- `ServletUtility.setBean(bean, req);` bean set kiya request me.
	  `ServletUtility.forward(getView(), req, resp);` view pe forward kiya
	- view par `String succ = ServletUtility.getSuccessMessage(request);` se expression tag me print kara liya
	-