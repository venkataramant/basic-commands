# varargs
	accept variable number of values is called varargs

```java

```
# Credits
	https://stackoverflow.com/questions/2925153/can-i-pass-an-array-as-arguments-to-a-method-with-variable-arguments-in-java
	
	1. Varargs gotchas #1: passing null
		count(null, null, null); // prints "3"
		count(null, null); // prints "2"
		count(null); // throws java.lang.NullPointerException!!!
		
		count(new Object[] { null }); // prints "1"
		count((Object) null); // prints "1"
	2. Vararg gotchas #2: adding extra arguments
		 String[] myArgs = { "A", "B", "C" };
	    System.out.println(ezFormat(myArgs, "Z"));
	    // prints "[ [Ljava.lang.String;@13c5982 ][ Z ]"
	3. Varargs gotchas #3: passing an array of primitives
		 //Autoboxing does not apply to array of primitives.
		 int[] myNumbers = { 1, 2, 3 };
		 System.out.println(ezFormat(myNumbers));
		 // prints "[ [I@13c5982 ]"
		 
		  Integer[] myNumbers = { 1, 2, 3 };
    		  System.out.println(ezFormat(myNumbers));
          // prints "[ 1 ][ 2 ][ 3 ]"