* Flask-Moment  ---Chapter3.6   
Flask-Moment是一个扩展，能把**moment.js**(一个实用javascript开发的优秀客户端开源代码库)即成到Jinja2模版中。  其实除了moment.js，Flask-Moment还依赖**jquery.js**。要在HTML文档到某个地方引入这两个库，可以直接引入，这样可以选择使用哪个版本，也可以使用扩展提供的辅助函数，从CDN(Content Dlivery Network, 内容分发网络)中引入通过测试的版本。而**Bootstrap中已经引入了jquery.js，因此只需引入moment.js**。

		(ven) xing$ pip install flask-moment
		
* [Flask-WTF](http://pythonhosted.org/Flask-WTF)  ---Chapter4  
这个扩展在**处理Web表单的过程**方面有很好的体验，它也对[WTForms](http://wtforms.simplecodes.com/)包进行了包装，方便即成到Flask程序中.
	
		(ven) xing$ pip install flask-wtf
		

* **SQL & NoSQL**  
	SQL(Structured Query Language)：擅长高效且紧凑的形式存储结构化数据，需花费大量精力保证数据的一致性。  
	NoSQL: document-oriented and key-value databases (文档数据库和键值对数据库)  
	对于中小型程序来说，两者都是很好的选择，且性能相当。   

* **[Flask-SQLAlchemy](http://flask-sqlalchemy.pocoo.org/2.1/), the Flask extension wrapper for [SQLAlchemy](http://www.sqlalchemy.org/).**  
Flask-SQLAlchemy is a Flask extension that simplifies the use of SQLAlchemy inside Flask applications. SQLAlchemy is a powerful relational database framework that sup‐ ports several database backends. It offers a high-level ORM and low level access to the database’s native SQL functionality.  
		
		(ven)xing$ pip install flask-sqlalchemy

* Flask-Mail扩展，虽然Python标准库中的smtplib也能在Flask程序中发送电子邮件，但包装了smtplib的Flask-Mail扩展能更好地和Flask集成。  
		
		(ven)xing$ sudo pip install flask-mail
		
	Flask-Mial连接到简单邮件传输协议(Simple Mail Transfer Protocal, SMTP)服务器，并把邮件交给这个服务器发送。如果不进行配置，Flask-Mail会连接localhost上的端口25，无需验证即可发送电子邮件。
	
	
* Requirements File,用于记录所有依赖包及其版本号，如果要在另一台电脑上重新生成虚拟环境，可利用此文件复现。
		
		# generate a Requirements file named 'requirements.txt'
		(ven)flasky xing$ pip freeze > requirements.txt
		
		# use Requirements file create a new virtual environment
		(ven)flasky xing$ pip install -r requirement.txt

* Flask-Login是一个非常有用的小型扩展，专门用来管理用户认证系统中的认证状态，且不依赖特定的认证机制。

		(venv)falsky xing$ pip install flask-login
		
		
		




	
