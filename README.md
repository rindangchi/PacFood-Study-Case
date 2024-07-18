# Introduction
This project is part of Pacmann Relational Database Class Week 8. 

# Case Description

## PacFood Business Overview

PacFood is food delivery service in Indonesia which partners with many restaurants in Indonesia. PacFood already has a lot of customers around Indonesia. 

## PacFood Business Model

- Customer choose restaurant in PacFood application then start to order the food
- Restaurant will prepare the food 
- When the food is ready PacDriver will pick up the food and deliver it to customers
- Customers receive their orders and pay the orders via cash



## Objective 
- Design relational database for PacFood
- Create dummy data to validate the database design. To validate the database design using dummy data below actions will be performed:
  - Text search review
  - Display restaurant based on particular menus
  - Display 5 nearest retaurant based on user's location
  - Rank restaurants based on order numbers

## Features and Limitations
### Restaurant
- Each restaurant has different menus
- Each restaurant should complete its address details
- Each restaurant should have at least one menu

### Customer
- Customers should complete their address details
- Each Customer can only have one address
- Customers can place their orders from nearby restaurant
- Customers can order multiple menus in one order
- A single order can only be placed from one restaurant

### Order
- Customers can write review about their orders
- Customer can give like or dislike with their orders
- Payment method is only via cash
- Order has five status: Confirmed, Processed, Delivering, Delivered, Cancelled
- Every status change will be logged in the system

### Driver
- Pacfood has partnered with several drivers
- Each Pacfood driver should have da valid driver license
- Drivers should complete their vehicle details
- Drivers are able to update its current location


# Design Process

## Mission Statement

Based on the Pacfood business overview and business model that has been described in section "Case Desciprtion", the mission statements of PacFood Delivery are described below:

- To provide a platform that connects restaurants and customers
- To help restaurants get more customers and revenues
- To make people easier to order food via online
- To organize drivers who responsible to deliver foods for customers

### Creating Table Structure

#### Identify Table Name

In this section, table names will be identified based on the business model that has been described before.

- Identify tables based on actor involved in the businesss:

| Table Name  | Description   |
| ------------- | ------------- |
| restaurant| To store detailed information about restaurant that partnered with PacFood | 
| users | To store detailed information about users who use Pacman service|
| driver | To store detailed information about driver who partnered with PacFood | 


- Identify tables based on features and limitations
  - Restaurant, user and drivers only domicile in Indonesia --> need a validation table to store data about cities in Indonesia
  - Drivers can update their coordinates --> need a table that can store coordinate logs
  - Each restaurant has at least one menu --> need a table that store menu data
  - Users enable to place orders from nearby restaurant --> need a table to store order information
  - User enable to place several menus in one order, but only from one restaurant --> need a table to store order detail with menu and restaurant information
  - Every status change will be logged in the system --> need a table to store change status log

| Table Name  | Description   |
| ------------- | ------------- |
| driver_coordinate | To store logs of driver coordinate position|
| food | To store food data sold by restaurants | 
| city | To store name of cities in Indonesia | 
| orders | To store information about order placed by user, including order status and driver |
| order_details | To store information about order details, such as food, menu ordered| 
| order_status | To store order status  | 
| order_status_log | To store order status change| 

Finally, there will be ten tables need to be created for PacFood delivery.

Besides the ten tables that already mentioned, we also required to create INDEX, the requirements are stated as below :

- Create Index for table Food field food_name because user is mainly searching by food name
- Create Index for table driver_coordinate field coordinate, the purpose is to search the nearest driver from the user's location

#### Identify Fields for Each Table

After deciding what tables need to be created, in this step fields will be defined for each table. 

