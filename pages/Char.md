- The **`Character`** class is a [[wrapper class]] in Java that provides methods to work with a single character (`char`), such as checking whether it is a digit, letter, uppercase, lowercase, or whitespace.
	- {{embed ((6a4dca61-55fc-43e8-a9c5-78c2ba4d20c6))}}
- ### Methods
  collapsed:: true
	- `Character.isDigit(x.charAt(i))`
		- means at given index whether the character is digit
		- first retrieves the character at index `i` from the string `x` using `charAt(i)`, then checks whether that character is a numeric digit (`'0'` to `'9'`).
		- **Example:**
			- ```java
			  String x = "Ram123";
			  Character.isDigit(x.charAt(0)); // false ('R')
			  Character.isDigit(x.charAt(3)); // true ('1')
			  Character.isDigit(x.charAt(5)); // true ('3')
			  ```