1. 从mysql官网下载repo并安装

	打开http://dev.mysql.com/downloads/repo/  
	从这里下载对应的版本。  
	CentOS 6 对应的是 Redhat6的mysql-community-release-el6-5.noarch.rpm  

		sudo yum localinstall mysql-community-release-el6-5.noarch.rpm

2. 使用yum安装mysql

		sudo yum install mysql-server

3. 开始和停止mysql服务

		开始mysql服务
		sudo service mysqld start

		检查mysql状态
		sudo service mysqld status

		停止mysql服务
		sudo service mysqld stop

4. 加强mysql安全

5. 安装mysql额外的组件
	