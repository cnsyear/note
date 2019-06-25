# Windows下Mysql5.7忘记密码如何重置

> 操作步骤

- 1.停止mysql服务

```
net stop mysql
```

- 2.关闭mysql安全检查

```
mysqld --skip-grant-tables

// 备注:执行完毕之后,此时如果不是处于等待状态, 而是命令已经结束, 则证明服务
// 有问题.
// 楼主在这耽搁了很久, 后来重启电脑从第一部从新操作解决问题.
```

- 3.依次执行下面命令,重置密码

```
mysql -u root

// 备注:该命令结束后,会出现enter password, 直接回车. 如果回车后报错, 
// 提示需要密码, 则步骤2出现问题. 可能mysql服务非正常停止. 我是通过重启
// 电脑解决

use mysql;

UPDATE user SET authentication_string=PASSWORD("root") WHERE User='root';
// 5.7以上密码对应字段为authentication_string,而非password

FLUSH PRIVILEGES;

quit;
```
