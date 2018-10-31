#实验2

##实验步骤

- 第1步：以system登录到pdborcl，创建角色con_res_view和用户new_user，并授权和分配空间：

```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_view;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO con_res_view;
Grant succeeded.
SQL> CREATE USER new_user IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER new_user QUOTA 50M ON users;
User altered.
SQL> GRANT con_res_view TO new_user;
Grant succeeded.
SQL> exit
```
> 语句“ALTER USER new_user QUOTA 50M ON users;”是指授权new_user用户访问users表空间，空间限额是50M。

![自定义运行结果](https://github.com/YangTingGet/Oracle/new/master/1.png)
![自定义运行结果](https://github.com/YangTingGet/Oracle/new/master/2.png)
![自定义运行结果](https://github.com/YangTingGet/Oracle/new/master/3.png)
![自定义运行结果](https://github.com/YangTingGet/Oracle/new/master/4.png)
