- [[Mon, 06.07.2026]]
- `Object` is the parent class of all classes in Java. Every class directly or indirectly inherits from `Object`, so every object can use the methods defined in the `Object` class.
	- Every Java class ultimately inherits from `Object`, either directly or through another class.
	- Since every class extends `Object`, every object gets common methods such as:
		- Common methods: 
		  | Method | Purpose |
		  | ---- | ---- | ---- |
		  | `toString()` | Returns string representation of the object |
		  | `equals()` | Compares two objects; checks by value |
		  | `hashCode()` | Returns hash code of the object |
		  | `getClass()` | Returns the object's class |
		  | `clone()` | Creates a copy of the object |
		  | `wait()` | Causes current thread to wait |
		  | `notify()` | Wakes one waiting thread |
		  | `notifyAll()` | Wakes all waiting threads |
		- <!--EndFragment-->