# Playground 1
	- # hi this is h1
	- ## hi this is h2
	- ### hi this is h3
	- #### hi this is h4
	- ##### hi this is h5
	- ###### hi this is h6
	- ---
	- ==highlight==
	- _italics_
	- **bold**
	- `this is the code`
	- <ins>underline</ins>
	- [[Mon, 20.07.2026]]
	- [#A] test
	- ```calc
	  
	  ```
	- ``` java
	  public void method(){
	    system.out.println("hello");
	  }
	  
	  ```
	- #+BEGIN_NOTE
	  Note
	  #+END_NOTE
	- #+BEGIN_TIP
	  Tip
	  #+END_TIP
	- #+BEGIN_IMPORTANT
	  Imp
	  #+END_IMPORTANT
	- #+BEGIN_CAUTION
	  Caution
	  #+END_CAUTION
	- #+BEGIN_EXAMPLE
	  example
	  #+END_EXAMPLE
	- #+BEGIN_VERSE
	  this is verse i dont
	  know what is that
	  #+END_VERSE
	- #+BEGIN_CENTER
	  Center
	  #+END_CENTER
	- #+BEGIN_COMMENT
	  this is the
	  comment
	  #+END_COMMENT
	- #+BEGIN_EXPORT ascii
	  and this is ascii
	  #+END_EXPORT
- ## Testing models
	- ## Comparator
	  collapsed:: true
		- Most used
		- At a time any one attribute can be used for sorting
		- One class can have multiple comparator
			- No. of comparator depends on no. of attributes based on which sorting will be done
			- for ex
				- 3 attributes can have 6 comparators
					- name -> orderbyname asc, orderbyname desc
		- Contains `compare` abstract method
			- `public interface Comparator<T>`
				- `int compare(T o1, T o2);`
					- gets to compare 2 objects of class
			- Comparator interface  
			  Contains abstract method compare  
			  compare method signature: int compare(T o1, T o2)  
			  Compares two objects of the same class
		- code:
			- make attribute public
				- if you make them private then need to create getter methods for ex. in  another class we need to use `o1.getProductPrice`
				- its comparator will be created in another class
					- because One class can have multiple comparator
					- so to access those comparators making attribute public
			- Comparator won't implement in class where we are giving attirbutes
				- those will implemented in another class filters
			- so in main we can pass both collection object as well as comparator object in collections sorting
			- ^^52:17^^
		-
		- Comparator  
		  Used to sort objects based on specific attributes  
		  Allows sorting by one attribute at a time  
		  A class can have multiple comparators depending on the number of attributes  
		  For example, 3 attributes can have 6 comparators (name ascending, name descending, etc.)  
		  
		  Comparator interface  
		  Contains abstract method `compare`  
		  Method signature: `int compare(T o1, T o2)`  
		  Compares two objects of the same class  
		  Returns negative, zero, or positive based on order  
		  
		  Example:  
		  `int compare(Product o1, Product o2)`  
		  Compares product prices or names  
		  
		  Implementation details  
		  Attributes must be accessible (public or via getters)  
		  If attributes are private, use getter methods like `o1.getProductPrice()`  
		  
		  Comparator is implemented in a separate class  
		  Not in the class where attributes are defined  
		  Enables multiple sorting rules for the same class  
		  
		  Usage in code  
		  Pass collection and comparator to `Collections.sort()`  
		  Example:  
		  `Collections.sort(list, new PriceComparator())`  
		  
		  Analogy:  
		  Like having different sorting rules for a list of books: sort by title, author, or publication year. Each rule is a separate comparator.
	- Earlier we use to create different class for table like insert , update, delete , create etc.
		- but now we will create a **model class** having all these as methods
			- classes which communicates with database are called *model class*
				- `public void add(int id, String firstname)` -> the id or firstname can be anything as they are obj.
				- Class Name -> TableNameModel
				- add queries of only one table otherwise it gets complicated
			- in class UserModel the date is of type `java.util` and in database date is of type `java.sql` convert util date to sql date
				- `new java.sql.Date(dob.getTime()))` converts to sql type
			- `prepareStatement()` is connection's method and write query inside it and store in `PreparedStatement obj`
				- import `java.sql.PreparedStatement`;
				- in `prepareStatement()` don't give values
				- Replace values with `?` as per no. of columns
				- `obj.setInt(parameterIndex means ?1,value to be stored ie firstName)` or setString or setDate
		- you can call add() using creating that class object and call using that obj function
			- in model.add(the date should be converted to simple date format sdf. then parsed to date format
			- ==32:03==
			-
			-
			- Code  
			  Earlier separate classes were created for insert, update, delete, and create operations.  
			  Now a single model class is used to handle all database operations for a single table.  
			  
			  Model Class  
			  - Classes communicating with the database are called model classes.  
			  - Class name follows the pattern: TableNameModel (e.g., UserModel).  
			  - Model class contains methods for all CRUD operations.  
			  
			  Date Conversion  
			  - Java.util.Date is used in code, while java.sql.Date is used in the database.  
			  - Convert util date to sql date using:  
			    new java.sql.Date(dob.getTime())  
			  
			  PreparedStatement  
			  - prepareStatement() is a method of Connection.  
			  - Write SQL query inside prepareStatement() and store in PreparedStatement obj.  
			  - Replace values with ? placeholders matching the number of columns.  
			  - Use setInt, setString, or setDate to assign values to parameters.  
			  - Parameter index is specified as ?1, ?2, etc.  
			  
			  Parameter Setting  
			  - Set values using:  
			    obj.setInt(1, firstName)  
			    obj.setString(2, lastName)  
			    obj.setDate(3, new java.sql.Date(dob.getTime()))  
			  
			  Usage  
			  - Create model class instance and call add() method.  
			  - Convert date to simple date format, then parse to date format.