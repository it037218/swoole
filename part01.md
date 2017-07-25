# swoole下载与安装
## 1、下载swoole
### 环境要求
php版本最好大于5.6
### 下载地址
到https://github.com/swoole/swoole-src/releases  下载最新的版本的swoole拓展源码，并解压到指定文件夹。
# 2、安装
进入swoole源文件目录
phpize
./configure
make
make install

查找并修改php.ini  
	如果服务器上安装了多个版本的php，应该找到对应的php版本的php.ini  
	1、通过phpinfo查找  
	2、通过“sudo find / -name 'php.ini'“ 查找文件所处的位置  
	打开php.ini，添加extension=swoole.so  
	通过php -m 可以查看已加载的模块中是否含有swoole  