| Table Name                 | Fields : data type                | Field Description                                                 | Key                 |
| -------------              | -------------                     | -----------------                                                 |-------------        |
| **city**                   | - city_id   : int                 | Store unique id for each city                                     | Primary Key (PK)    |
|                            | - name : varchar (225)            | Store restaurant'sname                                            |                     |
| **restaurant**             | - restaurant_id : int             | Store unique id for each restaurant                               | Primary Key (PK)    |
|                            | - name : varchar (225)            | Store restaurant name                                             |                     |
|                            | - email : varchar (225)           | Store email address of restaurant                                 |                     |
|                            | - phone_number : varchar (20)     | Store phone number of restaurant                                  |                     |
|                            | - address : text                  | Store information about address of restaurant                     |                     |
|                            | - city_id : int                   | Store information about city where the restaurant is located      |                     |
|                            | - coordinate : point              | Store coordinate location of the restaurant                       |                     |
|                            | - password : varchar (225)        | Store password information of the restaurant's account            |                     |    
| **food**                   | - food_id : int                   | Store unique id for each food                                     | Primary Key (PK)    |
|                            | - restaurant_id : int             | Store unique id for each restaurant                               |                     |
|                            | - food_name : varchar (225)       | Store information about the food name                             |                     |
|                            | - price : numeric                 | Store information about the food's price                          |                     |
|                            | - description : text              | Store information about the food's description                    |                     |
|                            | - availibillity : boolean         | Store information whether food is available or not                |                     |
| **users**                  | - user_id : int                   | Store unique id for each user                                     | Primary Key (PK)    |
|                            | - username : varchar (225)        | Store unique username for each user                               |                     |
|                            | - first_name : varchar (225)      | Store firstname of user                                           |                     |
|                            | - last_name : varchar (225)       | Store lastname of user                                            |                     |
|                            | - email : varchar (225)           | Store email address of user                                       |                     |
|                            | - phone_number : varchar (20)     | Store phone number of user                                        |                     |
|                            | - address : text                  | Store information about address of user                           |                     |
|                            | - city_id : int                   | Store information about city where user resided                   |                     |
|                            | - coordinate : point              | Store coordinate current location of user                         |                     |
|                            | - password : varchar (225)        | Store password information of user's account                      |                     | 
| **driver**                 | - driver_id : int                 | Store unique id for each driver                                   | Primary Key (PK)    |
|                            | - username : varchar (225)        | Store unique username for each driver                             |                     |
|                            | - first_name : varchar (225)      | Store firstname of driver                                         |                     |
|                            | - last_name : varchar (225)       | Store lastname of driver                                          |                     |
|                            | - email : varchar (225)           | Store email address of driver                                     |                     |
|                            | - phone_number : varchar (20)     | Store phone number of driver                                      |                     |
|                            | - driver_license : varchar (15)   | Store information about driver's license no.                      |                     |
|                            | - city_id: int                    | Store information about city where driver resided                 |                     |
|                            | - license_plat : varchar (20)     | Store information about licene plate no.                          |                     |
|                            | - password : varchar (225)        | Store password information of driver's account                    |                     |
| **driver_coordinate**      | - driver_coordinate_id : int      | Store unique id for each driver                                   | Primary Key (PK)    |
|                            | - driver_id : int                 | Store unique id for each driver                                   |                     |
|                            | - created_at : timestamp          | Store information when the coordinate is created                  |                     |
|                            | - coordinate : point              | Store coordinate information                                      |                     |
| **order_status**           | - order_status_id : int           | Store unique id for order status                                  | Primary Key (PK)    |
|                            | - status : varchar (20)           | Store information about status types                              |                     |
| **orders**                 | - order_id : int                  | Store unique id of each order                                     | Primary Key (PK)    |
|                            | - user_id: int                    | Store user id of user who order the food                          |                     |
|                            | - driver_id : int                 | Store driver id who deliver the food                              |                     |
|                            | - created_at : timestamp          | Store date information when the order is placed                   |                     |
|                            | - delivery_charge : numeric       | Store total charge for the order                                  |                     |
|                            | - review: text                    | Store user's review for the order                                 |                     |
| **order_detail**           | - order_detail_id : int           | Store unique id of ecah order                                     |                     |
|                            | - order_id : int       		 | Store unique id of each order related an order detail             |                     | 
|                            | - food_id : int         		 | Store unique id of food related to order detail                   |                     | 
|                            | - qty : numeric	                 | Store qty of food that ordered by user                            |                     | 
|                            | - is_like : boolean	         | Store information whether user like/dislike the food being ordered|                     |
| **order_status_log**       | - order_status_log_id : int       | Store unique id of ecah order status log                          | Primary Key (PK)    |
|                            | - order_id : int                  | Store unique id of each order related to status log               |                     | 
|                            | - order_status_id : int           | Store status type related to order status log                     |                     | 
|                            | - created_at : timestamp          | Store informartion about the date of current status               |                     | 


#### Identify Relationships Among Tables

After defining required fields for each table, the next step is to define relationship among the tables, below are the relationship defined for teh tables:

