---

---

## Flask Tutorial Web Development with Python  - Basic site setup


> If there is something you don't know, just google it.


### SSH Tiemout Setting

The default SSH timeout setting is in place for security purposes, but it can also be quite annoying.

[How to disable SSH timeout](https://docs.oseems.com/general/application/ssh/disable-timeout)  

So we want to extend the SSH timeout. To do this:  

	~$ cd /etc/ssh
	ssh$ sudo nano sshd_config
	#control + w, searching for "keepalive"
	
Now we want to add in the following below the TCPKeepAlive yes:

ClientAliveInterval 30
ClientAliveCountMax 99999

**Well Done.**


### Enable RPMForge Repository in CentOS6.x


**CentOS:** Community ENTerprise Operating System

[What is the difference between yum, apt-get, rpm, ./configure && make install?](http://superuser.com/questions/125933/what-is-the-difference-between-yum-apt-get-rpm-configure-make-install)

if you just want some software try **yum** first. If it is not available there, you can try to find an existing rpm package. If there is none or you have some special requirements, build from source.

RPMforge repositetory not a part of CentOS or RHEL, but it is designed to work with these operating sysyems.

[How to Enable RPMForge Repository in RHEL/CentOS 7.x/6.x/5.x](http://www.tecmint.com/enable-rpmforge-repository/)

1. Use "uname -a" command verify a system.


		[root@iZ28vqecfh6Z ~]# uname -a
		Linux iZ28vqecfh6Z 2.6.32-431.23.3.el6.x86_64 #1 SMP Thu Jul 31 17:20:51 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

2. Installing RPMForge Repository in CentOS6.5

		## CentOS 6 64 Bit OS 
		$ wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
		$ rpm -Uvh rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm

3. Importing RPMForge Repository Key  

		$ wget http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt
		$ rpm --import RPM-GPG-KEY.dag.txt

**Well Done.**