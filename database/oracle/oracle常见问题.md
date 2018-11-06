
## 数据库密码默认是180天过期，修改成无限制
1. 查看用户的proifle是哪个，一般是default：
```sql
SELECT username,PROFILE FROM dba_users;
```
2. 查看指定概要文件（如default）的密码有效期设置：
```sql
SELECT * FROM dba_profiles s WHERE s.profile='DEFAULT' AND resource_name='PASSWORD_LIFE_TIME';
```

3. 将密码有效期由默认的180天修改成“无限制”：
```sql
sql>ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;
```
修改之后不需要重启动数据库，会立即生效。

4. 修改后，还没有被提示ORA-28002警告的帐户不会再碰到同样的提示；已经被提示的帐户必须再改一次密码。
```sql
alter user TY_FS identified by DEV_TY_FS;
```