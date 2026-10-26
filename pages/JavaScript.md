- CheckBox Select All
	- A checkbox inside a table header cell. `onclick` runs the JavaScript each time you click it.
		- ```js
		  document.querySelectorAll('input[name=ids]')
		  ```
			- Finds **every** checkbox on the page whose `name` is `ids`. These are your row checkboxes. The result is a list of them.
		- ```js
		  .forEach(c => c.checked = this.checked)
		  ```
			- Goes through that list one by one. Each checkbox is called `c` in turn, and for each one it sets:
		- ```
		  c.checked = this.checked
		  ```
			- `this` is the header checkbox you just clicked, so `this.checked` is `true` if it’s now ticked and `false` if it’s unticked. Every row checkbox is set to match it.
	- ### Example
		- You have 3 row checkboxes (A, B, C) and click the header checkbox:
		- Header becomes ticked, so `this.checked = true`, and A, B, C all become ticked.
		- Click it again: `this.checked = false`, and A, B, C all become unticked.
	- ### The arrow  `=>`
	  `c => c.checked = this.checked` is a short way to write a small function that takes `c` and does the assignment. It means “for each checkbox c, do this”.