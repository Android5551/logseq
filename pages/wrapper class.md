- A **wrapper class** is a class that wraps (converts) a primitive data type into an object.
  id:: 6a4dca61-55fc-43e8-a9c5-78c2ba4d20c6
- Java provides a wrapper class for each primitive data type.
- ### Primitive ↔ Wrapper Class
  
  | Primitive | Wrapper Class |
  | ---- | ---- | ---- |
  | `byte` | `Byte` |
  | `short` | `Short` |
  | `int` | `Integer` |
  | `long` | `Long` |
  | `float` | `Float` |
  | `double` | `Double` |
  | `char` | `Character` |
  | `boolean` | `Boolean` |
- ### Example
  
  ```
  int num = 10;
  Integer obj = Integer.valueOf(num);
  
  System.out.println(obj);
  ```
  
  Output:
  
  ```
  10
  ```
- ### Why do we need Wrapper Classes?
- Convert primitive data types into objects.
- Required when working with Java Collections (`ArrayList`, `HashMap`, etc.), which store objects, not primitives.
- Provide useful utility methods.
  
  Example:
  
  ```
  Integer.parseInt("100");      // Converts String to int
  Character.isDigit('5');       // Checks if character is a digit
  Double.parseDouble("12.5");   // Converts String to double
  ```