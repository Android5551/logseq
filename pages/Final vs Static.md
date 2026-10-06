- final vs static
	- ### `final`
	  collapsed:: true
		- Means **cannot be changed**.
		  
		  ```java
		  final int x = 10;
		  x = 20; // Error
		  ```
		- #### Final variable
		  
		  ```java
		  final String NAME = "Piyush";
		  ```
		  
		  Value cannot be reassigned.
		- #### Final method
		  
		  ```java
		  final void display() {
		  }
		  ```
		  
		  Cannot be overridden by a child class.
		- #### Final class
		  
		  ```java
		  final class Test {
		  }
		  ```
		  
		  Cannot be inherited.
		  
		  ---
	- ### `static`
	  collapsed:: true
		- Means **belongs to the class, not to an object**.
		  
		  ```java
		  class Test {
		    static int count = 0;
		  }
		  ```
		  
		  Access without creating an object:
		  
		  ```
		  System.out.println(Test.count);
		  ```
		- #### Static method
		  
		  ```java
		  class Test {
		    static void show() {
		        System.out.println("Hello");
		    }
		  }
		  ```
		  
		  Call directly:
		  
		  ```
		  Test.show();
		  ```
		  
		  ---
	- ### Together: `static final`
	  collapsed:: true
		- Used for constants.
		  ```java
		  public static final double PI = 3.14159;
		  ```
		- `static` → one copy for the entire class.
		- `final` → value cannot change.
		  
		  Access as:
		  ```java
		  System.out.println(Math.PI);
		  ```
			- `PI` is a classic example of `static final`.
	- ### Easy way to remember
	  collapsed:: true
		- | Keyword | Meaning |
		  | ---- | ---- | ---- |
		  | `final` | Cannot change |
		  | `static` | Belongs to class |
		  | `static final` | Constant shared by all objects |
		- Example:
		  
		  ```java
		  class Account {
		    static int count = 0;          // Shared by all accounts
		    final int accountType = 1;     // Cannot change
		    static final String BANK = "SBI"; // Constant
		  }
		  ```
	- ---
	- ## `static` → one copy for the entire class.  what do you mean by that
		- Normally, **non-static variables belong to each object**.
			- Example:
				- ```java
				  
				  class Student {
				      int id;
				  }
				  ```
				  ```java
				  Student s1 = new Student();
				  Student s2 = new Student();
				  
				  s1.id = 101;
				  s2.id = 102;
				  ```
				  Here:
				  ```java
				  s1.id = 101
				  s2.id = 102
				  ```
				  Each object has its **own copy** of `id`.
			- Now with `static`:
			  ```java
			  class Student {
			    static int count = 0;
			  }
			  ```
			- ```java
			  Student s1 = new Student();
			  Student s2 = new Student();
			  - s1.count = 10;
			  - System.out.println(s2.count);
			  ```
			- Output:
			- ```
			  10
			  ```
			- Why?
			- Because there is **only one `count` variable for the entire class**, shared by all objects.
			- Think of it like this:
		- ### Non-static
		  
		  ```
		  s1 --> [id=101]
		  s2 --> [id=102]
		  ```
		  
		  Each object stores its own value.
		- ### Static
		  
		  ```
		  Student Class
		         [count = 10]
		            /     \
		          s1       s2
		  ```
		  
		  Both `s1` and `s2` point to the same `count`.
		  
		  That's why we usually access it through the class name:
		  
		  ```
		  Student.count = 10;
		  System.out.println(Student.count);
		  ```
		  
		  instead of:
		  
		  ```
		  s1.count
		  s2.count
		  ```
		- ### Real example
		  
		  ```java
		  class Student {
		  
		    static int totalStudents = 0;
		  
		    Student() {
		        totalStudents++;
		    }
		  }
		  ```
		  
		  ```java
		  new Student();
		  new Student();
		  new Student();
		  
		  System.out.println(Student.totalStudents);
		  ```
		  
		  Output:
		  
		  ```
		  3
		  ```
		  
		  If `totalStudents` were not static, every object would have its own counter and you couldn't keep track of the total number of students created.