忘记MYSQL的root账户密码时重置密码的方法()
1、修改MYSQL的登录设置文件/etc/my.cnf
vi /etc/my.cnf (可以利用whereis命令查找文件的路径）
然后在[mysqld]段中加上 skip-grant-tables,修改后保存并退出

2、重新启动mysqld
```/etc/init.d/mysqld restart
   #service mysqld restart 效果等同
```
3、连接Mysql数据库，此时连接数据库不需要输入密码
4、修改数据库中root的密码（mysql版本更新中已经将user表中的password字段替换成authentication_string字段，需注意使用的版本用的是哪个字段）
```
	>USE mysql;
	>UPDATE user set authentication_string=password('新密码') where user='root' and host='localhost';
	>flush privileges;
	>quit;
```
5、将配置文件中增加的skip-grant-tables删除后再保存，并重启mysql服务
[参考链接](https://blog.51cto.com/lxsym/477027)