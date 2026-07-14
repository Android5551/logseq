- [[Mon, 13.07.2026]]
	- When to use:
		- When Parent need to provide general behavior
		- When Child need to provide special behavior
	- The methods which is common to all child classes; gives different outputs; make that method to parent; so child can  override that method;
		- #+BEGIN_NOTE
		  Until and unless we overwrite the behavior will be generalized
		  #+END_NOTE
		- If done only override only parent class method will be called out
			- rewrites done when we remove `super.method()` and write our own code then only child class method will be called out.
		- `Green dot` shows method overrides previous method
		- example Shape has area can be rewritten by Triangle or it chooses not to.
		- example `papa ki paan ki dukan ; son 1 -> unemployed son 2 -> ips; paan ki dukan son 1 -> generalized son 2 -> specialized`
		- if child is specialized method will be called through Shape otherwise if child is generalized; method will be called through Circle.
	-