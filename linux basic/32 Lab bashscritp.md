## **Lab bashshel**

**Yêu cầu:** Cho danh sách các package : wget, curl, mtr , httpd. Viết bash script liệt kê các package nằm trong danh sách đã sẵn trên hệ

thống , sau đó cài đặt các package chưa được cài đặt 


**Thực hành**

Đầu tiên tạo các file chứa những package cần kiểm tra. `echo "wget curl mtr httpd" > package.txt`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/bash/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/bash/1.png)

Tạo file script installer.sh 

```
vi installer.sh 
```

Sau đó edit bằng nội dung sau:

```
for i in `cat /root/package.txt`;
do
        if [ `rpm -qa $i` ];then
                echo "$i Da duoc cai dat!"
        else
                echo "$i Chua duoc cai dat"
                echo $i >> /root/install.txt
        fi
done

if [ -e /root/install.txt ];then
        for i in `cat /root/install.txt`;
        do
                echo "dang cai cho ty de"
                yum install $i -y > /root/abc
                if [ `rpm -qa $i` ]; then
                        echo $i >> /root/installed.txt
                else
                        echo $i >> /root/notinstall.txt
                fi
        done

        rm -rf /root/install.txt

        for i in `cat /root/installed.txt`;
        do
                echo "$i Da duoc cai dat them"
        done

        if [ -e /root/notinstall.txt ]; then
                for i in `cat /root/notinstall.txt`;
                do
                        echo "Loi cai dat $i"
                done
        fi

fi

rm -rf /root/installed.txt

```

Thêm quyền và thực thi file `chmod +x ./installer.sh ./installer.sh`

Sau đó chạy lệnh `./installer.sh`

```
./installer.sh
```
Sau khi cài đặt xong kết quả trả ra 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/bash/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/bash/2.png)







