- [[Mon, 06.07.2026]]
	- ### String:
	  collapsed:: true
		- Array of characters is called String
		- `String` is a reference type because it is a class (an object).
			- Only objects (reference types) have methods like `length()` and `toUpperCase()`.
			- **Reference data type** = You don't have the thing itself. You only have the **house address** where it is kept.
				- `int age = 20;` → `20` is stored directly. ✅ Primitive
				- `String name = "Rahul";` → `name` stores the address of the `"Rahul"` object. ✅ Reference
				- Primitive stores the value; reference stores the address of the object.
		- In Java, the **`String` class belongs to the `java.lang` package**.
			- Example:
				- The **String object** `"Hello"` is a **house**.
					- `name` is a **piece of paper with the house's address**.
					  
					  `name` doesn't contain the text `"Hello"` itself. It contains the reference that tells Java where to find the `"Hello"` object.
				- In `String name = "Hello";`, **`name` is a reference variable that refers to the `String` object `"Hello"`**.
		- ### Difference between String and `new` String : #interview
		  collapsed:: true
			- ```java
			  String s = "Java"; // and 
			  String s = new String("Java");
			  ```
				- #### Heap Memory
				  collapsed:: true
					- Heap memory is a part of JVM memory where **objects** and **instance variables** are stored.
						- ##### Object
						  collapsed:: true
							- An **object** is a real entity created from a class. It occupies memory in the **heap**.
							- Created using the `new` keyword.
							- Contains **state (data)** and **behavior (methods)**.
							  
							  Example:
							  ```java
							  class Student {
							    String name;
							    int age;
							  }
							  
							  Student s1 = new Student();
							  ```
							  
							  Here:
							  
							  ```
							  s1 → Student object
							  ```
							  
							  The object is stored in **heap memory**.
							-
							- Whenever you create an object using `new`, memory is allocated in the heap.
						- ##### Instance Variable
						  collapsed:: true
							- Each object gets its **own copy** of instance variables.
							- Stored inside the object in heap memory.
							  
							  Example:
							  ```java
							  class Student {
							    String name;   // instance variable
							    int age;       // instance variable
							  }
							  ```
							  
							  When objects are created:
							  ```java
							  Student s1 = new Student();
							  Student s2 = new Student();
							  
							  s1.name = "Ram";
							  s2.name = "John";
							  ```
							  
							  Memory:
							  ```
							  Heap
							  
							  Student Object 1          Student Object 2
							  ----------------          ----------------
							  name = "Ram"              name = "John"
							  age = 0                   age = 0
							  ```
							  
							  Each object has its **own instance variables**.
				- #### String Literal
				  collapsed:: true
					- A **String literal** is a sequence of characters written inside **double quotes (`" "`)**
					- ##### How it works:
						- String literals are stored in the **String Literal Pool (String Pool)** inside the heap memory.
						- If the same literal already exists, Java reuses the existing object instead of creating a new one.
						  
						  Example:
						  ```java
						  String s1 = "Java";
						  String s2 = "Java";
						  ```
						  
						  Memory:
						  ```
						  String Literal Pool
						  
						  "Java"
						  ▲
						  │
						  s1
						  │
						  s2
						  ```
						  Both `s1` and `s2` point to the same object.
						- They save memory by sharing the same object.
						- Created without using `new`.
			- #### Difference between String and new String: #interview
			  collapsed:: true
				- ```java
				  String b = new String("Java");  // String object
				  // creates a new object in heap memory
				  "Java" is a string literal, so it may exist in the String Pool.
				  new forces creation of a new String object in normal heap memory.
				  b points to this new object.
				  ```
					- Memory:
					- ```
					  Heap
					  - String Pool:
					  "Java"
					  - Normal Heap:
					  String Object  ◄── b
					  ```
					- Example:
					- ```java
					  String a = "Java";
					  String b = new String("Java");
					  - System.out.println(a == b);
					  ```
					- Output:
					- ```
					  false
					  ```
					- Because they are different objects.
					- vs
					- ```java
					  String a = "Java";              // String literal
					  // literal stored in String Pool
					  ```
					- ### Simple Comparison 
					  
					  | `String a = "Java"` | `String b = new String("Java")` |
					  | ---- | ---- | ---- |
					  | Creates a string literal | Creates a new String object |
					  | Stored in String Pool | Stored in normal Heap |
					  | Reuses existing object | Always creates a new object |
					  | Saves memory | Uses extra memory |
					  | Faster | Slightly slower |
					- ### Easy analogy 
					  
					  **String literal:**
					  >"Java" is like a book in a library. If someone already added the book, everyone can use the same copy.
					  
					  **new String():**
					  > You ask the library to make a new personal copy of the same book.
					  
					  The content is the same (`Java`), but the objects are different.
		- Why it printed 'y': #interview
		  collapsed:: true
			- ```java
			  String name = "x"; // name points to the string literal "x" in the String Pool.
			  name = "y"; 
			  /* A new string literal "y" is used (or reused if it already exists
			  in the pool), and the reference variable name is updated to point to "y".
			  The original string "x" is not modified because String is immutable. 
			  Only the reference changes.
			  */
			  
			  System.out.println(name)
			  // output y
			  ```
				- `String` objects are immutable, so `name = "y"` does not change `"x"`. Instead, `name` is made to reference the string `"y"`.
				- The string `"x"` still exists in the String Pool. It just no longer has a reference from the variable `name`. If no references to `"x"` remain elsewhere, it simply becomes unused from your program's perspective.
				- ==Key Point==
					- **Strings are immutable**: their contents cannot be changed.
					- The variable `name` is a **reference variable**. Reassigning it changes **what object it points to**, not the contents of the original string.
	- ### Difference Between `==` and `.equals()` in Java
	  collapsed:: true
		- | `==` | `.equals()` |
		  | ---- | ---- | ---- |
		  | Compares **references (memory addresses)** | Compares **contents/values** |
		  | Returns `true` if both references point to the same object | Returns `true` if the objects are considered equal based on their contents (implementation depends on the class) |
		  | Can be used with primitives and objects | Used only with objects |
		- #### Example 1: String Literals
			- ```java
			  String s1 = "Java";
			  String s2 = "Java";
			  
			  System.out.println(s1 == s2);
			  System.out.println(s1.equals(s2));
			  
			  /* output
			  true
			  true
			  */
			  ```
			- **Why?**
				- `==` → Both variables point to the same string in the **String Pool**.
				- `.equals()` → Both strings contain `"Java"`.
		-
		- #### Example 2: Using `new`
			- ```java
			  String s1 = new String("Java");
			  String s2 = new String("Java");
			  
			  System.out.println(s1 == s2);
			  System.out.println(s1.equals(s2));
			  /*Output
			  false
			  true
			  */
			  ```
			- **Why?**
				- `==` → Different objects in memory.
				- `.equals()` → Same text (`"Java"`).
		- #### Example 3: Primitives
			- ```java
			  int a = 10;
			  int b = 10;
			  
			  System.out.println(a == b);
			  /*Output
			  true
			  */
			  ```
			- `==` compares the actual values of primitive types.
		- #### Memory Diagram
			- ```java
			  String s1 = new String("Java");
			  String s2 = new String("Java");
			  ```
			  
			  ```
			  Heap
			  
			  Object 1 ("Java") ◄── s1
			  
			  Object 2 ("Java") ◄── s2
			  ```
			- `s1 == s2` → `false` (different objects)
			- `s1.equals(s2)` → `true` (same contents)
		- #### Interview Definition #interview
			- **`==`** compares **references for objects** and **values for primitive types**.
			- **`.equals()`** compares the **contents (logical equality)** of objects. Its exact behavior depends on how the class implements `equals()`.
	-
