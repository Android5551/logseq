- Abstract
	- Incomplete
		- #+BEGIN_EXAMPLE
		  if father couldn't clear IIT then his child must clear IIT.
		  #+END_EXAMPLE
	- Abstract classes forces child class to implement specialised behaviour ==forcefully==.
		- Must override method
		- if child does not provide special behaviour then it too becomes abstract or incomplete.
	- Parent class won't give output because parent class has the method abstract
		- Abstract methods doesn't have body
			- ```java
			  public abstract void abs();
			  ```
	- A class becomes abstract when its method is abstract.
		- not necessarily every method but one is enough to declare class abstract.
	- `abstract` keyword for class and method
	- Abstract class object can't be created.
		- does not have constructor
	- if child class extends an abstract class
		- It needs to implement one of the two:
			- Make child class abstract
			- Otherwise, override the method of parent
	-