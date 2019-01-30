# **Modify the Command Line Prompt**

- Biến `PS1` là chuỗi ký tự được hiển thị như lời nhắc của command line. hầu hết các bản distro đều set PS1 là các giá trị mặc định đã biết, ví dụ ubuntu là user và hostname:

```
[root@localhost ~]#  echo $PS1
[\u@\h \W]\$
[root@localhost ~]# export PS1='[\u@\h \W(customt)]# '
[root@localhost ~(customt)]# echo $PS1
[\u@\h \W(customt)]#
[root@localhost ~(customt)]#  export PS1='[\u@\h \W]#
```