- [[Tue, 07.07.2026]]
  collapsed:: true
	- ### String Methods
		- `method()` -> in parenthesis the text is called method parameter or method arguments
		- #### Methods:
			- **`length()`** – Returns the number of characters in a string.
			- **`length() - 1`** – Gives the last index of the string.
			- **`indexOf()`** – Returns the index of the first occurrence of a character or substring.
				- substring means "Vijay Singh" -> "Singh"
			- **`lastIndexOf()`** – Returns the index of the last occurrence of a character or substring.
			- **`replace()`** – Replaces all occurrences of a character or substring with another.
			- **`toLowerCase()`** – Converts all characters to lowercase.
			- **`toUpperCase()`** – Converts all characters to uppercase.
			- **`startsWith()`** – Checks if the string starts with the given prefix. Returns `true` or `false`.
			- **`endsWith()`** – Checks if the string ends with the given suffix. Returns `true` or `false`.
				- Prefix and Suffix are case-sensitive
			- **`substring(beginIndex)`** – Returns the substring from the given index to the end.
			  id:: 6a4c952d-d0f0-4c99-a4a2-17dc7c7fe9b7
			- ==Note==
				- **Strings are immutable**, so methods like `replace()`, `toUpperCase()`, `toLowerCase()`, and `substring()` return a **new `String`** and do not change the original string.
			- **`String.charAt(index)`**
				- It returns the **character** present at the specified **index (position)** in the string.
				- **Example:**
					- ```java
					  String str = "Hello";
					  System.out.println(str.charAt(1)); // e
					  // Here, the character at index `1` is 'e'.
					  ```
	- ### String Related Classes
	  collapsed:: true
		- String
			- Cannot be changed. Any modification creates a **new object**.
		- String-Buffer
			- can change their contents at runtime
		- String-Builder
			-
		- #### Difference between String, StringBuffer and StringBuilder #interview
			- 📖 **String** → Ink on paper. You can't erase it; you need a new sheet.
			- 👥 **StringBuffer** → A whiteboard used by a team. People take turns writing to avoid conflicts.
			- ✍️ **StringBuilder** → Your personal notebook. You're the only one writing, so it's faster.
			-
			- **String** → Fixed text (immutable).
			- **StringBuffer** → Shared editable text (thread-safe).
			- **StringBuilder** → Personal editable text (fastest for a single thread).
			-
		-
		-
		-
-