## **Tìm hiểu về bash script**

**Tìm hiểu các cú pháp thường dùng trong bash script**

Mã Bash shell là một danh sách những lệnh mà chúng sẽ được thực thi một cách tuần tự. Thông thường nội dung một file bash shell sẽ có đuôi .sh và bắt đầu bằng 

```
#!/bin/bash
```

Đoạn mã đó chỉ ra rằng các mã lệnh nên được chạy trên bash shell, bất kể là người dùng chọn đã chọn loại shell nào. Bởi vì có nhiều loại 

shell nên cú pháp của chúng cũng sẽ đa dạng và có thể hoặc ít hoặc nhiều. 

Ví dụ là dấu #, trong bash shell nó sẽ được hiểu là tất cả những gì theo sau # sẽ là comment và không được thực thi. Nhưng trong shell khác 

thì nó không có nghĩa là như vậy. 

## **Biến**

## **Cách khai báo**

Bất kỳ ngôn ngữ nào cũng phải có biến để sử dụng và bash shell cũng không phải là một ngoại lệ. Cách định nghĩa biến theo format:      

tên_biến ="" 

```
var="xin chao"
```

Và gọi đến biến bằng cách thêm dấu $ trước tên biến. 

```
$var
```

Cơ bản là bash shell xem những cái phân cách nhau bởi khoảng trắng là những lệnh và thực thi chúng bạn cần chú ý:

**CHÚ Ý 1** Với toán tử gán =nói riêng và các toán tử khác nói chung, bạn không được để khoảng trắng trước và sau nó.

**CHÚ Ý 2:** Bạn không cần thiết lúc nào cũng cần "" để bao bọc giá trị của biến, bạn có thể bỏ chúng nếu giá trị không chứa khoảng trắng. 

## **Nháy đơn và nháy đôi với biến**

Bạn hãy xem đoạn code sau và đoán xem bash sẽ in ra màn hình những gì :

```
#!/bin/bash
var="xin chao"
echo '$var'
echo "$var"
```

Kết qủa là đây:

```
$var
xin chao
```

Bạn đã thấy nếu cần expand biến (tức là tham chiến đến giá trị của biến) thì dùng nháy đôi, còn nháy đơn sẽ không làm điều đó mà giữ nguyên 

biến. Nhưng nếu bạn muốn vừa giữ tên biến và cũng muốn lấy gía trị của nó trong dấu nháy đôi thì sẽ dùng \ :

```
echo "\$var=$var"
```

Kết quả

```
$var=xin chao
```

**Chú ý**: Hãy sử dụng nháy đôi để bảo vệ biến của bạn, như "$var". Bởi nếu giá trị của biến là chuỗi rỗng hoặc có chứa khoảng trắng thì có 

thể sẽ có lỗi trong mã của bạn.

## **Ngoặc nhọn để bảo vệ biến**

Bạn hãy thử chạy bash với dòng code như sau xem như thé nào

```
#!/bin/bash
X=brace
echo "$Xabc"
```

Bạn không thấy gì cả ? đương nhiên ! vì bash shell nhầm tưởng ý của bạn là biến Xabc và biến này thì bạn chưa định nghĩa nó. Nếu bạn muốn 

dùng như trên hãy dùng cặp ngoặc nhọn để bao quanh tên biến, khi đó shell sẽ hiểu bạn :

```
#!/bin/bash
X=brace
echo "${X}abc"
```

## **Lệnh rẽ nhánh if**

**GIỚI THIỆU**

Cũng như các ngôn ngữ lập trình, với một danh sách các lệnh thì không thể thiếu được câu lệnh rẽ nhánh cơ bản để kiểm tra xem điều kiện đúng

hay sai mà thực thi những việc mình cần.

Câu lệnh đơn giản nhất sẽ có cấu trúc như dưới:

```
if điều kiện
then
	1 hoặc nhiều câu lệnh ở đây
fi
```