|                       | city       | resaturant | user     | driver            | driver_coordinate | food         | order_status | orders       | order_detail     | order_status_log |
| ----------            | ---------- | ---------- | ---------| ----------        | ----------        | ----------   | ----------   | ----------   | -----------      | --------------   |
| city                  |            |   1:N      |  1:N     |  1:N              |                   |              |              |              |                  |                  |
| restaurant            |            |            |          |                   |                   |  1:N         |              |              |                  |                  |
| users                 |            |            |          |                   |                   |              |              | 1:N          |                  |                  |
| driver                |            |            |          |                   |  1:N              |              |              | 1:N          |                  |                  |
| driver_coordinate     |            |            |          |                   |                   |              |              |              |                  |                  |
| food                  |            |            |          |                   |                   |              |              |              |  1:N             |                  |
| order_status          |            |            |          |                   |                   |              |              |              |                  |  1:N             |
| orders                |            |            |          |                   |                   |              |              |              |  1:N             |  1:N             |
| order_detail          |            |            |          |                   |                   |              |              |              |                  |                  |
| order_status_log      |            |            |          |                   |                   |              |              |              |                  |                  |


#### Entity Relationship Diagram

After define tables, fields, and relationship among the tables, the next step is to create Entity Relationship Diagram (ERD). In this case ERD is created using lucidchart.

Below is teh ERD design: 

