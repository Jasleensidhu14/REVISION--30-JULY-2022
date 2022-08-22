# REVISION--30-JULY-2022
SQL Queries
//////30TH JULY 2022- REVISION //////
create database hurrysale
use hurrysale
CREATE TABLE hurrysale (
	order_id VARCHAR(15) NOT NULL, 
	order_date VARCHAR(15) NOT NULL, 
	ship_date VARCHAR(15) NOT NULL, 
	ship_mode VARCHAR(14) NOT NULL, 
	customer_name VARCHAR(22) NOT NULL, 
	segment VARCHAR(11) NOT NULL, 
	state VARCHAR(36) NOT NULL, 
	country VARCHAR(32) NOT NULL, 
	market VARCHAR(6) NOT NULL, 
	region VARCHAR(14) NOT NULL, 
	product_id VARCHAR(16) NOT NULL, 
	category VARCHAR(15) NOT NULL, 
	sub_category VARCHAR(11) NOT NULL, 
	product_name VARCHAR(127) NOT NULL, 
	sales DECIMAL(38, 0) NOT NULL, 
	quantity DECIMAL(38, 0) NOT NULL, 
	discount DECIMAL(38, 3) NOT NULL, 
	profit DECIMAL(38, 8) NO T NULL, 
	shipping_cost DECIMAL(38, 2) NOT NULL, 
	order_priority VARCHAR(8) NOT NULL, 
	`year` DECIMAL(38, 0) NOT NULL
    );  
    SET SESSION sql_mode = ' '
    //////SET SESSION sql_mode write for handling any error in the dataset. 
    Eg: If there is any comma, or semicolon, any mistake so it ignores by itself./////
select * from hurrysale 
///Load Data from Dataset Downloaded: Remember- Keep data directly in C Drive and keep this :/ sign ///

load data infile
'C:/sales_data_final.csv'
into table hurrysale
fields terminated by ','
enclosed by '"'
lines terminated by '\n'
ignore 1 rows 

select * from hurrysale 
//////Convert string (1/1/2022) to (Jan 1 2022 as Month Date Year Format) to date mode//////
//////Remember: Use % sign then M(month) then backslash followed by d(date) and y(year) //////
//////Eg:-'%m/%d/%Y' to avoid null values//////
////// use Year Y in capital to avoid truncated error//////
select str_to_date(order_date,'%m/%d/%y') from hurrysale 
select * from hurrysale 
//////How to add new column with a existing column : Use after in alter table //////
//////Syntax:- add column newcolumn_name date after existingcolumn_name//////
alter table hurrysale
add column order_date_new date after order_date 
//////Update data into the column to date format:-Use update Command with 'Set' keyword//////
//////SET SQL_SAFE_UPDATE = 0;////// For sql mode error
update hurrysale
set order_date_new = str_to_date(order_date,'%m/%d/%Y')
select * from hurrysale 
alter table hurrysale
add column ship_date_new date after ship_date
select * from hurrysale  
update hurrysale
set ship_date_new = str_to_date (ship_date, '%m/%d/%Y')
select * from hurrysale 
////// QUERIES BASED ON DATE //////
select * from hurrysale where ship_date_new ='2011-01-08' 
select * from hurrysale where ship_date_new > '2011-01-08' 
select * from hurrysale where ship_date_new between '2011-01-08' and '2011-04-22' 

////// Current Time and date together of your laptop: now Command//////
select now() 

///////Current date and Time: curdate and curtime seperate commands//////
select curdate() 
select curtime()
select * from hurrysale where ship_date_new < date_sub(now(), interval 1 week)
select date_sub(now(), interval 1 week) 
select date_sub(now(), interval  1 year) 

