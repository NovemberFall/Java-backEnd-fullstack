## MySQL configuration

- 配置环境变量，如何terminal上打开
- 如何更改密码

---


### open on terminal && change to new password

```ruby

## open terminal and type

sudo sh -c 'echo /usr/local/mysql/bin > /etc/paths.d/mysql'


## then close terminal and open a new terminal and type

mysql -u root -p


## now to set new password type

ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';

```







