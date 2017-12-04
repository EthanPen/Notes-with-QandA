1. **getattr()**
2. **callable()**
1. Example of use **re.sub**
2. [What doed the **_yield_** keyword do in python?](http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python)   
3. [How does **sys.stdin** work in Python?](https://www.quora.com/How-does-sys-stdin-work-in-Python)  


###getattr(object, name[, default])

	getattr(object, name[, default])  
Return the value of the named attribute of object. **name must be a string.** If the string is the name of one of the object’s attributes, the result is the value of that attribute. For example, getattr(x, 'foobar') is equivalent to x.foobar. If the named attribute does not exist, default is returned if provided, otherwise AttributeError is raised.


###callable(object)
	callable(object)
Return True if the object argument appears callable, False if not. If this returns true, it is still possible that a call fails, but if it is false, calling object will never succeed. Note that classes are callable (calling a class returns a new instance); class instances are callable if they have a __call__() method.




###1. Example of use re.sub

Here's the example of use re.sun by myself

	>>> import re
	>>> str = 'this is the *World Wide Spam* company!'
	>>> re_str = re.sub(r'\*(.+?)\*', r'<em>\g<1></em>', str)
	>>> re_str
	'this is the <em>World Wide Spam</em> company!'
	>>> re_str = re.sub(r'\*(.+?)\*', r'<em>\g<0></em>', str)
	>>> re_str
	'this is the <em>*World Wide Spam*</em> company!'
	>>> re_str = re.sub(r'\*(.+?)\*', r'<em>\g<2></em>', str)
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/re.py", line 155, in sub
	    return _compile(pattern, flags).sub(repl, string, count)
	  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/re.py", line 291, in filter
	    return sre_parse.expand_template(template, match)
	  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/sre_parse.py", line 833, in expand_template
	    raise error, "invalid group reference"
	sre_constants.error: invalid group reference
	>>>

Python Doc	
**re.sub(pattern, repl, string, count=0, flags=0)**  
Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl. If the pattern isn’t found, string is returned unchanged. repl can be a string or a function; if it is a string, any backslash escapes in it are processed. That is, \n is converted to a single newline character, \r is converted to a carriage return, and so forth. Unknown escapes such as \j are left alone. Backreferences, such as \6, are replaced with the substring matched by group 6 in the pattern. For example:

	>>>
	>>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):',
	...        r'static PyObject*\npy_\1(void)\n{',
	...        'def myfunc():')
	'static PyObject*\npy_myfunc(void)\n{'
	
If repl is a function, it is called for every non-overlapping occurrence of pattern. The function takes a single match object argument, and returns the replacement string. For example:

	>>>
	>>> def dashrepl(matchobj):
	...     if matchobj.group(0) == '-': return ' '
	...     else: return '-'
	>>> re.sub('-{1,2}', dashrepl, 'pro----gram-files')
	'pro--gram files'
	>>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)
	'Baked Beans & Spam'
	
The pattern may be a string or an RE object.

The optional argument count is the maximum number of pattern occurrences to be replaced; count must be a non-negative integer. If omitted or zero, all occurrences will be replaced. Empty matches for the pattern are replaced only when not adjacent to a previous match, so sub('x*', '-', 'abc') returns '-a-b-c-'.

In string-type repl arguments, in addition to the character escapes and backreferences described above, \g<name> will use the substring matched by the group named name, as defined by the (?P<name>...) syntax. \g<number> uses the corresponding group number; \g<2> is therefore equivalent to \2, but isn’t ambiguous in a replacement such as \g<2>0. \20 would be interpreted as a reference to group 20, not a reference to group 2 followed by the literal character '0'. The backreference \g<0> substitutes in the entire substring matched by the RE.


**Q:[What does the yield keyword do in Python?](http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python)**  
**A:** To understand what yield does, you must understand what generators are. And before generators come iterables.

**Iterables**

When you create a list, you can read its items one by one. Reading its items one by one is called iteration:

	>>> mylist = [1, 2, 3]
	>>> for i in mylist:
	...    print(i)
	1
	2
	3
	
mylist is an iterable. When you use a list comprehension, you create a list, and so an iterable:

	>>> mylist = [x*x for x in range(3)]
	>>> for i in mylist:
	...    print(i)
	0
	1
	4
Everything you can use "for... in..." on is an iterable; lists, strings, files...

These iterables are handy because you can read them as much as you wish, **but you store all the values in memory and this is not always what you want when you have a lot of values.**

**Generators**

Generators are iterators, **but you can only iterate over them once.** It's because **they do not store all the values in memory,** they **generate the values on the fly:**

	>>> mygenerator = (x*x for x in range(3))
	>>> for i in mygenerator:
	...    print(i)
	0
	1
	4
It is just the same except you **used ()** instead of **[].** BUT, you **cannot** perform for i in mygenerator a second time since generators can only be used once: they calculate 0, then forget about it and calculate 1, and end calculating 4, one by one.

**Yield**

