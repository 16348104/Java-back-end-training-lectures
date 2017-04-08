# Install

> [http://dblab.xmu.edu.cn/blog/](http://dblab.xmu.edu.cn/blog/)

### Mac

1. install homebrew

	```
	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	
	```
	
	```
	# 查看brew的帮助
	brew -help
	# 安装软件
	brew install hadoop
	# 卸载软件
	brew uninstall hadoop
	# 搜索软件
	brew search hadoop
	# 查看已经安装的软件
	brew list
	# 更新软件
	brew update
	# 更新某具体软件
	brew upgrade hadoop
	```
	
2. install ssh

	```
	ssh-keygen -t rsa -P ""
	cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
	```	
	
	```
	# 系统偏好设置 - 共享 - 远程登录
	ssh localhost
	```
	
3. install Hadoop

	```
	brew update
	brew install hadoop
	```	
	
	```
    Error: The `brew link` step did not complete successfully
    The formula built, but is not symlinked into /usr/local
    Could not symlink sbin/distribute-exclude.sh
    /usr/local/sbin is not writable.
    ```
    
    [Homebrew: Could not symlink, /usr/local/bin is not writable
](http://stackoverflow.com/questions/26647412/homebrew-could-not-symlink-usr-local-bin-is-not-writable)

	```
	sudo chown -R `whoami`:admin /usr/local/sbin/
	
	brew link hadoop
	```
4. Test Hadoop	

    - 单机模式
        
        ```
        cd /usr/local/Cellar/hadoop/2.7.3/
        mkdir input 
        ~~~mkdir output~~~
        
        cd input
        echo 'hello world' > file1.txt
        echo 'hello hadoop' > file2.txt
        
        hadoop jar ../libexec/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount ../input ../output
        
        more output/part-r-00000
        ```
        
        ```
        hadoop 1
        hello 2
        world 1
        ```
    
    - 伪分布模式
    
        
    


	

	