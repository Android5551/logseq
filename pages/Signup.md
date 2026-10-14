- UserRegistrationView form par `SignUp` button par click kiya.
  collapsed:: true
	- Form tag me:
	  `<form action="<%=ORSView.USER_REGISTRAION_CTL%>" method="post">`
- `doPost()` method humne baseCtl ko extend kiya hai to `Basectl` ki `doPost()` chalai
	- `B bean = populateBean(req)` ise humne `UserRegistrationCtl` me override kiya hai
	- `b.setRoleId(2L);` se role id student set kar denge bean me
	- `bean.setFirstName(DataUtility.getString(request.getParameter("firstName")))`
	- try block me check karenge ki `if bean.getId()>0` then `model.update(bean)`  else `model.add(bean)`aur `ServletUtlility.setSuccessMessage()` se *record updated/added successfully* set kar denge message, request ke form me.
	- UserModel ki add(bean) ya update(bean) method me insert/update ki query chalai record data base me add kiya
	  collapsed:: true
		- **add()**:
			- `public long add(UserBean b)`
			- `findByLogin` me `bean.getLogin` pass karenge aur `existbean` me set karenge
			  id:: 6acf221a-46a6-483e-978d-72f821fd0e6e
			- if(existBean != null) `throw new DuplicateRecordException("login already exists)`
			- query `insert into st_user values(???)` p.setLong(1,b.getId()) ...
		- **update()**
			- `public void update(UserBean b)`
			- ((6acf221a-46a6-483e-978d-72f821fd0e6e))
			- if(existBean != null && existBean.getId()!=bean.getId() then throw exception
			- query `update st_user set first_name=?,,, where id=?`
			- `p.setString(1, b.getFirstName());`
- UserModel ki add(bean) method call hui kyonki user add ho raha hai.
- View par:
	- ServletUtility.getSuccessMessage(request)
	  se  message get kiya aur
	  expression tag me print kiya.