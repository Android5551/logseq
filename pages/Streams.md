- [[Thu, 30.07.2026]]
  collapsed:: true
	- # Streams feature of Java 8
		- It filters and manipulates the data stored in data source
		  collapsed:: true
			- #+BEGIN_EXAMPLE
			  it works like water purifier ; source is water tank ; it takes water from it separates impure water , drain it and provides drinking water 
			  #+END_EXAMPLE
		- It does not store data,  performs only intermediate operations.
		- Lazy they don't execute immediately they just sit and wait, data source and stream does not work until objects[**The individual items stored in your data source.**] are needed by terminal operations
		  collapsed:: true
			- #+BEGIN_EXAMPLE
			  until you don't take drinking water you won't know if water is filtered or not
			  #+END_EXAMPLE
			- Data is stored in data source
		- ### data source:
		  collapsed:: true
			- Collections. Arrays, I/O (files)
			- where large amount of data is stored
		- ### Intermediate operations :
		  collapsed:: true
			- Streams
			- middle stage
			- It does NOT execute immediately. It just "records" what you want to do.
			- It has 3 methods:
				- #### Filter
				  collapsed:: true
					- Give conditions
					- #+BEGIN_EXAMPLE
					  - filter strings starting with 'T'
					  - ends with 'T'
					  - this one is case sensitive
					  #+END_EXAMPLE
					- no need to use if-else
				- #### Map
					- Prints
					- #+BEGIN_EXAMPLE
					  - prints all attributes here 
					  #+END_EXAMPLE
					-
				- #### Reduce
				  collapsed:: true
					- Limits
					- #+BEGIN_EXAMPLE
					  - can add limits
					  - skip
					  
					  #+END_EXAMPLE
		- ### Terminal
		  collapsed:: true
			- prints
			- using `ForEach` method (Performs an action on **every** element)
				- `count`
			-
		- can be found in `java.util`
		- **Once you call a terminal operation, the stream is CONSUMED and CANNOT be reused!**
		  **if done then `IllegalStateException`**
		- _Can't modify the source_
		- example
		  collapsed:: true
			- ![image.png](../assets/image_1785466611961_0.png)
			-
		- ## Streams vs Collections
		  collapsed:: true
			- | **Streams** | **Collections** |
			  | ---- | ---- | ---- |
			  | ☑️ It does not store data | ☑️ It stores data |
			  | ☑️ It is read-only | ☑️ It is read and write both |
			  | ☑️ It can only be read once | ☑️ It can be read multiple times |
			  | ☑️ Elements cannot be directly accessed | ☑️ Elements can be directly accessed (e.g., `list.get(0)`) pass the index 0 |
		- ## Code:
			- ### to convert Collection to Stream
			  collapsed:: true
				- `Collection.stream()`
				- `.stream()` converts collection to stream
			- ### To convert Stream to Collection
			  collapsed:: true
				- `stream().collect()`
			- ### To sort stream
			  collapsed:: true
				- `Collection.stream().sorted()`
					- prints in ascending order
					- For descending order
						- `Collection.stream().sorted(Collections.reverseOrder())`
							- use `Collections` `reverseOrder()` mehtod and instead of Collection use object like c or list etc.
							- here object like list or interface like Collection is data source. and after that intermediate ops
			- Can add multiple intermediate operations
			- ### Using map and convert to upperCase
				- #### Lambda Expression (->) feature of Java 8
					- if you want to do operations on an object on runtime i.e.  before printing
						- for ex. e is an object we used arrow token and perform ops at runtime
							- if you want to want to find out whether 1 is odd/even
							- 1 -> 1/2 checks if odd or even
							- e has value stored ; in right side whatever ops you perform or checks will be applied on left side **e** value
					- `list.stream().sorted().map(e -> e.toUpperCase)`
						- list is of type <String>
						- e means element or object as list is String so object e also be of String type; can write other letters too
							- in map there is _lambda expression_ called as _arrow token_
							- e is object of String so can call string methods
						- need to change each object to uppercase
						- map method works on each element
				- _in map you can use those methods who returns that object type value for ex. `e` type was String so it returned String type value like in uppercase or lowercase._
			- ### Using Filter and gets strings which starts from 'k'
				- can give conditions returns in boolean
				- `list.stream().distinct`
					- takes only unique elements and remove duplicates
				- `list.stream().filter(e -> e.startsWith("T")`
					- *case sensitive startswith*
				- _You can use those methods in `filter()` who returns in Boolean of that object for example `e`_
					- for example the condition return type is boolean
					- so pass the methods whose return type is boolean
						- e % 2 == 0 -> returns Boolean
						-
				- run from book
				-
			-
-