- ```java
  package arrays;
  //TODO find index of an element in an array
  public class FindIndexOfElement {
  	public static void main(String[] args) {
  		
  		int[] arr = { 10, 20, 30, 40, 50, 60 };
  		int element = 60;
  
  		for (int i = 0; i < arr.length; i++) {
  			if (arr[i] == element) {
  				System.out.println("Index of " + arr[i] + " is " + i);
  			}
  		}
  	}
  }
  
  ```