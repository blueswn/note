## Mysql问题

### 问题：Table 'performance_schema.session_status' doesn't exist

解决：进入Mysql的安装目录的bin文件夹，打开cmd进入该目录执行`mysql_upgrade -u root -p --force`命令然后输入密码问题解决。
