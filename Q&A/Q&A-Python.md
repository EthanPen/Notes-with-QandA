### Q&A - Python

Tags: Ethan.Penx

---

[TOC]

####1.Python 中使用 BeautifulSoup  CSS selector错误

example:  
​		
	wb_data = requests.get(url)
	soup = BeautifulSoup(wb_data.content, 'lxml')
	print type(soup)
	links = soup.select('ul.ym-submnu > li > b > a')
	
	## error 
	<class 'bs4.BeautifulSoup'
	TypeError: 'NoneType' object is not callable

报 NoneType 错误，但是  print type(soup) 却又是 <class 'bs4.BeautifulSoup'>
经过 N 久的查、问，发现其他人能正常使用，开始怀疑平台、环境问题!
最后重装库 BeautifulSoup 解决，能正常使用。  
 	
 	xing$  sudo pip uninstall beautifulsoup4
 	...
 	xing$ sudo pip install beautifulsoup4

####2.string & unicode
Your procedure's fine, you just need 1 more step; that is, encoding from unicode to utf-8 (or any other encoding that supports the 'weird characters'.)

Think of decoding as what you do to go from a regular string to unicode and encoding as what you do to get back from unicode. In other words:

* You de - code a str to produce a unicode string

* and en - code a unicode string to produce an str.


So:

	params = {'weird-chars': u'\xb0\xe7'}
	encodedchars = params['weird-chars'].encode('utf-8')
	encodedchars will contain your characters, displayed in the selected encoding (in this case, utf-8).

#### 3.SyntaxError: Non-ASCII character '\xef' in file 

