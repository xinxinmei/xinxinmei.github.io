## deepin 空间不够
### 将home目录挂载到独立分区
* 	准备分区   
	利用磁盘工具将分区格式化为ext4 格式
*	开始挂载
	>	umount /dev/sdb3   
		mkdir /mnt/home  
		mounnt /dev/sdb3 /mnt/home  
		cp -a -p /home/* /mnt/home
		mv home home.old
		blkid
		vim /etc/fstab
		```
			UUID=......		/home	 ext4	defaults	 0	 1
		```
	
*	收尾
	>	reboot  
		df

******
***注意cp的时候权限属性需要同时copy***


 	
	