![image](https://github.com/user-attachments/assets/3fc71595-f0a4-4a2a-924a-e31ec5e5fba1)


### Business Rules and Constraints


| Table Name                 | Business Rules                                                               | Constraints                                                                 |
| -------------              | -------------                                                                | -----------------                                                           |
| **city**                   | primary key is not auto increment                                            |                                                                             |
| **order_status**           | primary key is auto increment                                                | order_status_id type : serial                                               |
| **restaurant**             | information in table restaurant must complete                                | NOT NULL for below fields: name, email, phone_number, address, city_id, coordinate, password                   |
|                            | primary key is auto increment                                                | restaurant_id type : serial                                                 |
| **food**                   | information in table foods must complete, except description                 | NOL NULL for below fields: restaurant_id, food_name, price, description, availibity                            |     
|                            | primary key is auto increment                                                | food_id type : serial                                                       |
|                            | price should be more than 0                                                  | CHECK in field price > 0                                                    |
|                            | value for default_availibity is TRUE                                         | Availibility DEFAULT TRUE                                                   |
| **users**                  | information in table user must complete, except last name                    | NOT NULL for below fields: user_id, username, first_name, email, phone, address, city_id, coordinate, password |
|                            | primary key is auto increment                                                | user_id type : Serial                                                       |
| **driver**                 | information in table driver must complete, except last name                  | NOT NULL for below fields: driver_id, username, first_name,email, phone_number, driver_license, city_id, license_plat, password  |
|                            | primary key is auto increment                                                | driver_id type : Serial                                                     |
| **driver_coordinate**      | information in table driver_coordinate must complete                         | NOT NULL for below fields: driver_id, created_at, coordinate                |
|                            | primary key is auto increment                                                | driver_coordinate_id type : serial                                          |
| **orders**                 | information must complete for field: user_id, created_at, deliverry_charge   | NOT NULL for below fields: user_id, created_at, deliverry_char              |
|                            | value for delivery_charge should more than 0                                 | CHECK in field delivery_charge > 0                                          |
|                            | primary key is auto increment                                                | order_id type : serial                                                      |
| **order_detail**           | information in table order_detail mut complete, except field is_like         | NOT NULL for below field: order_detail_id, order_id, food_id, qty           |
|                            | value for qty should more than 0                                             | CHECK in field qty > 0                                                      |
|                            | primary_key is auto increment                                                | order_detail_id type : serial                                               |
| **order_status_log**       | information in table order_status_log must complete                          | NOT NULL for below fields: order_id, order_status_id, created_date          |
|                            | primary_key is increment                                                     | order_status_log_id type : serial                                           |


# Create Database in Postgresql

The next step is to create tables in postgresql database. 
## Tools 
- Dbeaver
- Database : postgresql
- Database name : PacFood
- Host : localhost: 5432

## Queries

Below are the queries for each table creation: 

### Table : city

```sql
create table city (
	city_id integer primary key,
	name varchar(225) not unique null 
);
```

### Table : restaurant

```sql

create table restaurant (
	restaurant_id SERIAL primary key,
	name varchar(225) not null,
	email varchar(225) not unique null,
	phone_number varchar(20) not null,
	address text not null, 
	city_id int not null,
	coordinate point not null, 
	password varchar(225) not null,

	constraint fk_restaurant_city
		foreign key(city_id)
		references city(city_id)	
);

```

### Table : food

```sql
create table food (
	food_id serial primary key,
	restaurant_id int not null,
	food_name varchar(225) not null,
	price numeric not null check(price> 0),
	description text not null,
	availability boolean not null default true,
	
	constraint fk_food_restaurant
		foreign key(restaurant_id)
		references restaurant(restaurant_id)
);

```

### Table : users

```sql
create table users (
	user_id serial primary key,
	username varchar(225) unique not null,
	first_name varchar(225) not null,
	last_name varchar(225), 
	email varchar(225) unique not null,
	phone_number varchar(20) not null,
	address text not null,
	city_id int not null,
	coordinate point not null,
	password varchar(225) not null,

	constraint fk_user_city
		foreign key(city_id)
		references city(city_id)
);

```

### Table : driver

```sql
create table driver (
	driver_id serial primary key,
	username varchar(225) unique not null,
	first_name varchar(225) not null,
	last_name varchar(225), 
	email varchar(225) unique not null,
	phone_number varchar(20) not null,
	driver_license varchar(15) not null,
	city_id int not null,
	license_plat varchar(20) not null,
	password varchar(225) not null,

	constraint fk_driver_city
		foreign key(city_id)
		references city(city_id)
);

```

### Table : driver_coordinate

```sql
create table driver_coordinate (
	driver_coordinate_id serial primary key,
	driver_id int not null,
	created_at timestamp not null,
	coordinate point not null,  

	constraint fk_drivercoordinate_driver
		foreign key(driver_id)
		references driver(driver_id)
);

```

### Table : order_status

```sql
create table order_status (
	order_status_id serial primary key,
	status varchar(20) unique not null
);
```

### Table : orders

```sql

create table orders (
	order_id serial primary key,
	user_id int not null,
	driver_id int,
	created_at timestamp not null, 
	delivery_charge numeric not null check(delivery_charge > 0),
	review text, 
	
	constraint fk_order_user
		foreign key(user_id)
		references users(user_id),
		
	constraint fk_order_driver
		foreign key(driver_id)
		references driver(driver_id)
);

```

### Table : order_detail

```sql
create table order_detail (
	order_detail_id serial primary key,
	order_id int not null,
	food_id int not null,
	qty numeric not null check(qty > 0 ),
	is_like boolean,
	
	constraint fk_orderdetail_order
		foreign key(order_id)
		references orders(order_id),
	
	constraint fk_orderdetail_food
		foreign key(food_id)
		references food(food_id)	
);
```

### Table : order_status_log


```sql
create table order_status_log (
	order_status_log_id serial primary key,
	order_id int not null,
	order_status_id int not null,
	created_at timestamp not null,
	
	constraint fk_orderstatlog_order
		foreign key(order_id)
		references orders(order_id),
		
	constraint fk_orderstatlog_orderstat
		foreign key(order_status_id)
		references order_status(order_status_id)
);
```

Now all tables already created :

![image](https://github.com/user-attachments/assets/c0134518-78d6-4aa7-ab0b-8ba4fb39e031)

Based on the requirements two INDEXes should be created.

### INDEX for table food

```sql

create index idx_food_name
on food using btree(food_name);

```

### INDEX for table driver coordinate

```sql

create index idx_driver_coordinate
on driver_coordinate using gist(coordinate);

```

Two indexes are successfully created:

![image](https://github.com/user-attachments/assets/e8b64fbc-ce93-48f1-b374-0a4bf6244b68)

### ERD Diagram generated from Dbeaver

![image](https://github.com/user-attachments/assets/46250f3d-9574-4055-a158-a1a01f811774)


# Create Dummy data for the table
The next step is to insert some data to the table.

## Install and Import Required Libraries

```python
# install library faker

!pip install Faker
!pip install tabulate
```

```python
# import required library

from faker import Faker
from tabulate import tabulate
import random
from datetime import datetime, timedelta
import csv
```

```python
#localization that we will use faker in format ID (indonesia)
FAKER = Faker("id_ID")
```

## Create Dummy Data
Data for below tables will be generated randomnly. The rest data for other tables is already provided by Pacmann.

- driver coordinate
- order
- order_detail
-order_status_log

### Create function to show data and extract csv file into tabular view

```python
#function to show data 
def show_data(table):
  tab = tabulate(tabular_data = table,
                 headers = table.keys(),
                 tablefmt="psql",
                 numalign="center")
  
  print(tab)
```

```python
#function to extract file .csv to dictionary 
def csv_to_dict(filename):

  #open csv file 

  with open(f'{filename}', mode = 'r', encoding = 'utf-8-sig') as file :
    csv_reader = csv.DictReader(file)

    #save data in dictionary format

    data = {}

    for row in csv_reader:
      for key, value in row.items():

        #set_default used to add key to the result dict
        #value from key, at first added with empty list 
        #empty list filled with method append for each row

        data.setdefault(key, []).append(value)
  return data 
```

### Create Dummy Data : Table driver_coordinate

Table driver_coordinate has relationship with table driver, so we need to extract table driver.

```python
#open table driver 

driver_table = csv_to_dict("/content/drive/MyDrive/Pacmann-PacFood study case/driver.csv")
```

```python
#show table driver

show_data(driver_table)
```

```python

"""
function to create dummy data for driver_coordinate table, with below headers:

- driver_id
- driver_coordinate_id
- created_at
- coordinate

arguments:

- n_data (int) : numbers of coordinates that want to be created
- driver_table (list) : list dictionary of driver data
- is_print (boolean) : if true then will show the result

return:

- table (list)

"""

def driver_coordinate_table(n_data, driver_table, is_print):

  #define start date
  start_date = datetime(2022, 1, 1)

  #define end date
  end_date = datetime(2023, 12, 31, 23, 59, 59)

  #create table
  table = {}

  table["driver_coordinate_id"] = [i + 1 for i in range(n_data)]
  table["driver_id"] = [random.choice(driver_table["driver_id"]) for i in range(n_data)]
  table["created_at"] = [FAKER.date_time_between(start_date = start_date, end_date = end_date) for i in range(n_data)]
  lat_log = [FAKER.local_latlng(country_code = "ID", coords_only = True) for i in range(n_data)]
  table["coordinate"] = [(f'{lat_log[i][0]}, {lat_log[i][1]}') for i in range(n_data)]

  #print table

  if is_print:
    show_data(table)

  return table
```


```python
#create driver_coordinate table for 100 datas

driver_coordinate_table = driver_coordinate_table(100, driver_table, is_print= True)
```

### Create Dummy Data : Table order

Table orders has relationship with table users and table driver. Previously we have extract table driver, now we will extract table user.

```python
#extract table user
user_table = csv_to_dict("/content/drive/MyDrive/Pacmann-PacFood study case/user_data.csv")
```

```python
show_data(user_table)
```

Besides user and driver data, there will also field review in our ERD design for table orders. For review we will take it randomly for table review.csv.

```python
#extract review table
review_table = csv_to_dict("/content/drive/MyDrive/Pacmann-PacFood study case/review.csv")
```

```python
#show review data
show_data(review_table)
```

```python
"""
function to create dummy data for order table.
headers:

- order_id
- user_id
- driver_id
- created_at
- delivery_charge
- review 

arguments:
- n_data (int) : number of data that want to be created
- user_table (list) : list of dictionary data user
- driver_table (list) : list of dictionary data driver
- is_print (bool) : if true then will show the data
- review (text) : review for ecah order

"""

def order_table(n_data, user_table, driver_table, review_table, is_print):

  #define start date
  start_date = datetime(2022, 1, 1)

  #define end date
  end_date = datetime(2023, 12, 31, 23, 59, 59)

  #create table
  table = {}

  table["order_id"] = [i + 1 for i in range(n_data)]
  table["user_id"] = [random.choice(user_table["user_id"]) for i in range(n_data)]
  table["driver_id"] = [random.choice(driver_table["driver_id"]) for i in range(n_data)]
  table["created_at"] = [FAKER.date_time_between(start_date = start_date, end_date = end_date) for i in range(n_data)]
  table["delivery_charge"] = [FAKER.random_int(5_000, 25_000, 1_500) for i in range(n_data)]
  table["review"] = [random.choice(review_table["Review"]) for i in range(n_data)]

  #print table

  if is_print:
    show_data(table)

  return table
```

```python
order_table = order_table(100, user_table = user_table, 
                          driver_table=driver_table, 
                          review_table=review_table, 
                          is_print= True)
```

### Create Dummy Data : Table order_detail

Table order_detail has relation with table food and orders So that we need to extract table food.

```python
# extract tabel food 
food_table = csv_to_dict("/content/drive/MyDrive/Pacmann-PacFood study case/food.csv")
```

```python
#show data
show_data(food_table)
```

```python
"""
function to create dummy data for order detail table.
headers:

- order_detail_id
- order_id
- food_id
- qty

arguments:
- n_data (int) : number of data that want to be created
- order_table (list) : list of dictionary order data
- food_table (list) : list of dictionary food data
- is_print (bool) : if true then will show the data

"""
def order_detail_table(n_data, order_table, food_table, is_print):
  #create table
  table = {}

  table["order_detail_id"] = [i + 1 for i in range(n_data)]
  table["order_id"] = [random.choice(order_table["order_id"]) for i in range(n_data)]
  table["food_id"] = [random.choice(food_table["food_id"]) for i in range(n_data)]
  table["delivery_charge"] = [FAKER.random_int(1, 15, 1) for i in range(n_data)]
  table["is_like"] = [FAKER.boolean(chance_of_getting_true=85) for i in range(n_data)]

  #print table

  if is_print:
    show_data(table)

  return table
```

```python
order_detail_table = order_detail_table(150, order_table = order_table, 
                          food_table=food_table, 
                          is_print= True)
```

### Create Dummy Data: order_status_log

Able order_status_log has relationship with table order and order_status.

```python
#extract table order_status
order_status_table = csv_to_dict("/content/drive/MyDrive/Pacmann-PacFood study case/order_status.csv")
```

```python
show_data(order_status_table)
```

```python
#create function generate status

"""
function generate status used to generate order_status_id randomly in table order_status_log
This function will create status id based on below rules:
- Each order with delivered status (id = 4) should also have status Confirmed (1), Processed (2), and Delivering (3). These status should be in a sqquence order form 1-2-3-4
- Function will assign order status Cancelled (5) for order with order_ids that multiples of 10

arguments:

order_table(list) : list of order

return :
list_status (list) : combination of id and status

"""
def generate_status(order_table):

    list_status = list()

    for i in order_table['order_id']:
      if(i%10 != 0) :
        for j in order_status_table['order_status_id'][:-1]:
          order_id = i
          status = j
          start_date = order_table['created_at'][i-1] + timedelta(hours=int(j))
          end_date = order_table['created_at'][i-1] + timedelta(hours=int(j)+1)
          created_at = FAKER.date_time_between(start_date, end_date)
          data = (f'{order_id} {status} {created_at}')
          list_status.append(data)
      else:
        order_id = i
        status = 5
        created_at = order_table['created_at'][i-1] + timedelta(minutes = 10)
        data = (f'{order_id} {status} {created_at}')
        list_status.append(data)
    return list_status   

```

```python
# function to create dummy data for order_status_log table.

"""
function to create dummy data for order_status_log table.
headers:
- order_status_log_id
- order_id
- order_status_id
- created_at
arguments:

- order_table (list) : list of dictionary order data
- order_status_table (list) : list of dictionary food data
- is_print (bool) : if true then will show the data
"""

def order_status_log_table(order_table, order_status_table, is_print):

  #create table
  table = {}
  list_status = generate_status(order_table)
  table["order_status_log_id"] = [i + 1 for i in range(len(list_status))]
  table["order_id"] = [i.split(' ')[0] for i in list_status]
  table["order_status_id"] = [i.split(' ')[1] for i in list_status]
  table["created_at"] = [f"{i.split(' ')[2]} {i.split(' ')[3]}" for i in list_status]

  #print table

  if is_print:
    show_data(table)

  return table
```

```python
order_status_log_table = order_status_log_table(order_table = order_table, 
                          order_status_table=order_status_table, 
                          is_print= True)
```

### Save Data in .csv format

```python
"""
function to generate dummy data into csv. 
arguments:

- data (list) : lit of dictionary data that will be save as csv file
- filename (string) : name for the csv file

return:
None 
"""

def save_to_csv(data, filename):

  #create csv file 
  with open(file = f"{filename}.csv", mode = "w", newline = "") as file:

    #create csv writer
    writer = csv.writer(file)

    #write header csv
    writer.writerow(list(data.keys()))

    #display length of data
    len_data = len(list(data.items())[0][1])

    #write data to csv file
    for i in range(len_data):
      row = []
      for key in data.keys():
        row.append(data[key][i])
      writer.writerow(row)
```

```python
#save data driver_coordinate to csv
save_to_csv(data = driver_coordinate_table, filename="driver_coordinate")

#save data order to csv
save_to_csv(data = order_table, filename="orders")

#save data order_detail to csv
save_to_csv(data = order_detail_table, filename="order_detail")

#save data order_status_log to csv
save_to_csv(data = order_status_log_table, filename="order_status_log")

```

# Copy Dummy Data to Database

The lat step is to copy the dummy data to the real tables in the database. 

```sql
copy city
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/city.csv'
csv 
header;

copy restaurant
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/restaurant.csv'
csv
header;

copy food
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/food.csv'
csv
header;

copy users
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/user_data.csv'
csv
header;

copy driver
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/driver.csv'
csv
header;

copy driver_coordinate
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/driver_coordinate.csv'
csv
header;

copy order_status
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/order_status.csv'
csv 
header;

copy orders
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/orders.csv'
csv 
header;

copy order_detail
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/order_detail.csv'
csv 
header;

copy order_status_log
from '/Users/rindangcahyaning/Documents/Bootcamp/Pacmann DE - Build RDBMS/pacfood/order_status_log.csv'
csv 
header;
```

# Retrive Data based on Business Question

After successfully inserting data to the tables, analysis by using SQL queries are performed to answer saveral business questions.

1. Retrive review data that the reviews are containing negative words, such as disappointed, bad, or sucks. Display the resaurant name and the reviews.

```sql
select r.name , o.review 
from orders o 
join order_detail od 
on o.order_id = od.order_id 
join food f 
on f.food_id  = od.food_id 
join restaurant r 
on r.restaurant_id = f.restaurant_id 
where review ilike '%sucks%' or review ilike '%Bad%' or review ilike '%disappointed%'

```

Result

![image](https://github.com/user-attachments/assets/8ca772da-a24e-4682-ac05-adcf1e9e0928)


2. Display all restaurants that have menu : Ayam, Bebek , Mie. Display restaurant names and menus.

```sql
select r.name, f.food_name
from food f 
join restaurant r 
on f.restaurant_id = r.restaurant_id 
where f.food_name ilike '%Bebek%' 
or f.food_name ilike '%mie%' 
or f.food_name ilike '%ayam%'
```

Result

![image](https://github.com/user-attachments/assets/a119f1aa-fee7-478f-a5f0-1e7e29283170)

   
3. Display 3 nearest restaurant for user with user_id : 24, display the restaurant names and the distances

Using postgis module from postgresql. At first, need to download and install postgis first. Many documentation out there that can be used as reference.

```sql
with user_coordinate as (
select st_setsrid(st_makepoint(coordinate[0], coordinate[1]), 4326)::geometry(point, 4326) as coordinate
from users u
where user_id = 24
),
resto_coordinate as (
select name, address, st_setsrid(st_makepoint(coordinate[0], coordinate[1]), 4326)::geometry(point, 4326) as coordinate
from restaurant r 
)
select name, address, distance_meter from 
(

select name, address, r.coordinate as rc,
	   u.coordinate as uc,
	   st_distance(
	   r.coordinate::geography, 
	   u.coordinate::geography
	   )
	   as distance_meter
	  
from resto_coordinate r
cross join user_coordinate u ) a

order by distance_meter asc 

limit 3;

```

Result:

![image](https://github.com/user-attachments/assets/b9c0e995-671e-4fde-939d-4526e9660e31)


4. Ranking popularity of reataurants based on number of orders. Display restaurant names and teh total order.

```sql
select r.name, count(o.order_id) as total_order,
dense_rank () OVER (ORDER BY count(o.order_id) DESC) ranking
from restaurant r 
join food f
on r.restaurant_id = f.restaurant_id 
join order_detail od 
on od.food_id = f.food_id 
join orders o
on o.order_id = od.order_id 
group by r.name
order by total_order desc;

```

Result:

![image](https://github.com/user-attachments/assets/a63f2a6e-bbea-4c88-b346-84fe955984ee)

   

