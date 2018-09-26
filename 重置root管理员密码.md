1. 确定是否为RHEL7系统
> [root@u ~]# cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.0 (Maipo)
2. 重启，出现引导界面时，按e键进入内核编辑界面。
- 在 linux16 参数这行的最后面追加“rd.break”参数，然后按下 Ctrl + X 组合键来运行修
改过的内核程序。
- 30s后，进入紧急救援模式
- 输入以下命令
```
mount -o remount,rw /sysroot

chroot /sysroot

passwd

touch /.autorelabel

exit

reboot
```
