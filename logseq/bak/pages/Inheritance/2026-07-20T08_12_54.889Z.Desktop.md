- [[Mon, 13.07.2026]]
	- `#->Protected` attributes : making parent class attributes protected helps child class to access it. Otherwise if private child class can't do that
	- put some properties in parent class for reusability such that child class can access it
	- #+BEGIN_IMPORTANT
	  Whenever you make child class object so memory will be allocated to child class but child will store parent property to its memory too
	  `Circle c = new Circle();`
	  so child can access its  own properties as well as parent's
	  #+END_IMPORTANT
	- You can make object of parent class and allocate memory to child class
		- `Shape s = new Circle();`
			-
			- color and border-width in circle;
				- because here parent is not extending child class
				- so parent properties only be there.
			- as we made parent class obj s hence all properties of parent will be there except child's
			- > called as Parent can keep child reference
			- Make obj of parent and give reference to child class