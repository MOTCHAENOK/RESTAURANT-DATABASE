# RESTAURANT-DATABASE
#TO CREATE A RESTAURANT DB
create database restaurant;
use restaurant;

create table customer(
customer_id int auto_increment primary key,
first_name varchar(100),mobile_number int,mail_id varchar(100), location varchar(50));

create table menu (
menu_id int,varity varchar(100)not null,
price int unique,cool_drinks varchar(200) default "unknown");
     
create table tables(
table_id int,tablename varchar(100),
seats varchar(100),status varchar(100));
     
create table orders(
order_id int not null,menu_id int,
quantity int not null,verify varchar(100));
     
create table reservation(
reservation_id int primary key auto_increment,
reservation_datetime datetime,
table_id int,customer_id int,
foreign key(customer_id) references customer(customer_id) );

#-----insert values    
insert into customer (customer_id,first_name,mobile_number,mail_id,location)
values (1,"hari",8248,"harihari@","chennai"),
(2,"pratha",3464,"perpar@",null),
(3,"alen",2975,"aleale@","salem"),
(4,"kumar",7502,"kumkum@",null),
(5,"akesh",5963,"akak@","karur");

insert into menu(menu_id,varity,price)values(10,"dosa",50),
(11,"rice",80),
(12,"chicken",120),
(13,"noodles",140),
(14,"non veg",100);
     
insert into tables (table_id,tablename,seats,status)
values(1,"A","5s","avible"),
(2,"B","2s","not"),
(3,"C","4s","avible"),
(4,"D","10s","avible"),
(5,"E","1s","not");
     
insert into orders(order_id,menu_id,quantity,verify)
values (12,10,100,"yes"),
(13,11,50,"yes"),
(148,56,260,"noo"),
(11,76,50,"yes"),
(24,35,67,"noo");

insert into reservation (reservation_id, reservation_datetime, table_id, customer_id) 
values (1, '2024-01-02 12:00:00', 1, 1),
(2,'2024-10-2 10:00:00',2,2),
(3,'2024-3-4 10:10:00',3,3),
(4,'2025-10-5 13:10:00',4,4),
(5,'2025-5-10 5:20:00',5,5);
     
 select*from customer;
 select*from menu;
 select*from tables;
 select*from orders;
 select*from reservation;
##----alter
     
 alter table tables change tablename tab_name varchar(50);
 alter table customer add column last_name varchar(100);
 
 ##----truncate
 truncate table orders;
 
 ##----drop
 drop database restaurant;
 
 ##---update
 update menu set varity ='dish_name';
 update customer set first_name= 'sori' where customer_id=1;
 
 ##---delete
 delete from reservation where customer_id = 4;
 
 describe table menu;
 
 #####--------NULL HANDLING(null,is null, not null)
 
select count(*) from customer where location = null;
select * from customer;
select count(*) from customer where location is null;
select count(*) from customer where last_name is null;
select count(*) from customer where location is not null

#--storing a sting value it is not a null value
insert into customer(customer_id,first_name,mobile_number,mail_id,location)
values (6,"Enok",94747847,"null","pamban");
##--example error "null" is a string

select customer_id,first_name,mobile_number,mail_id,location
from customer
where mail_id is null or
location is null or mobile_no is null ;

select customer_id,first_name,mobile_number,mail_id,location
from customer
where mail_id =  "null";

#--coalesce
select customer_id,mail_id,location,coalesce(location,"Abc")
from customer;
 
 #--if null and alias
 
select customer_id,
       mail_id,
       location,
       ifnull(location, 'AAA')
FROM customer;

#--default added values "unknown"
select * from menu;

 select * from menu;

 #--projection
 select table_id,customer_id from reservation;
 
 select * from orders where verify = "yes";
 
 #--like
 select table_id,tablename from tables where status like "available";
 
 #---between
select reservation_datetime , customer_id from reservation where table_id between 1 and 5;
 
#--or
select * from orders where verify = "yes" or "noo";

#--order by,asc
select * from customer order by first_name  asc;
#--group by ,sum
select order_id,sum(quantity) from orders as total_quantity group by order_id;
#--!=
select * from tables where tablename != "A";
#--=
select * from tables where status = "not";
#---<,>
select * from tables where table_id <3;
select * from menu where menu_id >11;

#--<=,>=
select * from reservation where reservation_id <= 4;
select* from orders where quantity >=100;

#--Aggregation,Grouping
#--sum,group by
select order_id, sum(quantity) as total_quantity
from orders 
group by order_id;
#--count
select count(*) as seats
from tables;

select count(*) as verified_orders
from orders
where verify = 'yes';

#--max,min,avg
select avg(reservation_price) as avg_reservation_price from reservation;
select max (reservation_price) asmax_reservation_price
from reservation;
select min(quantity) as total_quantity from orders;

select* from customer where location in ("chennai","karur");


drop table if exists orders;

create table orders (
    order_id int primary key auto_increment,
    customer_id int not null,
    menu_id int not null,
    quantity int not null
);

insert into orders (order_id,customer_id, menu_id, quantity)
values
(001,1, 10, 2), 
(002,1, 11, 1),  
(003,2, 12, 1);   

select c.first_name,c.location,m.varity as menu_item,o.quantity
from orders o
join  customer c on o.customer_id = c.customer_id
join menu m on o.menu_id = m.menu_id;

#----joins
select c.customer_id, c.first_name, m.varity, o.quantity
from orders o
inner join customer c on o.customer_id = c.customer_id
inner join menu m on o.menu_id = m.menu_id;

select c.customer_id, c.first_name, m.varity, o.quantity
from customer c
left join orders o on c.customer_id = o.customer_id
left join menu m on o.menu_id = m.menu_id;

select c.customer_id, c.first_name, m.varity, o.quantity
from customer c
right join orders o on c.customer_id = o.customer_id
right join menu m on o.menu_id = m.menu_id;


select c.customer_id, c.first_name, m.varity, o.quantity
from customer c
left join orders o on c.customer_id = o.customer_id
left join menu m on o.menu_id = m.menu_id

union 

select c.customer_id, c.first_name, m.varity, o.quantity
from customer c
right join orders o on c.customer_id = o.customer_id
right join menu m on o.menu_id = m.menu_id;

#--subquires, filtering 

select first_name, location
from customer c
where exists (select 1
from orders o
where o.customer_id =  c.customer_id
);

select varity
from menu
where menu_id in (
select menu_id
from orders
where customer_id in (
select customer_id
from customer
where location = 'chennai' ));

select customer_id, first_name, location
from customer
where customer_id in (
select customer_id
from orders
where quantity > (select avg(quantity) from orders)
);

select *
from menu
where menu_id in (
select menu_id
from orders
where customer_id in (
select customer_id
from customer
where location = 'chennai' ));

create view chennai_orders  as
select c.customer_id, c.first_name, m.varity, o.quantity
from customer c
join orders o on c.customer_id = o.customer_id
join menu m on o.menu_id = m.menu_id
where c.location = 'chennai';

show create view customer_orders;
show full tables where table_type = 'view';
drop view customer_orders;

delimiter //

create procedure getcustomerorders(in cust_id int)
begin
select o.order_id, m.varity, o.quantity
from orders o
join menu m on o.menu_id = m.menu_id
where o.customer_id = cust_id;
end //

delimiter ;

call getcustomerorders(101);

delimiter //

create function totalquantity(cust_id int)
returns int
deterministic
begin
declare total int;
select sum(quantity) into total
from orders
where customer_id = cust_id;
return ifnull(total, 0);
end //

delimiter ;


show procedure status where db = 'your_database';
