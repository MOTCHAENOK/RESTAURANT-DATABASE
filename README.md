# RESTAURANT-DATABASE
#TO CREATE A RESTAURANT DB
create database restaurant;
use restaurant;
     
create table customer(
customer_id int auto_increment primary key,
first_name varchar(100),mobile_number int,mail_id varchar(100));

create table menu (
menu_id int,varity varchar(100)not null,
price int unique);
     
create table tables(
table_id int,tablename varchar(100),
seats varchar(100),satus varchar(100));
     
create table orders(
order_id int not null,menu_id int,
quantity int not null,verify varchar(100));
     
CREATE TABLE reservation(
reservation_id INT PRIMARY KEY AUTO_INCREMENT,
reservation_datetime DATETIME NOT NULL,
table_id INT,customer_id INT,
FOREIGN KEY (customer_id) REFERENCES customer(customer_id) );
     
insert into customer (customer_id,first_name,mobile_number,mail_id)
values (1,"hari",8248,"harihari@"),
(2,"pratha",3464,"perpar@"),
(3,"alen",2975,"aleale@"),
(4,"kumar",7502,"kumkum@"),
(5,"akesh",5963,"akak@");
     
insert into menu(menu_id,varity,price)values(10,"dosa",50),
(11,"rice",80),
(12,"chicken",120),
(13,"noodles",140),
(14,"non veg",100);
     
insert into tables (table_id,tablename,seats,satus)
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

INSERT INTO reservation (reservation_id, reservation_datetime, table_id, customer_id) 
VALUES (1, '2024-01-02 12:00:00', 1, 1),
(2,'2024-10-2 10:00:00',2,2),
(3,'2024-3-4 10:10:00',3,3),
(4,'2025-10-5 13:10:00',4,4),
(5,'2025-5-10 5:20:00',5,5);
     
 select*from customer;
 select*from menu;
 select*from tables;
 select*from orders;
 select*from reservation;

     
 alter table tables change tablename tab_n varchar (100);
 alter table customer add column last_name varchar(100);
 truncate table orders;
 
 drop database restaurant;
 
 
