- [[Tue, 14.07.2026]]
	- Child can't be created or singleton can't be inherited and object can't be created by another class.
	- It provides everything itself
	- One app has one database only not more than one
	  collapsed:: true
		- n no. of instance can be created of app
			- every instance will have its own database
		- database creation has limitation
			- There is a method that make connection to database
			- mysql can't make more than 150 connections at a time because it will crash
				- 60-75 -> runs ok
				- 75+ -> slow
			- if creating app and integrating database you need to set connection limitation
			- create class to get one-time connection
				- Properties:
					- maxConnection
						- when you create instance of class (let's assume maxConnection=30); when you create another instance maxConnection=60 likewise +30 for other instances;
						  once it gets greater than 150 app got crashed
					- minConnection
					- initialPullConnection -> when we run connection at first  time we get this much connection beforehand
					- acquiredIncrementConnection -> at a time
	- Classes which gives connection we make it `Singleton` ; only  one time its instance will be created; once app starts its instance will be created once.
	  collapsed:: true
		- It has One `close connection` what it does is if maxConnection=30 then out of 30, 4 has completed their work then get automatically close so that other 4 gets connection
			- Instead of creating 60 connection we go for creating another instance of app to make app reliable ; in another instance we get 30 connections again; hence the `load balancing` done.
				- This is called `singleton design pattern` #interview
				-
		-
		- Data hiding:
			- **`public`** → Accessible from **anywhere** in the program.
			- **`private`** → Accessible **only within the same class**.
			- **`protected`** → Accessible **within the same package and by subclasses (even in other packages)**.
		-
	- ### Static keyword
	  collapsed:: true
		- #### Attributes
		  collapsed:: true
			- `Math.PI`
				- `PI` is static if only final then need to create Math class object to call Pi
			- >_The attributes which don't need to allocate memory that attribute assigned as static_
				- No need to create object to call that
				- called directly by class name
					- use it with final only; if final then only static
		- #### Methods
		  collapsed:: true
			- can be called using class directly