- [[Mon, 03.08.2026]]
  collapsed:: true
	- # InputFromKeyboard
	  collapsed:: true
		- `PrintWriter` gets data from keyboard and write in text file set in the path
		- `System.in` gets values from console
		- `InputStreamReader` gets the data which we give as output in console from keyboard ; reads until it gets `exit`
		- `BufferReader` reads that data line by line
			- it has method called `readLine`
			- `readLine` which reads one complete line of text from the keyboard.
		- `(!line.equals("exit"))`
			- it stops reading the data once you write `exit`
		- `out.println(line);`
			- writes line in the file
		- `line = in.readLine();`
			- read next line until we get `exit`
		- close all the objects.
	- # ReadAndWriteValidEmails
	  collapsed:: true
		- source has all text containing both valid emails as well as other texts
		- target will only have texts which are valid emails
		- ```java
		  FileReader source = new FileReader("C:\\iofolder\\Hello.txt");
		  FileWriter target = new FileWriter("C:\\iofolder\\rays.txt");
		  ```
		- email should end with `@gmail.com`
			- reads but doesn't write the data
			-
	- # ReadAndWriteBinaryFile
	  collapsed:: true
		- ```java
		  FileInputStream in = new FileInputStream(source); // read binary data
		  FileOutputStream out = new FileOutputStream(target); // write binary
		  ```
			- it takes data from source copy it and paste it in target
			- `i = in.read();` in while loop it reads again and again until we get -1
	- # TestScanner
	  collapsed:: true
		- Scanner is predefined class.
		- it scans values by getting output from console by user.
		- `System.in` for input once scanner class get the input and you need to find which type is that
			- for integer values use sc.nextInt()
			- sc.next() -> single word
			- sc.nextLine() -> a sentence
			-
		- `System.out` for output
		- it scans whatever you write and scans then as per value stores in variable for ex. int stores in int variable
		- `intValue = sc.nextInt();` stores int value
		-
	- # TestFileSplit
		- if file has 10 line of text it will create 10 new files
		-
-
	-