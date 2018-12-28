### 程序无法连接oracle，提示版本8.xx以上
实际上连接的oracle服务器是12版的，之所以提示该错误是由于连接oracle数据库要求客户端本地也有对应的dll（或安装oracle客户端）。

在(官网)[https://www.oracle.com/technetwork/database/database-technologies/instant-client/downloads/index.html]下载，复制其中的关键dll：
```
oci.dll

ociw32.dll

orannzsbb.dll

oraocci.dll

oraociei.dll
```
到程序运行目录即可

但因为服务器x64和客户端x32可能依然会抛出对应的计算机位数异常，所以不能直接从服务器copy对应dll出来，而应该附带对应版本的官网最小组件包中的dll
