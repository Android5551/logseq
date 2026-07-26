- [[Mon, 20.07.2026]]
  collapsed:: true
	- It does not have return type
	- It's name is same as class.
	- It is called at the time of object creation
	- Used to initialise instance
		- Provides memory to class variable
		- create parameterised constructor
		- To create instance use default constructor provided by java compiler
	- A class can have multiple constructors called constructor overloading
	- Constructors which receives parameters are parameterised constructors
	- When we use default constructor, to give memory to class attribute we use setter methods.
- [[Tue, 21.07.2026]]
	- # Calling constructor using constructor
	  collapsed:: true
		- Calling same class constructor -> use `this` keyword
		- Calling parent class constructor -> use `super` keyword
		- ## Uses:
			- We use constructor calling where we want constructor to be dependable upon attributes
				- when i want to store and use one attribute out of 4 i can make single constructor of 1 attribute
					- for 4 attributes -> needed one of each i.e. 4 , one having 4 attributes and 1 default = 6
			- We can create constructors according to number of attributes
			- To save memory we use constructor calling
	- if a class has more than one constructor it is called `constructor overloading`
	- if a class has 4 constructors then they can call each other in same class
	- whenever using parameterised constructor call default constructor
		- because whenever we make parameterised constructor , java compiler does not provide default constructor, so make a habit to create one as it may be needed later
	- constructor chaining example
	  collapsed:: true
		- ```python
		  package com.rays.oop.constructor.calling;
		  
		  public class Shape {
		  	protected String color;
		  	protected int borderWidth;
		  
		  	public Shape() { //6 
		  		System.out.println("This is default constructor"); //7
		  	}
		  	public Shape(String color) { //4
		  		this(); //5
		  		this.color = color;
		  		System.out.println(this.color); // 8
		  	}
		  	public Shape(String color, int borderWidth) { // 2
		  		this(color); //3
		  		this.borderWidth = borderWidth;
		  		System.out.println(this.borderWidth); //9
		  		
		  	}
		  	public static void main(String[] args) {
		  		Shape s  = new Shape("Red",3); //1
		  		
		  	}
		  }
		  
		  
		  
		  ```
	-