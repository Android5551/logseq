# Playground 1
	- # hi this is h1
	- ## hi this is h2
	- ### hi this is h3
	- #### hi this is h4
	- ##### hi this is h5
	- ###### hi this is h6
	- ---
	- ==highlight==
	- _italics_
	- **bold**
	- `this is the code`
	- <ins>underline</ins>
	- [[Mon, 20.07.2026]]
	- [#A] test
	- ```calc
	  
	  ```
		- This is code
			- ``` java
			  public void method(){
			    system.out.println("hello");
			  }
			  
			  ```
	- #+BEGIN_NOTE
	  Note
	  #+END_NOTE
	- #+BEGIN_TIP
	  Tip
	  #+END_TIP
	- #+BEGIN_IMPORTANT
	  Imp
	  #+END_IMPORTANT
	- #+BEGIN_CAUTION
	  Caution
	  #+END_CAUTION
	- #+BEGIN_EXAMPLE
	  example
	  #+END_EXAMPLE
	- #+BEGIN_VERSE
	  this is verse i dont
	  know what is that
	  #+END_VERSE
	- #+BEGIN_CENTER
	  Center
	  #+END_CENTER
	- #+BEGIN_COMMENT
	  this is the
	  comment
	  #+END_COMMENT
	- #+BEGIN_EXPORT ascii
	  and this is ascii
	  #+END_EXPORT
- ## Testing models
	- collapsed:: true
	  ```bash
	  ollama create logseq-3-4 -f Modelfile
	  ```
	- ```java
	  System.out.println("Hello");
	  ```
- Testing
  collapsed:: true
	- Comparator
		-
		- A **comparator** is a function or object that defines the **ordering** of elements in a collection, enabling operations like sorting, searching, or comparing items based on specific criteria. It is a fundamental concept in programming and data structures, used across languages and paradigms. Here's a structured breakdown:
		  
		  ---
		  
		  ### **1. Core Purpose**
		  A comparator determines how two elements should be ordered relative to each other. It answers the question:  
		  **"Given two elements, which one comes first?"**  
		  This is critical for tasks like:
		  - Sorting arrays/lists (e.g., ascending/descending order).
		  - Searching (e.g., binary search requires ordered data).
		  - Custom comparisons (e.g., sorting by name, date, or priority).
		  
		  ---
		  
		  ### **2. Key Characteristics**
		  - **Comparison Logic**: Defines rules for ordering (e.g., numeric, lexicographic, or custom).
		  - **Flexibility**: Can be tailored to specific use cases (e.g., sorting by price, then by rating).
		  - **Reusability**: Often encapsulated as a function or class for reuse.
		  
		  ---
		  
		  ### **3. Implementation Examples**
		  
		  #### **A. In Python**
		  ```python
		  # Custom sort by length of strings
		  words = ["apple", "banana", "cherry", "date"]
		  words.sort(key=lambda x: len(x))
		  print(words)  # Output: ['date', 'apple', 'cherry', 'banana']
		  ```
		  
		  #### **B. In Java**
		  ```java
		  // Sorting by string length
		  List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
		  words.sort((a, b) -> Integer.compare(a.length(), b.length()));
		  System.out.println(words);  // Output: [date, apple, cherry, banana]
		  ```
		  
		  #### **C. In JavaScript**
		  ```javascript
		  // Sorting by string length
		  let words = ["apple", "banana", "cherry", "date"];
		  words.sort((a, b) => a.length - b.length);
		  console.log(words);  // Output: ['date', 'apple', 'cherry', 'banana']
		  ```
		  
		  ---
		  
		  ### **4. Key Considerations**
		  - **Stability**: Ensure the sort is stable if multiple criteria are involved.
		  - **Performance**: For large datasets, use efficient sorting algorithms (e.g., Timsort in Python, which is used in Java and JavaScript).
		  - **Custom Comparators**: Use custom comparator functions when sorting by non-default criteria.
		  - **Edge Cases**: Handle empty arrays, single-element arrays, or null/undefined values appropriately.
		  
		  ---
		  
		  ### **5. Example with Multiple Criteria**
		  If you need to sort by multiple fields (e.g., first by name, then by age), you can extend the comparator:
		  
		  #### **Python**
		  ```python
		  people = [
		      {"name": "Alice", "age": 30},
		      {"name": "Bob", "age": 25},
		      {"name": "Alice", "age": 22}
		  ]
		  
		  people.sort(key=lambda x: (x["name"], x["age"]))
		  ```
		  
		  #### **JavaScript**
		  ```javascript
		  const people = [
		      { name: "Alice", age: 30 },
		      { name: "Bob", age: 25 },
		      { name: "Alice", age: 22 }
		  ];
		  
		  people.sort((a, b) => {
		      if (a.name !== b.name) {
		          return a.name.localeCompare(b.name);
		      }
		      return a.age - b.age;
		  });
		  ```
		  
		  #### **Python**
		  ```python
		  people = [
		      {"name": "Alice", "age": 30},
		      {"name": "Bob", "age": 25
- | Comparable | Comparator |
  | ---------- | ---------- |
  | Provides default sorting | Provides custom sorting |
  | Implemented inside the class | Usually implemented outside the class |
  | Contains `compareTo()` | Contains `compare()` |
  | Only one natural ordering | Multiple sorting orders possible |
- # Comparator
- `Comparator` is one of the most commonly used ways to sort objects in Java.
- It is used when sorting can be performed on different attributes of a class.
- At a time, only **one Comparator object** is used for sorting.
- A single class can have **multiple Comparator implementations**.
- The number of Comparators depends on the number of sorting requirements.
- ### Example
  
  Suppose a `Product` class has 3 attributes:
- id
- name
- price
  
  Possible Comparators:
- Sort by name (Ascending)
- Sort by name (Descending)
- Sort by price (Ascending)
- Sort by price (Descending)
- Sort by id (Ascending)
- Sort by id (Descending)
  
  So, 3 attributes can have multiple Comparators depending on business requirements.
  
  ---
- ## Comparator Interface
  
  ```
  public interface Comparator<T> {
  
    int compare(T o1, T o2);
  
  }
  ```
- ### compare() Method
  
  ```
  int compare(T o1, T o2);
  ```
- Receives two objects for comparison.
- Returns:
	- Negative value → `o1` comes before `o2`
	- Positive value → `o1` comes after `o2`
	- Zero → both objects are considered equal
	  
	  Example:
	  
	  ```
	  public int compare(Product p1, Product p2) {
	  
	   return p1.price - p2.price;
	  
	  }
	  ```
	  
	  ---
- ## Why Comparator is Implemented in Another Class
  
  Generally, Comparator is implemented in a separate class because:
- One class can have multiple sorting criteria.
- Keeping sorting logic separate follows the **Separation of Concerns** principle.
- The main entity class remains clean and focused on storing data.
  
  Example:
  
  ```
  class Product {
  
    public int id;
  
    public String name;
  
    public int price;
  
  }
  ```
  
  ```
  class PriceComparator implements Comparator<Product> {
  
    public int compare(Product p1, Product p2) {
  
        return p1.price - p2.price;
  
    }
  
  }
  ```
  
  ```
  class NameComparator implements Comparator<Product> {
  
    public int compare(Product p1, Product p2) {
  
        return p1.name.compareTo(p2.name);
  
    }
  
  }
  ```
  
  ---
- ## Public vs Private Attributes
- ### Public Attributes
  
  ```
  public int price;
  ```
- Comparator can access the field directly.
  
  ```
  return p1.price - p2.price;
  ```
- ### Private Attributes
  
  ```
  private int price;
  ```
- Direct access is not allowed outside the class.
- Getter methods must be used.
  
  ```
  public int getPrice() {
  
    return price;
  
  }
  ```
  
  ```
  return p1.getPrice() - p2.getPrice();
  ```
  
  **Best Practice:** Keep attributes `private` and use getters. This follows the principle of **Encapsulation**.
  
  ---
- ## Sorting Using Collections.sort()
  
  In the main method, both:
- Collection object (List)
- Comparator object
  
  are passed to `Collections.sort()`.
  
  ```
  Collections.sort(productList, new PriceComparator());
  ```
  
  or
  
  ```
  Collections.sort(productList, new NameComparator());
  ```
  
  Here:
- `productList` → collection to be sorted
- `PriceComparator()` / `NameComparator()` → sorting logic
  
  ---
- ## Comparator vs Comparable
  
  | Comparable | Comparator |
  | ---- | ---- | ---- |
  | Provides default sorting | Provides custom sorting |
  | Implemented inside the class | Usually implemented outside the class |
  | Contains `compareTo()` | Contains `compare()` |
  | Only one natural ordering | Multiple sorting orders possible |
  
  Example:
  
  ```
  Collections.sort(productList);
  ```
  
  Uses `Comparable`.
  
  ```
  Collections.sort(productList, new PriceComparator());
  ```
  
  Uses `Comparator`.
  
  ---
- ## Key Points
- Used for **custom sorting**.
- One class can have **multiple Comparators**.
- Comparator interface contains the `compare()` method.
- Sorting logic is usually kept in separate classes.
- Best practice is to keep attributes `private` and access them through getters.
- `Collections.sort(list, comparator)` requires both a collection and a Comparator object.
- Comparator is preferred when objects need to be sorted on different attributes.
-
- ---
- # Comparator
- Most commonly used for custom sorting in Java.
- Used when objects need to be sorted based on different attributes.
- At a time, only one Comparator object is used for sorting.
- One class can have multiple Comparator implementations.
- Number of Comparators depends on the number of sorting requirements.
- ## Example
- Suppose Product has:
	- id
	- name
	- price
- Possible Comparators:
	- Sort by Name Ascending
	- Sort by Name Descending
	- Sort by Price Ascending
	- Sort by Price Descending
	- Sort by Id Ascending
	- Sort by Id Descending
- Therefore, one class can have multiple Comparators based on business requirements.
- ## Comparator Interface
  
  ```
  public interface Comparator<T> {
    int compare(T o1, T o2);
  }
  ```
- ## compare() Method
  
  ```
  int compare(T o1, T o2);
  ```
- Receives two objects for comparison.
- Used to define custom sorting logic.
- ### Return Values
- Negative value
	- o1 comes before o2
- Positive value
	- o1 comes after o2
- Zero
	- Both objects are considered equal
- ### Example
  
  ```
  public int compare(Product p1, Product p2) {
    return p1.price - p2.price;
  }
  ```
- ## Why Comparator is Implemented in Another Class
- One class can have multiple sorting criteria.
- Keeping sorting logic separate makes code cleaner.
- Follows Separation of Concerns (SoC).
- Entity class remains focused on storing data only.
- ### Product Class
  
  ```
  class Product {
    public int id;
    public String name;
    public int price;
  }
  ```
- ### Price Comparator
  
  ```
  class PriceComparator implements Comparator<Product> {
  
    public int compare(Product p1, Product p2) {
        return p1.price - p2.price;
    }
  }
  ```
- ### Name Comparator
  
  ```
  class NameComparator implements Comparator<Product> {
  
    public int compare(Product p1, Product p2) {
        return p1.name.compareTo(p2.name);
    }
  }
  ```
- ## Public vs Private Attributes
- ### Public Attributes
  
  ```
  public int price;
  ```
- Comparator can access the field directly.
  
  ```
  return p1.price - p2.price;
  ```
- ### Private Attributes
  
  ```
  private int price;
  ```
- Direct access is not allowed outside the class.
- Getter methods must be used.
  
  ```
  public int getPrice() {
    return price;
  }
  ```
  
  ```
  return p1.getPrice() - p2.getPrice();
  ```
- ### Best Practice
- Keep attributes private.
- Use getter methods to access them.
- Follows Encapsulation principle.
- ## Sorting Using Collections.sort()
- In main method, both:
	- Collection object (List)
	- Comparator object
	  
	  are passed to Collections.sort().
- ### Sort by Price
  
  ```
  Collections.sort(productList, new PriceComparator());
  ```
- ### Sort by Name
  
  ```
  Collections.sort(productList, new NameComparator());
  ```
- ### Parameters
- productList
	- Collection to be sorted
- Comparator Object
	- Defines sorting logic
- ## Comparator vs Comparable
  
  | Comparable | Comparator |
  | ---- | ---- | ---- |
  | Provides default sorting | Provides custom sorting |
  | Implemented inside class | Usually implemented outside class |
  | Contains compareTo() | Contains compare() |
  | Only one natural ordering | Multiple sorting orders possible |
- ## Comparable Example
  
  ```
  Collections.sort(productList);
  ```
- Uses Comparable.
- Uses natural/default ordering.
- ## Comparator Example
  
  ```
  Collections.sort(productList, new PriceComparator());
  ```
- Uses Comparator.
- Uses custom ordering.
- ## Key Points
- Used for custom sorting.
- One class can have multiple Comparators.
- Comparator interface contains compare() method.
- compare() compares two objects.
- Sorting logic is usually implemented in separate classes.
- Best practice is to keep attributes private and use getters.
- Collections.sort(list, comparator) accepts both List and Comparator objects.
- Preferred when multiple sorting criteria are required.
- ---
- # Comparator
	- Most commonly used for custom sorting in Java.
	- Used when objects need to be sorted based on different attributes.
	- At a time, only one Comparator object is used for sorting.
	- One class can have multiple Comparator implementations.
	- Number of Comparators depends on the number of sorting requirements.