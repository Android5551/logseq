- Abstract
  collapsed:: true
	- Incomplete
	  collapsed:: true
		- #+BEGIN_EXAMPLE
		  if father couldn't clear IIT then his child must clear IIT.
		  #+END_EXAMPLE
	- Abstract class won't provide general behaviour.
	- Abstract classes forces child class to implement specialised behaviour ==forcefully==.
	  collapsed:: true
		- Must override method
		- if child does not provide special behaviour then it too becomes abstract or incomplete.
	- Parent class won't give output because parent class has the method abstract
	  collapsed:: true
		- Abstract methods doesn't have body
			- ```java
			  public abstract void abs();
			  ```
	-
	- A class becomes abstract when its method is abstract.
	  collapsed:: true
		- not necessarily every method but one is enough to declare class abstract.
	- `abstract` keyword for class and method
	- ==Abstract class object can't be created.==
	  collapsed:: true
		- does not have constructor
	- if child class extends an abstract class
		- It needs to implement one of the two:
			- Make child class abstract
			- Otherwise, override the method of parent
	- Earlier when we did method overriding in complete class there was `super` keyword which shows generalised behaviour but now it will be a specialised behaviour, so no `super` keyword will be there
		- As abstract class has incomplete method so the child class had completed this abstract class by overriding. Hence method is defined in child class. not parent i.e. area method will be called from child class
		  collapsed:: true
			- To create object of abstract class you need to take its child class reference which had overridden parent class method
				- #+BEGIN_EXAMPLE
				  Rbi decides it won't give interest rates to other child classes or banks so you can put it as abstract class.
				  then other banks have to override the method of parent class known as `interestRate()` and give their own specialised behaviour 
				  #+END_EXAMPLE
				- parent class's object and reference of child.
					- `Shape s = new Circle();`
				- Shape won't get memory as it is incomplete so memory will be provided to Circle as it had completed the class by overriding the method
			- As parent can't call child's method we need to typecast it.
			-
	- `Concrete class` -> classes which completes an abstract class by method overriding are called concrete class.
		- #+BEGIN_EXAMPLE
		  Rectangle, circle 
		  #+END_EXAMPLE
	-
-