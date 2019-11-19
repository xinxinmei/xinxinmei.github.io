## docker 及建立本地网站
* docker search centos:6
* docker pull centos:6
* docker images
* docker ps -a
* docker run -i -t centos:6 /bin/bash
* docker cp file /home
* vi /root/run.sh
>	source ~/.bashrc  
	sh /opt/tomcat/bin/catalina.sh run

* chmod u+x /root/run.sh
* docker ps -a
* docker commit [id] javaweb:0.1
* docker run -d -p 58080:8080 --name java-web javaweb:0.1 /root/run.sh
* 127.0.0.1:58080
* docker run -tdi -v /date:/data --name data-v centos
* docker run -ti --volumes-from data-v --name  web centos
