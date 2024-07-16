# Case Description

## PacFood Business Overview

PacFood is food delivery service in Indonesia which partners with many restaurants in Indonesia. PacFood already has a lot of customers around Indonesia. 

## PacFood Business Model

- Customer choose restaurant in PacFood application then start to order the food
- Restaurant will prepare the food 
- When the food is ready PacDriver will pick up the food and deliver it to customers
- Customers receive their orders and pay the orders via cash

![image](https://github.com/user-attachments/assets/acb26c75-1378-4b08-9292-ebf2f8bbaf4f)

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
| user | To store detailed information about users who use Pacman service|
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
| **user**                   | - user_id : int                   | Store unique id for each user                                     | Primary Key (PK)    |
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
|                            | - order_id : varchar (225)        | Store unique id of each order related an order detail             |                     | 
|                            | - food_id : varchar (225)         | Store unique id of food related to order detail                   |                     | 
|                            | - qty : varchar (225)             | Store qty of food that ordered by user                            |                     | 
|                            | - is_like : varchar (225)         | Store information whether user like/dislike the food being ordered|                     |
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
| user                  |            |            |          |                   |                   |              |              | 1:N          |                  |                  |
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

![image](https://github.com/user-attachments/assets/165048cc-8766-4e94-8388-57f89c04c41b)


### Business Rules and Constraints


| Table Name                 | Business Rules                                                         | Constraints                                                                   |
| -------------              | -------------                                                          | -----------------                                                             |
| **city**                   | primary key is not auto increment                                      |                                                                               |
| **order_status**           | primary key is auto increment                                          | order_status_id type : serial                                                 |
| **restaurant**             | information in table restaurant must complete                          | NOT NULL for below fields: name, email, phone_number, address, city_id, coordinate, password                                                  |
|                            | primary key is auto increment                                          | restaurant_id type : serial                                                 |
| **food**                   | information in table foods must complete, except description           | NOL NULL for below fields: restaurant_id, food_name, price, description, availibity                                                    |      
|                            | primary key is auto increment                                          | food_id type : serial                                                       |
|                            | price should be more than 0                                            | CHECK in field price >= 0                                                   |
|                            | Value for default_availibity is TRUE                                   | Availibility DEFAULT TRUE                                                   |
| **user**                   | information in table user must complete, except last name              | NOT NULL for below fields: username, first_name, email, phone, address, city_id, coordinate, password                                          |
|                            | primary key is auto increment                                          | user_id type : Serial                                                       |
|                            | - primary key is auto increment                                        |                                                                               |
|                            | - primary key is auto increment                                        |                                                                               |
|                            | - primary key is auto increment                                        |                                                                               |
|                            | - primary key is auto increment                                        |                                                                               |
|                            | - primary key is auto increment                                        |                                                                               |
|                            | - primary key is auto increment                                        |                                                                               |
