|	System V init命令（RHEL 6系统）	|	systemctl命令（RHEL 7系统）	|	作用	|	
|	---	|	---	|	---	|	
|	service foo start	|	systemctl start foo.service	|	启动服务	|	
|	service  foo restart	|	systemctl restart foo.service	|	重启服务	|	
|	service foo stop	|	systemctl stop foo.service	|	停止服务	|	
|	service foo reload	|	systemctl reload foo.service	|	重新加载配置文件（不终止服务）	|	
|	service foo status	|	systemctl status foo.service	|	查看服务状态	|	
