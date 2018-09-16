|	System V init命令（RHEL 6系统）	|	systemctl命令（RHEL 7系统）	|	作用	|
|	---	|	---	|	---	|
|	chkconfig foo on	|	systemctl enable foo.service	|	开机自动启动	|
|	chkconfig foo off	|	systemctl disable foo.service	|	开机不自动启动	|
|	chkconfig foo	|	systemctl is-enabled foo.service	|	查看特定服务是否为开机自动启动	|
|	chkconfig --list	|	systemctl list-unit-files --type=service	|	查看各个级别下服务的启动与禁用情况	|
