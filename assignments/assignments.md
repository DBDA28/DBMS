Session 4- Lab Assignment

Question: using customers and product table, write sql query to find the salespersons andcustomers he
handles, print customer name, city, salesman, commission.
Solution:-
`select c.name, p.commission, p.salesman from product p inner join customer c on p.cust_id = c.cust_id where p.commission in
(select max(commission) from product group by salesman);`
