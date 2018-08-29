# 命令提示符


> [root@localhost ~]# 

**root**：当前登录用户

**localhost**：主机名

**~**：当前所在的目录，此处为“家”目录

**#**：root超级用户的提示符，如果是普通用户，则为 $ 

# 命令格式

>命令 [选项] [参数]

中括号 [] 表示可选 # 查询目录中的内容：ls



>ls [选项] [文件或目录] 

选项：
-a : 显示所有文件，包括隐藏文件
-l : 显示详细信息
-d : 查看目录属性
-h : 人性化显示文件大小
-i : 显示inode 

根据以上选项，敲入命令，显示结果分别如下： [root@localhost ~]# ls
anaconda-ks.cfg test
[root@localhost ~]# ls -a
. .. anaconda-ks.cfg .bash_history .bash_logout .bash_profile .bashrc .cache .config .cshrc .tcshrc test[root@localhost ~]# ls -l
总用量 4
-rw-------. 1 root root 2752 11月10日 02:51 anaconda-ks.cfg
drwxr-xr-x. 2 root root 6 11月12日 19:26 test
[root@localhost ~]# ls -l anaconda-ks.cfg -rw-------. 1 root root 2752 11月10日 02:51 anaconda-ks.cfg
[root@localhost ~]# ls -ld test/
drwxr-xr-x. 2 root root 6 11月12日 19:26 test/
[root@localhost ~]# ls -lh
总用量 4.0K
-rw-------. 1 root root 2.7K 11月10日 02:51 anaconda-ks.cfg
drwxr-xr-x. 2 root root 6 11月12日 19:26 test
[root@localhost ~]# ls -i
71259104 anaconda-ks.cfg 36099565 test
请注意观察 ls -l 与 ls -lh 命令的结果的区别 这里需要解释一下： -rw-------. 1 root root 2.7K 11月10日 02:51 anaconda-ks.cfg
drwxr-xr-x. 2 root root 6 11月12日 19:26 test
首先第一个符号 “-”（引号内的-），表示文件类型（常用的有三种，即-表示文件，d表示目录，l表示软链接文件），此外还有不常用的，为块设备文件，字符设备文件、套接字文件、管理文件。 在上述中，我们可以看到 anaconda-ks.cfg 是一个文件，而 test 是一个目录（可理解为windows的文件夹的概念）。 其次，除去第一个符号，我们来看rw-------，一共有九个字符，需分为三组，分别为rw-,---,---,每个组按照顺序分别表示u所有者，g所属组,o其他人的权限。在上述中，分别对应为 root，root。即第一个root表示所有者权限为root权限，第二个root表示所属组的权限也是root权限，对于其他人，则无所谓的权限可言。 其中，r表示可读，w表示可写，x表示执行的权限。 为了更加明白，对于 anaconda-ks.cfg 这个文件，这里列一个表格： 前三个字符	中间三个字符	后三个字符
rw-	—-	—-
所有者u的权限	所属组g的权限	o其他人的权限
可读可写	无权限	无权限
那么，对于 test 这个文件 rwxr-xr-x，请读者自行判断它的权限。 在九个字符之后的点 “.”，表示ACL权限，之后的数字 1 表示引用计数，比如一个文件有一个软链接（类似windows快捷方式），那么它的引用计数就是2。 root 后面的2.7k表示文件的大小，再后面表示日期，最后是文件的名称。 目录处理命令
创建目录：mkdir
mkdir -p [目录名] -p : 递归创建 [root@localhost ~]# ls
anaconda-ks.cfg test
[root@localhost ~]# mkdir otherFolder
[root@localhost ~]# ls
anaconda-ks.cfg otherFolder test
[root@localhost ~]# mkdir folder_2/test_2
mkdir: 无法创建目录"folder_2/test_2": 没有那个文件或目录
[root@localhost ~]# mkdir -p folder_2/test_2
[root@localhost ~]# ls
anaconda-ks.cfg folder_2 otherFolder test
[root@localhost ~]# ls folder_2/test_2
如上所示，mkdir 不加选项 -p 时，可以创建一个空目录，但是无法递归创建一个包含子目录的目录。加上 -p 即可递归创建。 切换所在目录：cd
cd [目录] 操作： cd ~ : 进入当前用户的家目录 cd-： 进入上次目录 cd.. : 进入上一级目录 cd : 回到家目录 [root@localhost ~]# ls
anaconda-ks.cfg folder_2 otherFolder test
[root@localhost ~]# cd /folder_2/test_2
[root@localhost test_2]# cd
[root@localhost ~]# cd -
/root/folder_2/test_2
[root@localhost test_2]# cd ../../otherFolder
[root@localhost otherFolder]# cd ..
[root@localhost ~]#
注意理清概念：相对路径和绝对路径 绝对路径：从根目录一级级找下去，需要写全路径 [root@localhost ~]# cd folder_2/test_2
[root@localhost test_2]#
相对路径：参照当前所在目录进行查找 [root@localhost test_2]# cd ../../otherFolder
[root@localhost otherFolder]#
查询所在目录位置：pwd
pwd 可以说是最简单的命令了，查询所在目录的位置 [root@localhost ~]# pwd
/root
[root@localhost ~]# ls
anaconda-ks.cfg folder_2 otherFolder test
[root@localhost ~]# cd folder_2/
[root@localhost folder_2]# ls
test_2
[root@localhost folder_2]# cd test_2/
[root@localhost test_2]# pwd/root/folder_2/test_2
删除空目录：rmdir
rmdir [目录名] 只能删除空目录，这个命令用得比较少。 [root@localhost ~]# ls
anaconda-ks.cfg folder_2 otherFolder test
[root@localhost ~]# rmdir otherFolder
[root@localhost ~]# ls
anaconda-ks.cfg folder_2 test
[root@localhost ~]# rmdir folder_2
rmdir: 删除 "folder_2" 失败: 目录非空
[root@localhost ~]#
删除文件或目录：rm
rm -rf [文件或目录] r 表示可以同时删除文件和目录，f表示强制删除 如果不添加任何选项，那么只可以删除文件，删除时提示是否确认删除 如果只添加选项 -r，那么可以删除文件也可以删除目录，删除时提示是否确认删除 如果添加了选项 -rf，那么将不做任何提示删除文件或目录 [root@localhost ~]# ls
abc.txt anaconda-ks.cfg folder_2 test
[root@localhost ~]# rm abc.txt
rm：是否删除普通空文件 "abc.txt"？y
[root@localhost ~]# rm test
rm: 无法删除"test": 是一个目录
[root@localhost ~]# rm -r test
rm：是否删除目录 "test"？y
[root@localhost ~]# ls
anaconda-ks.cfg folder_2
[root@localhost ~]# rm -rf folder_2
[root@localhost ~]# ls
anaconda-ks.cfg
[root@localhost ~]#
复制命令：cp
cp [选项] [原文件或目录] [目标目录] 选项：
-r : 复制目录
-p : 同时复制文件属性
-d : 若源文件是链接文件，则复制链接属性
-a : 包含以上所有选项，相当于 -rpd 在[目标目录]后面加上文件名，就是改名复制。 [root@localhost ~]# ls
anaconda-ks.cfg bbc.txt folder_a folder_b
[root@localhost ~]# cp bbc.txt folder_a[root@localhost ~]# ls folder_a/
bbc.txt[root@localhost ~]# cp folder_a folder_b
cp: 略过目录"folder_a"
[root@localhost ~]# cp -r folder_a folder_b
[root@localhost ~]# ls folder_b
folder_a test_1
[root@localhost ~]# ll
总用量 4
-rw-------. 1 root root 2752 11月10日 02:51 anaconda-ks.cfg
-rw-r--r--. 1 root root 0 11月13日 17:21 bbc.txt
drwxr-xr-x. 2 root root 20 11月13日 17:38 folder_a
drwxr-xr-x. 4 root root 34 11月13日 17:39 folder_b
[root@localhost ~]# ll folder_a
总用量 0
-rw-r--r--. 1 root root 0 11月13日 17:38 bbc.txt
[root@localhost ~]# cp -a bbc.txt folder_b
[root@localhost ~]# ll folder_b
总用量 0
-rw-r--r--. 1 root root 0 11月13日 17:21 bbc.txt
drwxr-xr-x. 2 root root 20 11月13日 17:39 folder_a
drwxr-xr-x. 2 root root 6 11月13日 17:38 test_1
[root@localhost ~]#
这里需要解释一下的是，在原文件 bbc.txt 中，其修改时间为 17:21，在普通复制下，它的时间这个属性是不会被复制，我们可以看到复制后的bbc.txt的时间为17:38，如果需要连同属性一起复制，那么就加上 -pd 或者 直接 -a，如上所示，我们把bbc.txt复制到folder_b，这时我们查看属性的时候，时间属性和原属性是一致的。 在上述命令中，ll 是 ls -l 的简写。 剪切或改名命令：mv
mv [原文件或目录] [目标目录] 如果原文件或者目录 与 目标目录在同一个目录下，那么就是重命名 如果不在同一个目录下，那么就是剪切 通过以下实践理解： [root@localhost ~]# ls
anaconda-ks.cfg bbc.txt
[root@localhost ~]# mv bbc.txt abc.txt
[root@localhost ~]# ls
abc.txt anaconda-ks.cfg
[root@localhost ~]# mkdir test
[root@localhost ~]# ls
abc.txt anaconda-ks.cfg test
[root@localhost ~]# mv abc.txt test/
[root@localhost ~]# ls
anaconda-ks.cfg test
[root@localhost ~]# ls test/
abc.txt
[root@localhost ~]#
链接命令：ln
ln -s [原文件] [目标文件] 生成链接文件
-s : 创建软连接 硬链接的特征： 拥有相同 i 节点和存储block块，可以看做是同一个文件 可通过i节点识别，i节点是相同的 不能跨分区 不能针对目录使用 通过上述命令，可以理解为为某个内容添加一个标签，通过打开这个标签就可以进入这个内容，硬连接，即再生成一个标签，同样可以通过这个标签进入这个内容。 如果内容被修改，那么不管从硬链接的哪个文件进入，都是被修改的。 软链接的特征： 类似windows的快捷方式 软链接拥有自己的i节点和block块，但是数据块只保存原文件的文件名和I节点号，并没有实际的文件数据 lrwxrwxrwx l为软链接（软链接的权限都为rwxrwxrwx，这只是软链接本身的权限） 修改任意文件，另一个都改变 删除原文件，软链接不能用（和windows的快捷方式一样） 硬链接： [root@localhost ~]# ls
anaconda-ks.cfg
[root@localhost ~]# mkdir folder
[root@localhost ~]# ls
anaconda-ks.cfg folder
[root@localhost ~]# touch bbb.txt
[root@localhost ~]# ls
anaconda-ks.cfg bbb.txt folder
[root@localhost ~]# ln bbb.txt folder/ccc.txt
[root@localhost ~]# ll folder/ 总用量 0
-rw-r--r--. 2 root root 0 11月13日 18:08 ccc.txt
[root@localhost ~]# ll bbb.txt -rw-r--r--. 2 root root 0 11月13日 18:08 bbb.txt
软链接： [root@localhost ~]# mkdir folder_b
[root@localhost ~]# ln -s bbb.txt folder_b/eee.txt
[root@localhost ~]# ll 总用量 4
-rw-------. 1 root root 2752 11月10日 02:51 anaconda-ks.cfg
-rw-r--r--. 2 root root 0 11月13日 18:10 bbb.txt
drwxr-xr-x. 2 root root 20 11月13日 18:09 folder
drwxr-xr-x. 2 root root 20 11月13日 18:11 folder_b
[root@localhost ~]# ll folder_b
总用量 0
lrwxrwxrwx. 1 root root 7 11月13日 18:11 eee.txt -> bbb.txt
[root@localhost ~]# rm -rf bbb.txt [root@localhost ~]# ll folder_b
总用量 0
lrwxrwxrwx. 1 root root 7 11月13日 18:11 eee.txt -> bbb.txt
删除了原文件，软链接的箭头目标为红色一闪一闪，表示找不到目标文件。 常用目录作用
[root@localhost ~]# ls /
bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys temp tmp usr var
/ 根目录 /bin 命令保存目录（普通用户权限） /sbin 命令保存目录（root权限） /boot 启动目录，包含启动相关文件，和开机有关 /dev 设备文件保存目录 /etc 配置文件保存目录 /home 普通用户家目录 /lib 系统库保存目录 /mnt 系统挂载目录 /media 挂载目录（常用于光盘挂载） /root 超级用户家目录 /tmp 临时目录 /proc 直接写入内存的 /sys 直接写入内存的 /usr 系统软件资源目录 /var 系统相关文档内容

