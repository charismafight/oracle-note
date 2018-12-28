### 程序无法连接oracle，提示版本8.xx以上
实际上连接的oracle服务器是12版的，之所以提示该错误是由于连接oracle数据库要求客户端本地也有对应的dll（或安装oracle客户端）。

在[官网](https://www.oracle.com/technetwork/database/database-technologies/instant-client/downloads/index.html)下载，复制其中的关键dll：
```
oci.dll

ociw32.dll

orannzsbb.dll

oraocci.dll

oraociei.dll
```
到程序运行目录即可

但因为服务器x64和客户端x32可能依然会抛出对应的计算机位数异常，所以不能直接从服务器copy对应dll出来，而应该附带对应版本的官网最小组件包中的dll



### oracle连接字符串中的实例
oracle在安装时默认实例不为空（与sqlserver不同），安装windows客户端时默认的实例名是orcl，所以连接字符串要求ip/orcl来指定实例才可正常访问



### OCIEnvCreate 失败，返回代码为 -1，但错误消息文本不可用。


```
Enter user-name: system
Enter password:
ERROR:
ORA-12560: TNS:protocol adapter error
```
在尝试用sqlplus登录远端oracle服务器时抛出异常，但用服务器端同样命令访问正常

ORACLE_SID、TNS_ADMIN设置之后sqlplus username/pwd@orcl 可以正常连接，但程序问题依旧

sqlplus成功之后，检查程序中的引用，有两类oracle组件，从nuget卸载一个旧的，保留官网的Oracle.ManagedDataAccess.Client后出现新的异常
```
ORA-12514: TNS: 监听程序当前无法识别连接描述符中请求的服务
```
至此已经有更加明确的异常提示了，多半与配置相关
