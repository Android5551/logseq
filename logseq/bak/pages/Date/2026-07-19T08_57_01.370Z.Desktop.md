- [[Tue, 07.07.2026]]
	- Package name : `java.util`
	- Need to import manually as it is not java.lang root package
	- ### Object creation
		- ```java
		  Date d = null;
		  d = new Date();
		  ```
		- ```java
		  Date d = null;
		  ```
			- `Date` is a class (reference type).
			- `d` is a reference variable.
			- `null` means `d` is not pointing to any object yet.
			- No object is created in the heap.
			- Memory:
			  ```
			  Stack
			  -----
			  d → null
			  ```
		- ```java
		  d = new Date();
		  ```
			- `new Date()` creates a new `Date` object in the heap.
			- The reference variable `d` now stores the address/reference of that object.
			  Memory:
			  ```
			  Stack              Heap
			  -----              ----
			  d  ------------->  Date object
			  ```
			- ==Important Points==
				- `null` means "no object is referenced".
				- `new` creates an object in heap memory.
				- A reference variable can first be `null` and later point to an object.
				  
				  Both are valid:
				  ```
				  Date d = new Date();
				  ```
				  or
				  ```
				  Date d = null;
				  d = new Date();
				  ```
				  The second form is useful when the object creation depends on some condition.
- [[Wed, 08.07.2026]] ==1:20:12==
	- `new` to create new object of class
	- `Thread.sleep(1000)`
		- 1000 milliseconds
		- to run task every second
		- use `Interrupted Exception`
		- new date object should be inside while loop otherwise a fix date will be printed it won't be dynamic
	- ---
	- DOB print
		- here past time is not available
		- dob uses of.
		- now - dob = age
	- > `Date` to `FormattedDate` use objsdf.Format(obj.date)
	  >  `FormattedDate` String to `Date` use parse Method(Str.obj)
	-
	- Local Date
		- no new keyword needed
		- no time in this available
		- it uses current date
			- use DayOfWeek program `testLocalDate.java`
			-
	-
	-
	-