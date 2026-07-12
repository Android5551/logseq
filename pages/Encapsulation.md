- [[Wed, 08.07.2026]]
  collapsed:: true
	- used to create Expert classes
		- > expert classes has related methods and attributes
	- All classes in java are expert classes
	- Expert class attribute is private
		- methods are public
	- UML(Unified Module Language) diagram or class diagram
		- First part is called class
		- Second has attributes
			- `-` -> denotes private
			- `+` -> denotes public
			- `$`-> denotes constant with Capital Letters
			-
	- ---
	- collapsed:: true
	  ```java
	  public void setNumber(String number) {
	      this.number = number; // Account object's number = method's number
	  }
	  ```
		- Breakdown:
			- `public` → access modifier (can be called from anywhere)
			- `void` → the method **does not return any value**
			- `setNumber` → method name
			- `(String number)` → the method accepts one parameter of type `String`
			- `this.number`
				- The `number` that belongs to the **Account object**
				- `this` points to the **current object** (here, the `Account` object).
				- **Why to use ==this==**
					- when there is a **name conflict** between a class attribute and a method parameter.
			- `number` -> the variable passed into method
		- `setNumber()` A setter is used to **change** a private attribute.
			- Stores the data; generally does not return anything.
		- `getNumber()` A getter is used to **read** a private attribute.
- [[Fri, 09.07.2026]]
  collapsed:: true
	- ## Difference between variable and class attributes
		- Under Method is called variable
		- Under class is called class attributes
	- ### class attributes
		- private datatype Attribute;
			- do not store value
		- constant Attribute:
			- store value during creation of this attribute
			- does not change value
			- public
		- #### Indirectly access private class attributes
			- Create methods ; getters and setters
				- ##### Setters
					- A method which stores value in these attributes is called setters
						- need to give argument.
						- that argument is stored to class attribute
						- Public
						- **return type** void because it only gives value
						- #+BEGIN_IMPORTANT
						  To call class attribute use `this ` keyword
						  #+END_IMPORTANT
						- > Method argument gets stored into class attribute
						-
				- ##### Getters
					- A methods which prints stored values is called getters
					- **Return type** will be datatype related to respective class datatype
					- Public
					- use keyword `this` to call class attribute
	- #+BEGIN_CAUTION
	  The getters, setters and all class attributes will not be in main class and is called structure; to use this structure we need to create object
	  #+END_CAUTION
		- ```java
		  Person p = new Person();
		  // new allocates memory
		  ```
			- `Person()` is constructor
			- `Person p = null;` -> this is object creation
				- if you call any method of class using `p` there will be no allocation of values in memory
				  because there is no instance (`using new keyword`) creation
				- #+BEGIN_NOTE
				  To allocate memory to class or create instance we use `constructor` 
				  #+END_NOTE
			- Every object made using new keyword gets new memory
				- #+BEGIN_IMPORTANT
				  Each memory has reference ID called memory address; when we create instance, this new object got memory address; in that memory value gets stored of object
				  when you want to get this value from getter ; it uses that reference
				  that reference is called pointers in C++
				  #+END_IMPORTANT
				- > Java is pointer-less programming ; as it does that internally
	- if a class datatype is `Date` type you need to create `Date object` for that and import `java.util`
	  in main
		- #+BEGIN_NOTE
		  when we create object of date it gives current date and time in `String` type
		  To give your type of formatted date use `SimpleDateFormat` class ; make the object of simpledateformat and pass the format like "dd-MM-yyyy"
		  #+END_NOTE
		- #+BEGIN_IMPORTANT
		  + Method required to change `String` type to `Date` -> `parse` method on `SimpleDateFormat` and pass `String` type date in double quotes; add exception too
		       + ```java
		            SimpleDateFormat sdf = new SimpleDateFormat("dd-MM-yyyy");
		            Date date = sdf.parse(str);
		          ```
		  + Method required to change `Date` to `String` -> `format` method on `SimpleDateFormat` and pass `Date object needed to be formatted`
		        + ```java
		             String str = sdf.format(date);
		           ```
		  #+END_IMPORTANT
		-
		-