[http://stackoverflow.com/questions/10589620/syntaxerror-non-ascii-character-xa3-in-file-when-function-returns-%C2%A3](http://stackoverflow.com/questions/10589620/syntaxerror-non-ascii-character-xa3-in-file-when-function-returns-%C2%A3)

**A:**   
I'd recommend reading that PEP the error gives you. The problem is that your code is trying to use the ASCII encoding, but the pound symbol is not an ASCII character. 

Try using UTF-8 encoding. You can start by putting # -*- coding: utf-8 -*- at the top of your .py file. To get more advanced, you can also define encodings on a string by string basis in your code. 

However, if you are trying to put the pound sign literal in to your code, you'll need an encoding that supports it for the entire file.

#### 4. OSX El Capitan: sudo pip install OSError: [Errno: 1] Operation not permitted  

[http://stackoverflow.com/questions/33004708/osx-el-capitan-sudo-pip-install-oserror-errno-1-operation-not-permitted](http://stackoverflow.com/questions/33004708/osx-el-capitan-sudo-pip-install-oserror-errno-1-operation-not-permitted)

Instructions telling sudo pip install are inherently wrong.

If there is any tutorial out there which says you should do sudo pip then please file a bug against this package. The author is dis-educating Python community, as time has proven sudo pip to be a broken practice.

OSX El Capitan introduced a mechanisms to prevent damaging the operating system files. /System/Library/Frameworks/Python.framework/Versions/2.7/share is one of the protected locations. 

A normal user has no reason to put or write any files there. This is because the operating system itself relies on these files and sudo pip, with all force given from the above, would unconditionally overwrite them. Usually bad things would not happen, but the chances are there. Apple wants to protect their OS users to accidentally bricking their installation.

Instead, you need to install a Python package, like IPython, locally to the home folder of your user. The easiest way is to create a virtual environment, activate it and then run pip in the virtual environment.

Example:

	cd ~  # Go to home directory
	virtualenv my-venv
	source my-venv/bin/activate
	pip install IPython

More info

* [Official Python package installation tutorial.](https://packaging.python.org/installing/)
* [How to create virtual environments.](https://packaging.python.org/installing/#creating-virtual-environments)

Alternatively, one should be able to do pip install --user. But again, no sudo needed.

#### 5.Retrieving python module path

[http://stackoverflow.com/questions/247770/retrieving-python-module-path](http://stackoverflow.com/questions/247770/retrieving-python-module-path)

	import a_module
	print a_module.__file__

Will actually give you the path to the .pyc file that was loaded, at least on Mac OS X. So I guess you can do

	import os
	path = os.path.dirname(amodule.__file__)

You can also try

	path = os.path.abspath(amodule.__file__)  	
To get the directory to look for changes.

#### 6. What is the difference between Jupyter and IPython Notebook?

[https://www.quora.com/What-is-the-difference-between-Jupyter-and-IPython-Notebook](https://www.quora.com/What-is-the-difference-between-Jupyter-and-IPython-Notebook)

Perhaps the shortest answer is in the Jupyter documentation:  
> The Jupyter Notebook used to be called the IPython Notebook.

And, somewhat more verbosely, at the IPython web site:
> As of IPython 4.0, the language-agnostic parts of the project: the notebook format, message protocol, qtconsole, notebook web application, etc. have moved to new projects under the name Jupyter. IPython itself is focused on interactive Python, part of which is providing a Python kernel for Jupyter.

IPython Notebook was accumulating additional backend languages, making the name confusing.  So the project was reorganized to reflect the architecture: a language-independent notebook that works with various language "kernels".  The notebook server itself is written in Python, but the frontend/backend interaction is  language-independent.  This makes Python just another backend as far as the notebook is concerned.


#### 7.Generate random integers between x and y

[http://stackoverflow.com/questions/3996904/generate-random-integers-between-0-and-9](http://stackoverflow.com/questions/3996904/generate-random-integers-between-0-and-9)

Try:

	from random import randint
	print randint(0,9)


#### 8 Python requests“Max retries exceeded with url” error

[http://blog.csdn.net/shi_weihappy/article/details/51009602](http://blog.csdn.net/shi_weihappy/article/details/51009602)


今天写Python网络爬虫的时候遇到一个问题，报错的具体内容如下：

	HTTPConnectionPool(host='dds.cr.usgs.gov', port=80): Max retries exceeded with url: /ltaauth//sno18/ops/l1/2016/138/037/LC81380372016038LGN00.tar.gz?id=stfb9e0bgrpmc4j9lcg45ikrj1&iid=LC81380372016038LGN00&did=227966479&ver=production (Caused by NewConnectionError('<requests.packages.urllib3.connection.HTTPConnection object at 0x105b9d210>: Failed to establish a new connection: [Errno 65] No route to host',))


多方查阅后发现了解决问题的原因：http连接太多没有关闭导致的。

解决办法：

1、增加重试连接次数

	requests.adapters.DEFAULT_RETRIES = 5

2、关闭多余的连接

requests使用了urllib3库，默认的http connection是keep-alive的，requests设置False关闭。
操作方法

	s = requests.session()
	  s.keep_alive = False


#### 9 Max retries

[http://stackoverflow.com/questions/23013220/max-retries-exceeded-with-url](http://stackoverflow.com/questions/23013220/max-retries-exceeded-with-url)

What happened here is that itunes server refuses your connection (you're sending too many requests from same ip address in short period of time)

> Max retries exceeded with url: /in/app/adobe-reader/id469337564?mt=8

error trace is misleading it should be something like "No connection could be made because the target machine actively refused it".

There is an issue at about python.requests lib at Github, check it out here

To overcome this issue (not so much an issue as it is misleading debug trace) you should catch connection related exceptions like so:

	try:
	    page1 = requests.get(ap)
	except requests.exceptions.ConnectionError:
	    r.status_code = "Connection refused"

Another way to overcome this problem is if you use enough time gap to send requests to server this can be achieved by sleep(timeinsec) function in python (don't forget to import sleep)

	from time import sleep

All in all requests is awesome python lib, hope that solves your problem.

####10. [Does python have generic methods?](http://stackoverflow.com/questions/20449398/does-python-have-generic-methods)

No. Python is not a statically typed language, so there is no need for them. Java generics only provide compile time type safety; they don't do anything at runtime. Python doesn't have any compile time type safety, so it wouldn't make sense to add generics to beef up the compile time type checks Python doesn't have.

A list, for example, is an untyped collection. There is no equivalent of distinguishing between List<Integer> and List<String> because a Python list can store any type of object.

#### 11. [[beautiful soup 遇到class标签的值中含有空格的处理](http://www.cnblogs.com/elodio/p/how_to_deal_with_class_tag_including_space_using_beautifulsoup.html)](http://www.cnblogs.com/elodio/p/how_to_deal_with_class_tag_including_space_using_beautifulsoup.html)

用Python写一个爬虫，用BeautifulSoup解析html。
其中一个地方需要抓取下面两类标签：

```
<dd class="ab "   >blabla1</dd>
<dd class="ab cd" >blabla2</dd>
```

第一类class的值的末尾有一个空格。
第二类class的值中间有一个空格，而且开头部分和第一类相同。

在css中，class的值不应该有空格，所以第一类会忽略空格，第二类会被当做多值属性。参考官方文档[多值属性](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html#id12)。

所以在处理时也不需再考虑class值中的空格。

传入参数时用列表过滤器是最方便的，如下:

```
soup.find_all("dd", class_= ["ab", "cd"])
```



[Stackoverflow: Beautifulsoup multiple class selector](http://stackoverflow.com/questions/40305678/beautifulsoup-multiple-class-selector)

Use `css selectors` instead:

```python
soup.select('div.A.B')
```

#### 12 [Usage of unicode() and encode() functions in Python](http://stackoverflow.com/questions/10288016/usage-of-unicode-and-encode-functions-in-python)

You are using `encode("utf-8")` incorrectly. Python byte strings (`str` type) have an encoding, Unicode does not. You can convert a Unicode string to a Python byte string using `uni.encode(encoding)`, and you can convert a byte string to a Unicode string using `s.decode(encoding)` (or equivalently, `unicode(s, encoding)`).

If `fullFilePath` and `path` are currently a `str` type, you should figure out how they are encoded. For example, if the current encoding is utf-8, you would use:

```
path = path.decode('utf-8')
fullFilePath = fullFilePath.decode('utf-8')
```

If this doesn't fix it, the actual issue may be that you are not using a Unicode string in your `execute()` call, try changing it to the following:

```
cur.execute(u"update docs set path = :fullFilePath where path = :path", locals())
```