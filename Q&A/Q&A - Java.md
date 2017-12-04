## Q&A - Java

Tags: Ethan.Penx

---

####1. [Java String import](http://stackoverflow.com/questions/7953987/java-string-import)

String is present in package **java.lang** which is imported by default in all java programs.

####2. [What is the difference between Integer and int in Java?](http://stackoverflow.com/questions/8660691/what-is-the-difference-between-integer-and-int-in-java)

**int is a primitive type.** Variables of type int store the actual binary value for the integer you want to represent. int.parseInt("1") doesn't make sense because int is not a class and therefore doesn't have any methods.

**Integer is a class,** no different from any other in the Java language. Variables of type Integer store references to Integer objects, just as with any other reference (object) type. Integer.parseInt("1") is a call to the static method parseInt from class Integer (note that this method actually returns an int and not an Integer).

####3. [Division of integers in Java](http://stackoverflow.com/questions/7220681/division-of-integers-in-java)

Converting the output is too late; the calculation has already taken place in integer arithmetic. You need to convert the inputs to double:

	System.out.println((double)completed/(double)total);
	
Note that you don't actually need to convert both of them; so long as one is double, the other will be implicitly converted. But I prefer to do both, for symmetry.

PS: [Why is the result of 1/3 == 0?](http://stackoverflow.com/questions/4685450/why-is-the-result-of-1-3-0)

####4. [Initializing multiple variables to the same value in Java](http://stackoverflow.com/questions/6202818/initializing-multiple-variables-to-the-same-value-in-java)

	String one, two, three;
	one = two = three = "";
	
This should work with immutable objects. It doesn't make any sense for mutable objects for example:

	Person firstPerson, secondPerson, thirdPerson;
	firstPerson = secondPerson = thirdPerson = new Person();
	
All the variables would be pointing to the same instance. Probably what you would need in that case is:

	Person firstPerson = new Person();
	Person secondPerson = new Person();
	Person thirdPerson = new Person();
	
Or better yet use an array or Collection.


####5. [What is a NullPointerException, and how do I fix it?](http://stackoverflow.com/questions/218384/what-is-a-nullpointerexception-and-how-do-i-fix-it)

When you declare a reference variable (i.e. an object) you are really creating a pointer to an object. Consider the following code where you declare a variable of primitive type int:

	int x;
	x = 10;
	
In this example the variable x is an int and Java will initialize it to 0 for you. When you assign it to 10 in the second line your value 10 is written into the memory location pointed to by x.

But, when you try to declare a reference type something different happens. Take the following code:

	Integer num;
	num = new Integer(10);
	
The first line declares a variable named num, but, it does not contain a primitive value. Instead it contains a pointer (because the type is Integer which is a reference type). Since you did not say as yet what to point to Java sets it to null, meaning "I am pointing at nothing".

In the second line, the new keyword is used to instantiate (or create) an object of type Integer and the pointer variable num is assigned this object. You can now reference the object using the dereferencing operator . (a dot).

The Exception that you asked about occurs when you declare a variable but did not create an object. If you attempt to dereference num BEFORE creating the object you get a NullPointerException. In the most trivial cases the compiler will catch the problem and let you know that "num may not have been initialized" but sometime you write code that does not directly create the object.

For instance you may have a method as follows:

	public void doSomething(SomeObject obj){
	   //do something to obj
	}
	
in which case you are not creating the object obj, rather assuming that is was created before the doSomething method was called. Unfortunately it is possible to call the method like this:

	doSomething(null);
	
in which case obj is null. If the method is intended to do something to the passed-in object, it is appropriate to throw the NullPointerException because it's a user error and the user will need that information for debugging purposes.

Alternatively, there may be cases where the purpose of the method is not solely to operate on the passed in object, and therefore a null parameter may be acceptable. In this case, you would need to check for a null parameter and behave differently. You should also explain this in the documentation. For example, doSomething could be written as:

	/**@param obj An optional foo for ____. May be null, in which case 
	*  the result will be ____. */
	public void doSomething(SomeObject obj){
	    if(obj != null){
	       //do something
	    } else {
	       //do something else
	    }
	}

Finally, [How to pinpoint the exception location & cause using Stack Trace](http://stackoverflow.com/questions/3988788/what-is-a-stack-trace-and-how-can-i-use-it-to-debug-my-application-errors)

####6. [Java – Convert String to int](https://www.mkyong.com/java/java-convert-string-to-int/)

In Java, you can use Integer.parseInt() to convert a String to int.

** 1. Integer.parseInt() Examples **

Example to convert a String “10” to an primitive int.

	String number = "10";
	int result = Integer.parseInt(number);
	System.out.println(result);
Output	
	
	10
	
** 2. Integer.valueOf() Examples **

Alternatively, you can use Integer.valueOf(), it will returns an Integer object.

	String number = "10";
	Integer result = Integer.valueOf(number);
	System.out.println(result);
Output

	10
_Note_  
In summary, parseInt(String) returns a primitive int, whereas valueOf(String) returns a new Integer() object.

** 3. NumberFormatException **
If the string does not contain a parsable integer, a NumberFormatException will be thrown.

	String number = "10A";
	int result = Integer.parseInt(number);
	System.out.println(result);
Output

	Exception in thread "main" java.lang.NumberFormatException: For input string: "10A"
		at java.lang.NumberFormatException.forInputString(Unknown Source)
		at java.lang.Integer.parseInt(Unknown Source)
		at java.lang.Integer.valueOf(Unknown Source)
		
		

