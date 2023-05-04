create table student1 (roll int, name varchar(10), marks float check (marks<100));

insert into student1 values(1,"foo",313);

select * from student1;

create table student1 (roll int, name varchar(10), marks float, primary key(roll,name));

create table student (roll int primary key auto_increment, name varchar(10) not null, marks float default 40);

select count(roll) as total from student;

select sum(marks) from student;

select min(marks) as total from student;

ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';

Q Session 4- Lab Assignment
using customers and product table, write MySQL query to find the salespersons andcustomers he
handles, print customer name, city, salesman, commission.
Solution:
`select c.name, p.commission, p.salesman from product p inner join customer c on p.cust_id = c.cust_id where p.commission in
(select max(commission) from product group by salesman);`

stored procedure for profit/loss-

```MySQL

delimiter &&
create procedure profitloss(SP int,CP int, out result varchar(10) ,out val int)
begin
if(SP>CP) then
        set result='Profit';
	set val = SP-CP;
else
        set result='Loss';
	set val = CP-SP;
end if;
select result,val;
end &&
delimiter ;
  
```
cursor in stored procedure:
```MySQL
delimiter &&
create procedure mycursor()
        begin
        -- variables declaration
        declare r int;
        declare n varchar(10);
        declare m float;
        declare done int default 0;

        -- cursor declaration
        declare cur1 cursor for select roll,name,grade from student
        where grade >= 60;
        -- exception handler for end of result set
        declare continue handler for not found set done=1;

        -- open the cursor and loop
        open cur1;
label:loop

-- fetch the record
fetch cur1 into r,n,m;
if done=1 then leave label;
end if;
insert into backup values(r,n,m);
end loop;
close cur1;


end &&
delimiter ;

```
cursor to for below condition
roll=roll+100 and marks=marks/100 + 1.05
```MySQL
delimiter &&
   create procedure mycursor1()
           begin
           -- variables declaration
           declare r int;
           declare n varchar(10);
           declare m float;
           declare done int default 0;

           -- cursor declaration
           declare cur1 cursor for select roll,name,grade from student
           where grade >= 60;
           -- exception handler for end of result set
           declare continue handler for not found set done=1;

           -- open the cursor and loop
           open cur1;
   label:loop

   -- fetch the record
   fetch cur1 into r,n,m;
   if done=1 then leave label;
   end if;
   insert into backup values(r+100,n,m/100+1.05);
   end loop;
   close cur1;


   end &&
   delimiter ;

```
Trigger in MySQL

```MySQL
delimiter &&
create trigger before_insert_student
before insert on student for each row
begin
    set new.grade=new.grade+1.05;

end &&
delimiter ;

```

```MySQL
delimiter &&
create trigger before_insert_student_checkGrade                     before insert on student for each row
begin
if (new.grade <0 or new.grade > 100) then
set new.grade=40;
end if;
end &&
delimiter ;

```

Inserting in product table generates a billing table with price incl. GST and total billing amount
```MySQL
delimiter &&
create trigger before_insert_product
after insert on product for each row
begin
insert into billing values(new.product_id, new.price*1.18, new.qty*new.price*1.18);
end &&
delimiter ;

```

```MySQL
delimiter &&
create trigger student_log
after update on student for each row
begin
insert into student_log values(user(),now(),concat('previous: ', old.grade,' updated: ', new.grade));
end &&
delimiter ;

```
```MySQL
delimiter &&
create trigger student_log1
after delete on student for each row
begin
insert into student_log values(user(),now(),concat(user(),'deleted','roll no',old.roll));
select what from student_log order by whattime desc limit 1;
end &&
delimiter ;


FIXME

```
