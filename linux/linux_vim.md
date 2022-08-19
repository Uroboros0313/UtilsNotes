> # SSH连接linux

1. 用户名/密码登录

`ssh <username>@<IP address or domain name>`

2. 密钥登录

```
icacls <已下载的与实例关联的私钥文件的路径> /grant <Windows 系统用户帐户>:F
icacls <已下载的与实例关联的私钥文件的路径> /inheritancelevel:r
ssh -i <已下载的与实例关联的私钥文件的路径> <username>@<IP address or domain name>

```
> # Vim
## 删除
```
d1G	删除光标所在到第一行的所有数据
dG	删除光标所在到最后一行的所有数据
```