Và đương nhiên chúng ta sẽ có else như bao ngôn ngữ khác

```
if điều kiện 
then
	1 hoặc nhiều câu lệnh ở đây
else 
	xử lý khác ở đây
fi
```
Nhưng với elseif thì shell viết hơi khác một chút là efif, nhưng bạn cũng có thể dùng bao nhiều elif tùy thích.

```
if điều kiện 1
then
	xử lý 1
elif điều kiện 2
then
	xử lý 2
fi
```

**Các toán tử**

Toán tử - nói đến rẽ nhánh thì đương nhiên những toán tử sau bắt buộc phải có. Trong bash shell có những toán tử cơ bản sau:


|**Toán tử**|**Ý nghĩa**|**Số lượng toán hạng**|
|||||
|-n|Chuỗi không empty, độ dài lớn hơn 0|1|
|-z|Chuỗi empty, độ dài bằng 0|1|
|-d|Tồn tại thự mục có tên là ...|1|
|-f|Tồn tại file có tên là...|1|
|-eq| 2 toán hạng là số integer và nó bằng nhau|2|
|-neq| ngược lại của -eq|2|
|=|2 toán hạng bằng nhau (chuỗi)|2|
|-lt|toán hạng đầu nhỏ hơn toán hạng thứ 2 (cả 2 là số integer)|2|
|-gt|toán hạng đầu lớn hơn toán hạng thứ 2 (cả 2 là số integer)|2|
|-le|toán hạng đầu nhỏ hơn hoặc bằng toán hạng thứ 2 (cả 2 là số integer)|2|
|-ge|toán hạng đầu lơn hơn hoặc bằng toán hạng thứ 2 (cả 2 là số integer)|2|


Bạn có thể xem ví dụ sau để hiểu cách dùng if cũng như các toán hạng 

```
#!/bin/bash
A=1
B=2
string1="Not empty"
if [ $A -lt $B ]	# $A có nhỏ hơn $B không ?
then
	echo "${A} nhỏ hơn ${B}"
fi

if [ -z "$string1" ]; then # kiểm tra $string1 có empty không?
	echo "\${string1} rỗng"
else
    echo "\${string1} không rỗng"
fi
```

**Vòng lặp**

**For**

Sau đây là cú pháp của vòng lặp for

 
Như bạn thấy thì vòng lặp for sẽ duyết qua tất cả các phần tử được phân cách nhau bởi dấu khoảng trắng, nên như chú ý ở trên với phần biến 

nếu bạn có khoảng trắng trong giá trị của biến thì hãy sử dụng cặp nháy ""

Trong bash shell thì ký tự * được hiểu là tất cả ký tự ví dụ *.bak thì bash sẽ hiểu là tất cả các file backup có đuôi .bak chẳng hạn. Nên 
ta sẽ có một ví dụ chắc sẽ hữu ích hơn như là tìm trong một thư mục chỉ định mà gặp file backup thì di chuyển đến thư mục /home/backup 
chẳng hạn.

```
#!/bin/bash
for A in *.bak
do
	mv $A /home/backup
done
```

**While**

Như bao ngôn ngữ khác thì while sẽ lặp đến khi điều kiện chỉ định còn là true

```
#!/bin/bash
# lặp từ 1 đến khi bằng 100 thì thôi, in ra từ 1 ~ 99
A=1
while [ $X -le 99 ]
do
	echo $X
	X=$((X+1))
done
```


**Mảng**

Mảng trong shell cũng là một kiểu dữ liệu mà trong nó chứa danh các giá trị theo index như các ngôn ngữ lập trình cơ bạn. Cơ bản bạn sẽ 

khởi tạo một mảng biến bằng cách :

```
#!/bin/bash
var[1]="test"
# truy cập mảng
echo ${var[1]}
# hoặc khai báo như dưới
var2=( [0]="mot" [1]="hai" [3]="bon" ) # vì phần tử thứ 3 của mảng không được khởi tạo nên nó sẽ là null
var3=( mot hai ba ) # phân cách các phần tử bằng dấu khoảng trắng

# để đếm số phần tử trong mảng bạn sẽ dùng kí tự # như sau
echo ${#var2[@]}
# hoặc
echo ${#var2[*]}
```

