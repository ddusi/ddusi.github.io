2020-02-04-MySQL MariaDB change user password



## 2. MySql & MariaDB 계정 비밀번호 변경하기

### MySQL MariaDB change user password





프로젝트를 하면서 아주 사소한 것이지만, 각 DB계정의 비밀번호가 달라서 충돌되는 경우가 있다. 이때 서로 비밀번호를 맞춰주기 위해 DB의 비밀번호를 손 쉽게 변경해 보자 





1. 쿼리를 이용하는 방법

   - 첫번째 방식

   ```
   //update mysql.user set password = password('패스워드') where user ='아이디' and host = '%'; 
   //flush privileges;
    
   update mysql.user set password = password('root') where user = 'root' and host='%';
   flush privileges;
   ```

   - 두번째 방식

   ```
   //set password for '아이디'@'%' = password('패스워드');
   set password for 'root'@'%' = password('root');
   ```

   - 세번째 방식

   ```
   //grant usage on *.* to '아이디'@'%' identified by '패스워드';
   grant usage on *.* to 'root'@'%' identified by 'root';
   ```





2. 커맨드를 사용한 방법

```
//mysqladmin -u아이디 -p기존패스워드 password 신규패스워드
mysqladmin -uroot -proot password newroot
```

개인적으로 커맨드를 사용하는 방식이 더 간단하고 쉽다.

> 이상하게 쿼리문을 이용하면 권한문제인지 잘 적용이 되지 않는다.







