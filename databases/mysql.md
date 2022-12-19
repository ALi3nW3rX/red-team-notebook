# Mysql

```powershell
#Retrieve ALL Data:
select * from users;

#Retrieve Username and Password:
select username,password from users;

#Return only 1 row of data:
select * from users LIMIT 1;

#Return a certain amount of rows and skip a certain amount of rows. First number skips and the second number is how many rows to return
select * from users LIMIT 2,1;

#Return data that matches exactly:
select * from users where username='admin';

#This will return everyone who is not "Admin":
select * from users where username != 'admin';

#This will return rows of either
select * from users where username='admin' or username='jon';

#This will return if both are ture:
select * from users where username='admin' and password='p4ssword';

#Percentage is a wild card to select beginnings or endings.
select * from users where username like 'a%';

#Union
SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;

#Insert
insert into users (username,password) values ('bob','password123');

#Update
update users SET username='root',password='pass123' where username='admin';

#Delete
delete from users where username='martin';

#Delete all the table info:
delete from users;


```
