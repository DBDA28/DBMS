create a keyspace for tables

```CQL

create keyspace pgdbda
   ... with replication = {
   ... 'class':'SimpleStragtegy',
   ... 'replication_factor':1};

```

creating schema for the table

```CQL

create table emp
          ... (id int primary key,
          ... name text,
          ... salary int,
          ... contact int);
```
Insert data in the table

```CQL

insert into emp (id,name,salary,contact) values(101,'Amar',5600,4567);
insert into emp (id,name,salary,contact) values(102,'Akash',7800,2617);
insert into emp (id,name,salary,contact) values(103,'Asha',4500,9468);
insert into emp (id,name,salary,contact) values(104,'Neeta',8700,8098);
insert into emp (id,name,salary,contact) values(105,'Rani',5900,8234);

```

Alter the table

```CQL

alter table emp
          ... add address text;

```
Dropping the column from table

```CQL

alter table emp drop address;

```
Insert keeping one address field null

```CQL

insert into emp (id,name, salary) values(106,'Raju',6900);

```
update field

```CQL

update emp set contact=3535 where id=106;

```
deleting row from the table

```CQL

delete from emp where id = 106;

```

filter data

```CQL

select * from emp where id in ( 105,102);

```
When filtering the data with conditions. due to perfomance issues allow filtering is used.

```CQL

select * from emp where salary > 6000 allow filtering;

```


practice question

```CQL

create table fb (post_id int primary key, type text, likes int, comments int, shares int);

```

Insert data in the table

```CQL

insert into fb (post_id,type,likes,comments,shares) values(10566,'text',45,3,2);
insert into fb (post_id,type,likes,comments,shares) values(10678,'link',23,6,1);
insert into fb (post_id,type,likes,comments,shares) values(10674,'photo',244,56,6);
insert into fb (post_id,type,likes,comments,shares) values(10326,'photo',42,12,2);
insert into fb (post_id,type,likes,comments,shares) values(10266,'link',133,95,12);
insert into fb (post_id,type,likes,comments,shares) values(10429,'text',580,245,11);
insert into fb (post_id,type,likes,comments,shares) values(10538,'video',255,90,12);
insert into fb (post_id,type,likes,comments,shares) values(10245,'photo',123,90,23);

```
show the contents of the posts with type, likes, comments and shares
cqlsh:pgdbda> select type, likes, comments, shares from fb;

update the likes and comments of id 10538 to 156 and 78 respectively
update fb set likes=156, comments=78 where post_id=10538;

insert new entry record (id ,type, comments and share only)
insert into fb (post_id,type,comments,shares) values(10246,'photo',13,9);

find the total no of likes and shares
select sum(likes) as "sum of likes", sum(shares) as "sum of shares" from fb;

Find average of comments
select avg(comments) as "avg" from fb;

print ids of post with likes more than 100
select post_id from fb where likes > 100 allow filtering;

count total values on likes column
select count(likes) from fb;

Delete the post where the comments are less 10




