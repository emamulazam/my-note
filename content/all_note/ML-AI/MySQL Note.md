
Video link: [Youtube-video](https://www.youtube.com/watch?v=yE6tIle64tU)

Handbook link: [Hand book](https://drive.google.com/file/d/1WjyJnDAKflRWvqgZbtM0b-Ur0nQY0VXx/view?usp=drive_link)


# Basic

## Create Database

To create a database name `azam` write

```
create database azam;
```

To use `azam` database 

```
use azam;
```

To delete databases 

```
drop database azam;
```


## Table

### Create Table

Creating a table name `users`

```
create table users (
	id int auto_increment primary key,
    name varchar(100) not null,
    email varchar(100) unique not null,
    gender enum('Male', 'Female', 'Other'),
    date_of_birth date,
    created_at timestamp default current_timestamp
);
```

### Rename Table

To rename table name from `users` to `friend`

```
rename table users to friend;
```

### Delete Table
### Data Types Explained

1. `INT` : Integer type, used for whole numbers.
2. `VARCHAR(100)` : Variable-length string, up to 100 characters.
3. `ENUM` : A string object with a value chosen from a list of permitted values. eg. `gender ENUM('Male', 'Female', 'Other')`
4. `DATE` : Stores date values. eg. `date_of_birth` DATE
5. `TIMESTAMP` : Stores date and time, automatically set to the current timestamp when a row is created.
6. `BOOLEAN` : Stores TRUE or FALSE values, often used for flags like `is_active`.

### Constraints Explained

1. `AUTO_INCREMENT` : Automatically generates a unique number for each row.
2. `PRIMARY KEY` : Uniquely identifies each row in the table.
3. `NOT NULL` : Ensures a column cannot have a NULL value.
4. `UNIQUE` : Ensures all values in a column are different.
5. `DEFAULT` : Sets a default value for a column if no value is provided. eg. `created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP` , `is_active BOOLEAN DEFAULT TRUE`

### See data

To see all data from `users` table

```
select * from users;
```

To see `name` and `email` from `users` table use this

```
select name, email from users;
```

## Alter Table

### Add column in existing table

`is_active` column in `users` table.

```
alter table users add column is_active boolean default true;
```

### Drop column column

To drop / Delete a column a column name `is_active`

```
alter table users drop is_active;
```

### Modify a column type

To change column type

```
alter table users modify column name varchar(150);
```

### Modify column position

To change `email` column position 

```
alter table users modify column email varchar(100) after id;
```

To change `date_of_birth` column position to first.

```
alter table users modify column date_of_birth date first;
```

## Insert value

To insert value to database according to column 

```
insert into users value ('2002-09-24', 1, 'emamulazam@gmail.com', 'azam', 'male', default);
```

Insert data compere column name

Default value will auto update like id, time

```
insert  into users (email, name, gender) value ('eazam@gmail.com', "eazam", "male");
```

You can insert multiple data one time

```
insert  into users (email, name, gender, date_of_birth) value 
('eazam1@gmail.com', "eazam1", "male", "2001-5-2"),
('eazam2@gmail.com', "eazam2", "male", "2001-5-2"),
('eazam3@gmail.com', "eazam3", "male", "2001-5-2"),
('eazam4@gmail.com', "eazam4", "male", "2001-5-2");
```

## Data query

gender not equal to male

```
select * from users where gender != 'male';
```

Born before `1995-01-31`

```
select * from users where date_of_birth < "1995-01-31";
```

id 10 and before

```
select * from users where id <= 10;
```

To see id 5-15

```
select * from users where id between 5 and 15;
```

To see 6300, 65000, 71000 salary people in databases.

```
select * from users where salary in (63000, 71000, 65000);
```

Gender is female and salary is more or equal to 70000

```
select * from users where gender = 'Female' and salary >= 70000;
```

Small to big date 

```
select * from users order by date_of_birth asc;
```

Big to small date

```
select * from users order by date_of_birth desc;
```

To see first 10 row 

```
select * from users limit 10;
```

## Update data

To update data of id 2

```
update users set date_of_birth="2000-01-31" where id=2;
```

To update more then 1 column, here change email and salary

```
update users set email="aarav@gmail.com", salary=70000 where id=1;
```

## Delete data

Delete id 3 to 6 

```
delete from users where id between 3 and 6;
```

Delete row contain this email

```
delete from users where email="ishaan@example.com";
```

## Constraint

Make a `name` column unique

```
alter table users add constraint unique_name unique (name);
```

## Function

To see how many row in a table

```
select count(*) from users;
```

To see how many `Male`

```
select count(*) from users where gender="male";
```

To see min max salary
```
select min(salary), max(salary) from users;
```

If we want to replace the `min(salary)` with `minimum` and `max(salary)` with `maximum`

```
select min(salary) as minimum, max(salary) as maximum from users;
```

To see sum of the salary

```
select sum(salary) from users;
```

To see average salary group wise

```
select gender, avg(salary) from users group by gender;
```

`having` use after group by

```
select gender, avg(salary) as "Avarage Salary", count(*) from users group by gender having avg(salary)>65000;
```

To see birthday to today

```
select name, datediff(curdate(), date_of_birth) as day from users;
```

There are some math function

| *Function*          | *Purpose*              |
| ------------------- | ---------------------- |
| count()             | Count rows             |
| sum()               | Total of a column      |
| avg()               | Average of values      |
| min() / max()       | Lowest / highest value |
| length()            | String length          |
| concat()            | merge strings          |
| year() / datediff() | Date breakdown / age   |
| round()             | Rounding numbers       |
| floor()             | Rounding by minimum    |
| ceil()              | Rounding by maximum    |
| if()                | Conditional logic      |

## Auto Commit and Transactions

To disable auto-commit 

```
set autocommit = 0;
```

To save changes permanently

```
commit;
```

To see last commit

```
rollback;
```

To enable auto-commit

```
set autocommit = 1;
```

## Foreign key

```
CREATE TABLE addresses (
id INT AUTO_INCREMENT PRIMARY KEY,
user_id INT,
street VARCHAR(255),
city VARCHAR(100),
state VARCHAR(100),
pincode VARCHAR(10),
CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

Here a table is creating name addresses 

1. `CONSTRAINT fk_user`:
	This is **naming** the foreign key constraint `fk_user`.
2. `FOREIGN KEY (user_id)`
	This says: _"In the `addresses` table, the column `user_id` must match a value in another table."
3. `REFERENCES users(id)`
	This tells MySQL: _"The valid values for `user_id` come from the column `id` in the `users` table."
4. `ON DELETE CASCADE`
	Meaning: If you delete a user from the `users` table, MySQL will **automatically delete** all related addresses from `addresses`.

## Joint

To make a inner joint to table 

If any user don't have address then it will not return

```
use azam;
select users.name, addresses.city
from users
inner join addresses on users.id = addresses.user_id;
```

left join

Return all the value  of `users.name` column and missing value will null

```
left join addresses on users.id = addresses.user_id;
```

Right join

Return all the value  of `addresses.city` column and missing value will null

```
right join addresses on users.id = addresses.user_id;
```


### Self join

First make and populate the new column

```
alter table users
add column referred_by_id int;

update users set referred_by_id = 1 where id in (2,3,5,15,20,9);
update users set referred_by_id = 2 where id = 4;
select * from users;
```

Now make a join with same table

```
select 
a.id, 
a.name as user_name,
b.name as refferred_by_name
from users a
inner join users b on a.referred_by_id = b.id
```
## Union

To see all the item at once use (no duplicate will return )

```
select email, name from users
union
select email, name from admin_users;
```

To see duplicate use `union all` instead of `union`

order by = increase in order

```
select email, name, date_of_birth, "User" as roll from users
union all
select email, name, date_of_birth, "Admin" as roll from admin_users
order by date_of_birth;
```

## Create View

To Create View

This new virtual table `rich_users` will reflect `users` table content 

```
create view rich_users as
select * from users where salary > 70000;
```

To delete view use

```
drop view rich_users;
```

## Index

To see index of a table use

```
show indexes from users;
```

To create index

```
create index in_salary on users(salary);
```

To create more than 2 column index use

```
create index in_salary on users(name, salary);
```

To delete index use

```
drop index in1_salary on users;
```

## Stored Procedures

To create stored procedures

```
delimiter $$
create procedure select_users()
begin
	select * from users;
end $$
delimiter ;
```

To call the Stored procedure

```
call select_users();
```

To see procedure

```
show procedure status where db = 'azam';
```

To delete procedure

```
drop procedure if exists select_users;
```

