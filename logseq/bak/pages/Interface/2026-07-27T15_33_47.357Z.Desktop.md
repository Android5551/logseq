## Define:
	- A class has different interfaces.
	  collapsed:: true
		- #+BEGIN_EXAMPLE
		  - a website has light theme and dark theme these are interfaces
		  - amazon festive page or diwali page or big billion page
		  
		  - Person parent class , Student child class Student can be of pcm, pcb etc. so these are interfaces of Student.
		      - Student extends person but implements pcm , pcb
		      - A class doesn't have multiple parents but multiple implementations are possible
		  
		  - Businessman is a Person but he can be richman, social worker 
		  #+END_EXAMPLE
	- Interface has all methods abstract.
	- All attributes are constant, value will be assigned once.
	- As child can't have two parents.
		- there is a student who is person and is student of biology how can we define it.
			- we can't do student with parent person and parent bio
			- so we use interface.
			- student extend person and implements bio
				- so need to forcefully override
- ### Difference between Interface and abstract class
	- Abstract class can have both abstract and non abstract methods
		- can have constants and non constants attributes
	- Interface has all methods abstract.
	- All attributes are constant
-