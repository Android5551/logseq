- [[Mon, 13.07.2026]]
	- ## Definition
	  collapsed:: true
		- creates ((6a5cd5fe-18ad-4c76-a932-80df6f6f3166))
			- ex. `Dhirubhai ambani` is generalised class
				- `Mukesh` and `anil` are specialised class.
				- Specialised classes
				  id:: 6a5cd5fe-18ad-4c76-a932-80df6f6f3166
					- also called as child class, sub class
					- these are expert classes
					- classes which inherits parent class properties and provides their specialised behaviour
				- Generalised classes
					- parent class, super class
					- Having common properties
		- Inheritance provides reusablity
			- Shape class having its attributes like colour and border width
				- circle having radius if it `extends` Shape ; no need to create ((6a5cd931-f76c-44aa-b14d-bfc45ef3b853)) and ((6a5cd96a-6828-4f0d-ba37-b09fbf0dea20)) of parent class attributes only radius.
					- setter method
					  id:: 6a5cd931-f76c-44aa-b14d-bfc45ef3b853
					  collapsed:: true
						- having no return type
						- to set value.
						- having arguments
						- ```java
						  public void setValue(String color){
						    this.color = color;	// this for accessing private attributes
						  }
						  ```
					- getter method
					  id:: 6a5cd96a-6828-4f0d-ba37-b09fbf0dea20
					  collapsed:: true
						- to get value
						- having return type
						- having no arguments
						- ```java
						  public String getValue(){
						    return this.color;
						  }
						  ```
					- `Alt+Shift+s+r` #shortcut
		- In Inheritance Parent has multiple children but a child can't have multiple parents
			- because if Parent has colour property so child will get confused which one to inherit
	- ## Types
	  collapsed:: true
		- Single
			- Parent has one child
		- Multilevel
			- Parent has child and child has a child
		- Hierarchical
			- Parent has multiple child
		-
	- `#->Protected` attributes : making parent class attributes protected helps child class to access it. Otherwise if private child class can't do that
	- put some properties in parent class for reusability such that child class can access it
	- #+BEGIN_IMPORTANT
	  Whenever you make child class object so memory will be allocated to child class but child will store parent property to its memory too
	  `Circle c = new Circle();`
	  so child can access its  own properties as well as parent's
	  #+END_IMPORTANT
	- You can make object of parent class and allocate memory to child class
	  collapsed:: true
		- `Shape s = new Circle();`
			-
			- color and border-width in circle;
				- because here parent is not extending child class
				- so parent properties only be there.
			- as we made parent class obj s hence all properties of parent will be there except child's
			- > called as Parent can keep child reference
			- Make obj of parent and give reference to child class
	- ### Automobile class
	  collapsed:: true
		- ##### methods
			- brake() no args
			  id:: 6a5cca40-5d59-4cfc-bf29-ca7fb6685406
				- whenever we call brake method speed gets reduced
					- when speed gets 0 print message car gets stopped don't apply brake
						- if speed == 0 car gets stopped
						- else speed -10
			- change gear()
				- if gear = 1 -> speed  = 20
				- send argument in change gear()
				- max gear 4
					- speed = 0 -> neutral
					- speed = 20 -> 1st gear
					- 40 -> 2nd gear
			- accelerator() no args
				- speed >=400 print max speed
					- else speed +10
				- set the speed = 200,
				- Whenever accelerator method gets called the speed should increase by 10
					- ex 210, 220... likewise up to 400.
					- after that it should print like if speed is greater than 400
						- Message apply ((6a5cca40-5d59-4cfc-bf29-ca7fb6685406)) your speed is too high
			-
	- `final` and `static` makes an attribute value fixed.
	-