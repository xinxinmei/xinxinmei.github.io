新增用户：useradd tom		//密码为空的话不允许登陆
修改密码：passwd tom	
查看密码：cat /etc/passwd | grep tom
修改家目录：usermod -d /home/tom_new -m tom
查看密码相关的信息：cat /etc/shadow | grep tom
冻结用户：usermod -L tom
解冻用户：usermod -U tom
删除用户：userdel tom
增加用户组： groupadd team
查看用户组：cat /etc/group
删除用户组：groupdel team
查看用户： user、who、w
调查用户：finger
切换用户：su或sudo
创建文件： touch
删除文件：rm filename
移动或重命名文件:mv 目标文件 目标文件夹			mv filename new_filename
查看文件：cat filename		//-n 显示行号
查看文件头：head filename	、head -n 20 filename//默认查看前10行
查看文件为：tail -f /var/log/messages		//类似head
文件格式转换：dos2unix filename
删除目录： rmdir dirname、rm -r dirname
文件和目录复制：cp a.txt b.txt	\ cp a.txt /home	\cp -r dir  dir
改变文件权限： chmod u+w filename			//u、g、o、+、-、=、rwx
改变文件的拥有者：chown tom a.txt		//文件夹-R递归
改变文件的拥有组：chgrp team a.txt		//文件夹-R递归
查看文件属性：file filename
一般查找：find 开始路径path -name filename
数据库查找：updatedb；locate filename
查找执行文件：which passwd	、 whereis passwd
文件压缩打包：gzip a.txt	,gunzip a.txt.gz	//压缩和解压单个文件
			tar -zcvf  boot.tgz /boot  		//将boot目录下的文件打包为boot.tgz
			tar -zxvf  boot.tgz			//将boot.tgz解压成boot目录
			tar -zxvf  boot.tgz -C /tmp		//将boot.tgz解压到tmp目录
			z:代表使用的是gzip或者是gunzip
			c:代表创建压缩文件
			x:代表解压缩
			v:显示当前文件
			f:指使用文件名
			-C：解压到指定目录
使用bzip2解压缩：bzip2 a.txt
				bzip2 -d a.txt.bz2
				
查看设备：fdisk -l
磁盘挂载：mount /dev/sdb1 dir
接触挂载：umount /dev/sdb1	或者挂载点
管道：ls -l  | more			//将命令作为下一条命令的输入
grep搜索文本：grep [-icnv] '需要匹配的字符' filename
				i:不区分大小写
				c:统计包含匹配的行数
				n:输出行号
				v:反向匹配
sort排序：sort [-ntkr] filename
			n:采取数字排序
			t:指定分割符
			k:指定第几列
			r:反向排序
uniq删除重复内容： uniq [-ic]		cat a.txt | uniq
					i:忽略大小写
					c:计算重复行数
cut截取文本： cut  -f 指定列 -d ‘分隔符’
tr做文本转换：tr '[a-z]' '[A-Z]'		tr -d ':'
paste做文本合并：paste a.txt b.txt			paste -d: a.txt b.txt
split分割大文件：split -b 64m bigfile smallfile		split -l 500 bigfile smallfile
ifconfig检查和配置网卡: ifconfig eth0 ip地址 netmask 掩码
						ifconfig eth0 ip地址/掩码数字（24）
						ifconfig eth0 down/up
						ifdown eth0
						ifup eth0
						service network restart
						cd /etc/sysconfig/network-scripts
路由和网关设置：	 route add/del default gw 192.168.159.2
					route -n //查看路由表
dns客户端配置： /etc/hosts


ps查看进程：ps
			A：列出所有的进程
			aux：显示所有包含其他使用这的进程
			
kill进程：kill [信号代码] 进程id
查询进程打开的文件：lsof [options] filename
				-c string :显示包含string的进程
				
				
gcc编译程序：gcc a.c -o a
将目录追加到path变量中： export PATH=$PATH:/root

makefile文件:make   make install 
configure命令生成makefile： ./configure --参数
							./configure --prefix=/usr/local/apache/ --enable-modules=most
							




































