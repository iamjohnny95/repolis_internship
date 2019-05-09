cài đặt Mysql bằng bash script

```
#! bin bash

echo "Qua trinh cai dat bat dau"

if [ -e mysql*.rpm ];
	then

		echo "Co file rpm mysql"
		rm mysql*.rpm
		echo "Xoa file hien tai"
		echo "Tai lai file"
		echo " Doi mot lat"
		wget https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm

	else
		echo "Tai file rpm mysql ve may"
		echo "Cho doi trong it phut"
		wget https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
		echo "Tai ve thanh cong RPM"

	fi


	rpm -ivh mysql*.rpm

	yum install mysql-community-{server,client,common,libs}-* --exclude='*minimal*' -y

	systemctl enable mysql

	systemctl start mysql 

	if [ "`systemctl | grep -o mysqld.service`" == "mysqld.service" ]  

		then

			echo "Service MYSQL da chay"

		fi

	echo "Da cai dat MYSQL-SERVER"

```
