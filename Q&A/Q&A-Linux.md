##Linux Q&A
Tags: Ethan_penx

---

[TOC]

#### [display content of all files with their filenames with cat?](http://stackoverflow.com/questions/12554698/display-content-of-all-files-with-their-filenames-with-cat)

```shell
xing$ tail -n +1 *.txt
```

or 

```shell
xing$ tail *.txt
```



####1. [What is the difference between vi and vim?](http://unix.stackexchange.com/questions/30465/what-is-the-difference-between-vi-and-vim)

As far as I know vi is more commonly found on out-of-the-box unix systems while vim often has to be installed. Also vim stands for vi improved, but improved how?

What are the main differences?  
**A:** Vim tries to resemble the syntax and semantic of Vi command as much as possible. But being an "improved version", Vim adds new commands and features. It also changes the semantic of some Vi commands to better match the current expectations of its programmers.  
I really wish I'd known that you can use Ctrl-C instead of ESC to switch out of insert mode. That's been a real productivity boost for me.

####2. [git checkout](https://git-scm.com/docs/git-checkout) command

git-checkout - Switch branches or restore working tree files  

#####[git-checkout(1) Manual Page](https://www.kernel.org/pub/software/scm/git/docs/git-checkout.html)

#####[--> Problem & Solution](http://stackoverflow.com/questions/17989165/git-checkout-master-error-the-following-untracked-working-tree-files-would-be-o)  
Problem  
​	
	xing$ git checkout master   
	error: The following untracked working tree files would be overwritten by checkout:
	    source/a/foo.c
	        ...... (too many lines)
	Please move or remove them before you can switch branches.
	Aborting

Solution

	xing$ git checkout -f master

​	



####3. [HowTo: Use cat Command In Linux / UNIX](http://www.cyberciti.biz/faq/howto-use-cat-command-in-unix-linux-shell-script/)
It can be used for the following purposes under UNIX or Linux:

* Display text files on screen.
* Copy text files.
* Combine text files.
* Create new text files.  

example: copy file

	$ cat oldfile.txt > newfile.txt

####4. [Linux Command Line History](http://www.thegeekstuff.com/2008/08/15-examples-to-master-linux-command-line-history/?utm_medium=twitter&utm_source=twitterfeed)

Execute a specific command from history (use !+ num)

	# history | more
	1  service network restart
	2  exit
	3  id
	4  cat /etc/redhat-release
	
	# !4
	cat /etc/redhat-release
	Fedora release 9 (Sulphur)

####5. [Exit the VIM editor](http://stackoverflow.com/questions/11828270/how-to-exit-the-vim-editor)

Hit the **Esc** key; that goes into command mode. Then you can type

* **:q** to quit (short for :quit)
* **:q!** to quit without saving (short for :quit!)
* **:wq** to write and quit (think write and quit)
* **:wq!** to write and quit even if file has only read permission (if file * does not have write permission: force write)
* **:x** to write and quit (shorter than :wq)
* **:qa** to quit all (short for :quitall)

When you press :, a : will appear at the bottom of the screen.

Or you can press Esc ZZ (Esc Shift+Z Shift+Z) to write/save if the file was changed, then quit.

Or if you don't want to save changes you can use ZQ instead.

Vim has extensive help, so type Esc:helpReturn and you will have all your answers and even a neat tutorial.

#### 6. [How to move multiple files at once to a specific destination directory?](How to move multiple files at once to a specific destination directory?)

If you want to move ABC-IDENTIFIER-XYZ.ext or IDENTIFIER-XYZ.xml, you can use:

	mv *IDENTIFIER* ~/YourPath/

The symbol* is a wildcard for zero or more characters, this means zero or more characters, followed by IDENTIFIER, followed by zero or more characters.

This will move all the files that contain the IDENTIFIER you specified. 


#### 7. [What is the difference between yum, apt-get, rpm, ./configure && make install?](http://superuser.com/questions/125933/what-is-the-difference-between-yum-apt-get-rpm-configure-make-install)

These tools all install software into your system, but are working on different levels.

**./configure && make install**

Running ./configure && make install builds and installs the libraries or executables directly from the source code.

The make install step basically just copies the final files into your system. Many sources come with a special make uninstall rule to remove them again, but this is not guaranteed and of course only works as long as you have the configured sources around. Also, this does not take care of required dependencies.

Often there is only the source code available for a certain package, so this is the only way to go. Also, ./configure usually accepts lots of options allowing you to tailor your package.

Not being able to find out what software installed which file, and the lack of a reliable way to remove them from the system are major shortcomings of this approach.

**RPM (Redhat Package Manager)**

rpm installs already configured and compiled software in your system and it also comes with a uninstall to get rid of it again. The packages have to be created by somebody. This person already decided on what features to include and how to best integrate the package into your system layout. It also comes with a list of dependencies.

Since rpms are used for many distributions there, you will often want to make sure that this rpm was written for your distribution so that install paths, dependencies and other housekeeping things integrate well.

On Debian systems, the equivalent package format is .deb and the installation and database is handled by the dpkg tool.

**Yum**

yum is an additional wrapper around rpm. It keeps its own database of rpm files available for your distribution, generally in online repositories. For the stable versions of most distributions all packages inside that database will play well with each other. This database can be searched (e.g. with yum search some_name).

It will also automatically resolve dependencies for you. Packages (and with some extra help their dependencies) can be easily uninstalled as well.

On Debian systems, the equivalent repository and dependency-resolution tools are provided by Apt (apt-get and aptitude).
So to sum it up: if you just want some software try yum first. If it is not available there, you can try to find an existing rpm package. If there is none or you have some special requirements, build from source.

#### [How can I delete a word backward at the command line (bash and zsh)?](http://unix.stackexchange.com/questions/94331/how-can-i-delete-a-word-backward-at-the-command-line-bash-and-zsh)

ctrlw is the standard "kill word" (aka `werase`). ctrlu kills the whole line (`kill`).

​	



####Other Command
* rename a file  & rename a directly

   xing$ mv t.txt test.txt
   	xing$ mv folder Folder

* activate & deactivate virtual environment
  ​	
  	flask xing$ source venv/bin/activate
  	(venv)flask xing$
  	
  	(venv)flask xing$ deactivate
  	flask xing$ 

* DNS Lookup Command

   Find Out the Domain IP

   	MBP-Ethan:~ xing$ host -t a www.baidu.com
   	www.baidu.com is an alias for www.a.shifen.com.
   	www.a.shifen.com has address 14.215.177.38
   	www.a.shifen.com has address 14.215.177.37
   	
   	#Find Out the Domain name server
   	MBP-Ethan:~ xing$ host -t ns www.baidu.com
   	www.baidu.com is an alias for www.a.shifen.com.

* Goes back to previous directory

   ```
   ~$ cd -
   ```

   ​		


​	


