- [[Sat, 04.07.2026]]
	- `arrays.length - 1`
		- gives last index
	- ### Ascending sorting Arrays [[Arrays]]
	  collapsed:: true
		- ```java
		  // Is this new number smaller than my current second minimum"
		  			// If yes, replace it.
		  			if (arr[i] > min && secondmin < arr[i]) {
		  ```
		-
- [[Sun, 05.07.2026]]
  collapsed:: true
	- ### bubble sort a.k.a. ascending order
		- ```java
		  package arrays;
		  // bubble sort 
		  public class ArraySorting {
		  
		  	public static void main(String[] args) {
		  
		  		int[] arr = { 20, 10, 50, 30, 40 };
		  		int temp = 0;
		  
		  		for (int i = 0; i < arr.length; i++) {
		  			for (int j = i + 1; j < arr.length; j++) {
		  				if (arr[j] < arr[i]) {
		  					System.out.println();
		  					temp = arr[j];   // temp = 10
		  					arr[j] = arr[i]; // 20, 10.. -> 20, 20..
		  					arr[i] = temp;   // 20, 20 .. -> temp, 20 -> 10, 20
		  				}
		  			}
		  
		  			System.out.println(arr[i]);
		  		}
		  
		  	}
		  
		  }
		  
		  
		  ```
		- what we are doing here is:
			- comparing `index 1` with `index 0`;
			- if `index 1` < `index 0` place `index 1` to `temp` to use it later
				- `index 0` assigned to `index 1` such that value of `0` and `1` will be same
				- basically we are swapping values so that first will be least number
				-
				-