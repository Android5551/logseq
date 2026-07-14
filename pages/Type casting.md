## When to use
- As parent can't call child method because parent cant extend child. and you need to call child method:
	- To do that we use type casting
		- Parent object to child obj typecast
		- example typecast `s` to Circle
		- > if `s` has memory of Circle child the typecasting is possible only in that child only
		  s having reference to Circle then typecasting can only be done to Circle
			- ```java
			  Shape s = new Circle();
			  // typecasting
			  Circle c = (Circle) s;
			  ```
			- #+BEGIN_CAUTION
			  If casted on any other child class
			  gets `ClassCastException` error
			  #+END_CAUTION
			-
		-