**Case** 

- Ví dụ: 

```
echo "Enter name of vehicle: "
	read vehicle

	case $vehicle in
		"car" )
			echo "$Rent vehicle is 100$";;
		"van" )
			echo "$Rent vehicle is 80$";;
		"bicycle")
			echo "$Rent vehicle is 50$";;
		"truck")
			echo "$Rent vehicle is 10$";;

	esac

```

**Cú pháp điều kiện**

**So sánh số**

|**Cú pháp**|**Ý nghĩa**|
|n1 -eq n2| Kiểm tra n1 =n2|
|n1 -ne n2| Kiểm tra n1 khác n2|
|n1 -lt n2| Kiểm tra n1 nhỏ hơn n2|
|n1 -le n2| kiểm tra n1 nhỏ hơn hoặc bằng|
|n1 -gt n2| kiểm tra n1 lớn hơn n2|
|n1 -ge n2| kiểm tra n1 lớn hơn hoặc bằng n2|

**So sánh chuỗi**

|**Cú pháp**|**Ý nghĩa**|
|s1 =s2|Kiểm tra s1 =s2|
|s1!= s2|Kiểm tra s1 khác s2|
|-z s1|Kiểm tra s1 có kích thước bằng 0|
|-n s1|Kiêm tra s1 có kích thước khác 0|
|s1|Kiểm tra s1 khác rỗng|

**Toán tử kết hợp**

|**Cú pháp**|**Ý nghĩa**|
|!|Phủ định(not)|
|-a|Và(and)|
|-o|Hoặc(or)|

**Kiểm tra file(Thư mục)**

|**Cú pháp**|**Ý nghĩa**|
|-f [file]|Kiểm tra xem file có phải là tệp hay không|
|-d [file]|Kiểm tra xem file có phải là thư mục hay không|
|-r [file]|Kiểm tra file có đọc (read) được hay không|
|-w [file]|Kiểm tra file có ghi (write) được hay không|
|-x [file]|Kiểm tra file có thực thi (execute) được hay không|
|-s [file]|Kiểm tra file có kích thước lớn hơn 0 hay không|
|-e [file]|Kiểm tra xem file có tồn tại hay không|


**Các ví dụ về shellscript:**

**Hướng dẫn chuyển đổi từ chữ hoa sang chữ thường**

4 Cách thường sử dụng nhất để chuyển đổi một đoạn text từ chũ hoa sang chữ thường và ngược lại trong bashshell

ví dụ: 

Mình có một chuỗi sau:

```
STRING="toi ten la son"
```
**1.Sử dụng chương trình 'tr'**

- Chữ hoa -> chữ thường 

```
# echo "$STRING" | tr -s '[:upper:]' '[:lower:]'
toi ten la son
```

- Chữ thường -> chữ hoa

```
# echo "$STRING" | tr -s '[:lower:]' '[:upper:]'
TOI TEN LA SON
```

**2.Sử dụng chương trinh 'awk'**

- Chữ hoa -> chữ thường

```
# echo "$STRING" | awk '{print tolower($0)}'
toi ten la son
```

- Chữ thường -> chữ hoa

```
# echo "$STRING" | awk '{print toupper($0)}'
TOI TEN LA SON
```

**Sử dụng chương trình 'sed'**

- Chữ hoa sang chữ thường

```
# echo "$STRING" | sed 's/./\L&/g'
toi ten la son
```

- Chữ thường sang chữ hoa

```
# echo "$STRING" | sed 's/./\U&/g'
TOI TEN LA SON
```

**4.Bash 4.0 shell built-nin**

- Chữ hoa sang chữ thường 

```
# echo "${STRING,,}"
toi ten la son
```

