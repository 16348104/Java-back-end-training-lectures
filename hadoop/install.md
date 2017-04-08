# Install

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
	
4. test Hadoop	


	

	