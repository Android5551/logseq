# JSP
collapsed:: true
	- ## When server not working in jsp
	  collapsed:: true
		- Rename `index.jsp` to `Index.jsp` in both  *web.xml* and in *WebApp folder*
	-
- # Project-04
  collapsed:: true
	- ## When we can't access tables of Project 04 via mysql or can't see data in project ors
		- ((6a742931-8eee-4bc4-a74b-5f3cb16fb92c))
	- ## Long
		- ```
		  Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.lang.Long.longValue()" because the return value of "in.co.rays.proj4.bean.RoleBean.getId()" is null
		  ```
			- turn Long to long in BaseBean
	- ## ClassNotFoundException
	  collapsed:: true
		- ### 1. Check what Tomcat actually has
		  
		  Open this folder in File Explorer:
		  
		  ```
		  C:\Users\FSOS\Documents\CODE\GIT\eclipse\p04\Project04R\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\ORSProject-04\WEB-INF\lib
		  ```
		  
		  Look for `c3p0-0.9.1.2.jar`.
		- **Missing, or the `lib` folder is empty:** go to step 2.
		- **Present:** the jar is there but not loading. Tell me, and also check that the `mysql-connector-java` jar sits next to it.
		- ### 2. Make Eclipse deploy Maven dependencies
		- Right-click the project > **Properties > Deployment Assembly**.
		- If **Maven Dependencies** isn’t listed, click **Add... > Java Build Path Entries > Maven Dependencies > Finish**.
		- Apply and close.
		- ### 3. Refresh and rebuild
		- Right-click the project > **Maven > Update Project...** (Alt+F5), tick **Force Update of Snapshots/Releases**, OK.
		- In the Servers view, right-click the server > **Clean...** and **Clean Tomcat Work Directory**.
		- Restart the server and try logging in again.
- # Adv Java
  collapsed:: true
	- ((6a742930-b24f-4fae-b85d-f7cae80b14cf))