- Chữ thường sang chứ hoa

```
# echo "${STRING^^}"
TOI TEN LA SON
```

**Bài tập lập trình shell, nhập tên tuổi và xuất ra năm đạt 100 tuổi.**

**Đề bài**

Bạn hãy viết 1 chương trình script cho phép user nhập tên và tuổi của họ vào. Sau đó hãy in ra số năm mà user sẽ đạt độ tuổi 60, 80 và 100 tuổi. 

Tạo một file .sh

```
#!/bin/bash

read -p "- Ten ban la gi : " NAME
read -p "- Ban bao nhieu tuoi : " AGE

if [ -z "${NAME}" ];then

echo "-Ban chua nhap ten. Thoat."
exit 1
fi

if [ -z ${AGE} ];then
	echo "- Ban chua nhap tuoi. Thoat"
	exit 1
elif [ ${AGE} -lt 0 ];then
	echo "- Tuoi khong the nho hon 0. Thoat"
	exit 1
fi

CURRENT_YEAR="2019"
AGE_100=$(expr ${CURRENT_YEAR} - ${AGE} + 100)
AGE_80=$(expr ${CURRENT_YEAR} -  ${AGE} +80 )
AGE_60=$(expr ${CURRENT_YEAR} -  ${AGE} +60 )

echo ""
echo "-+ Bạn se 60 tuoi vao nam : ${AGE_60}"
echo "-+ Bạn se 80 tuoi vao nam : ${AGE_80}"
echo "-+ Ban se 100 tuoi vao nam : ${AGE_100}"

exit 0
```
**Tìm user có tên dài nhất và user có tên ngắn nhất trên linux**

- Đầu tiên, ta cần xác định là thông tin tên username trên Linux nằm ở file '/etc/passwd', ở cột thứ 1. Vậy nên ta sẽ filter cột thứ 1 với ký tự phân cách là :

- Kế đến ta sẽ lấy độ dài của từng cái tên, rồi so sánh chúng với giá trị MIN, MAX đã gán giá trị trước đó.

```
#/bin/bash

#Khai báo biến
MAX_LENGTH_NAME=0
MIN_LENGTH_NAME=0
WHO_NAME="unknown"
count=0

# Lay thong tin tren tung username

for name in $(cat /etc/passwd | cut -d':' -f1)
do

# Lay thong tin do dai cua bien 'name'
# Get the length of name 

LENGTH_NAME=${#name}

# So sanh do dai lon nhat, ai dai hon gan bien max cho nguoi do  

if [ ${LENGTH_NAME} -gt ${MAX_LENGTH_NAME} ];then
MAX_LENGTH_NAME="${LENGTH_NAME}"
WHO_MAX_NAME="${name}"
fi

```

**Hướng dẫn code hiện thị thông báo xác nhận yes/no bash shell**

Kết hợp `read` và `case`

```
#!/bin/bash

while true 
do 
	read -p "Ban co muon cai dat chuong trinh nay khong ?" ANSWER
	case $ANSWER in
		[Yy]* )
		echo "Toi muon cai dat !"
		break
		;;
		[Nn]* )
		echo "Toi khong thich cai dat !"
		exit
		;;
		* ) echo "Chon lua chon khac"
		;;
	esac
done

exit 0
```

**Ví dụ trích xuất con số từ 1 chuỗi ký tự trong bash shell**

Ví dụ: Sử dụng đoạn text là 'tôi năm nay 24 tuoi rồi' và trích xuất ra con số '24'

```
# STRING="Toi nam nay 24 tuoi roi."
# echo "${STRING//[!0-9]/}"
24
```

for i in `cat /root/package.txt`;

do
	if [-z `rpm -qa $i`];then
	echo "- Goi chua duoc cai dat"
	echo $i >> /root/install.txt
	exit 1
	fi
done

if [ -e /root/install.txt ];then
	for i in `cat /root/install.txt`;
	do 
		yum install $i -y
```