Yield is a keyword that is used like return, except the function will return a generator.

	>>> def createGenerator():
	...    mylist = range(3)
	...    for i in mylist:
	...        yield i*i
	...
	>>> mygenerator = createGenerator() # create a generator
	>>> print(mygenerator) # mygenerator is an object!
	<generator object createGenerator at 0xb7555c34>
	>>> for i in mygenerator:
	...     print(i)
	0
	1
	4
Here it's a useless example, but it's handy when you know your function will return a huge set of values that you will only need to read once.

To master yield, you must understand that **when you call the function, the code you have written in the function body does not run.** The function only returns the generator object, this is a bit tricky :-)

Then, your code will be run each time the for uses the generator.

Now the hard part:

The first time the for calls the generator object created from your function, it will run the code in your function from the beginning until it hits yield, then it'll return the first value of the loop. Then, each other call will run the loop you have written in the function one more time, and return the next value, until there is no value to return.

The generator is considered empty once the function runs but does not hit yield anymore. It can be because the loop had come to an end, or because you do not satisfy a "if/else" anymore.


**Itertools, your best friend**

The itertools module contains special functions to manipulate iterables. Ever wish to duplicate a generator? Chain two generators? Group values in a nested list with a one liner? Map / Zip without creating another list?

Then just import itertools.

An example? Let's see the possible orders of arrival for a 4 horse race:

	>>> horses = [1, 2, 3, 4]
	>>> races = itertools.permutations(horses)
	>>> print(races)
	<itertools.permutations object at 0xb754f1dc>
	>>> print(list(itertools.permutations(horses)))
	[(1, 2, 3, 4),
	 (1, 2, 4, 3),
	 (1, 3, 2, 4),
	 (1, 3, 4, 2),
	 (1, 4, 2, 3),
	 (1, 4, 3, 2),
	 (2, 1, 3, 4),
	 (2, 1, 4, 3),
	 (2, 3, 1, 4),
	 (2, 3, 4, 1),
	 (2, 4, 1, 3),
	 (2, 4, 3, 1),
	 (3, 1, 2, 4),
	 (3, 1, 4, 2),
	 (3, 2, 1, 4),
	 (3, 2, 4, 1),
	 (3, 4, 1, 2),
	 (3, 4, 2, 1),
	 (4, 1, 2, 3),
	 (4, 1, 3, 2),
	 (4, 2, 1, 3),
	 (4, 2, 3, 1),
	 (4, 3, 1, 2),
	 (4, 3, 2, 1)]
 
**Understanding the inner mechanisms of iteration**

Iteration is a process implying iterables (implementing the _ _  iter _ _ _() method) and iterators (implementing the _ _ _next _ _ _() method). Iterables are any objects you can get an iterator from. Iterators are objects that let you iterate on iterables.

More about it in this article about [how does the for loop work.](http://effbot.org/zone/python-for-statement.htm)



**[Q:How does sys.stdin work in Python?](https://www.quora.com/How-does-sys-stdin-work-in-Python)**  
**A:** First of all lets see what the official Python2 docs say:

	stdin is used for all interpreter input except for scripts 	but including calls to input() and raw_input().
	
[Source: http://docs.python.org/2/library...](http://docs.python.org/2/library...)

They (sys.stdin, sys.stderr and sys.stdout) are better described in Python3 docs however,

	File objects used by the interpreter for standard input, output and errors:
	stdin is used for all interactive input (including calls toinput());
	stdout is used for the output of print() and expressionstatements and for the prompts of input();
	The interpreter’s own prompts and its error messages go to stderr.
	By default, these streams are regular text streams as returned by theopen() function. 
	
[Source: http://docs.python.org/3.3/libra...](http://docs.python.org/3.3/libra...)


What the above means is that, sys.stdin is a File Object that is being used by Python interpreter for input.  
By default, sys.stdin is set to sys.__stdin__ which is input from the standard device. (The values of sys.stdin and sys.__stdin__ may however be None incase no console is connected)  

You can replace the value of sys.stdin by any File-like Object[1], and in effect that File-like object will become the source of you input.  

The below script for Python3 will demonstrate, the idea:

	import sys, io
	string = "A line from the string as stdin IO \n This line wont be read"    # A line of text we'll use as stdin	
	file = open('test.txt')   # A text file we'll use as stdin
	line = input()    # Input from stdin, hopefully keyboard in this case
	print(line)
	sys.stdin = io.StringIO(string)    # Assigning stdin a File-like object from the string
	line = input()    # Read a line from the stdin
	print(line)
	sys.stdin = file    # Assign stdin the file object, so it will read from it
	line = input()    # Read a line from file
	print(line)
	sys.stdin = sys.__stdin__    # Reset the stdin to its default value

Note: Create a "text.txt" file with a few lines of text, in the directory where you store this script and ensure you give it proper permissions if on *nix before running the code. 

Run, the above code to understand what's happening. The inline comments are pretty explanatory.


