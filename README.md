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

Based om the Pacfood business overview and business model that has been described in section "Case Desciprtion", the mission statements of PacFood Delivery are described below:

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
  - Users enable to place orders from restaurant --> need a table to store order information
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

| Table Name      | Fields : data type                | Field Description                                                 | Key                 |
| -------------   | -------------                     | -----------------                                                 |-------------        |
| **city**        | - city_id   : int                 | Store unique id for each city                                     | Primary Key (PK)    |
|                 | - name : varchar (225)            | Store restaurant'sname                                            |                     |
| **restaurant**  | - restaurant_id : int             | Store unique id for each restaurant                               | Primary Key (PK)    |
|                 | - name : varchar (225)            | Store restaurant name                                             |                     |
|                 | - email : varchar (225)           | Store email address of restaurant                                 |                     |
|                 | - phone_number : varchar (20)     | Store phone number of restaurant                                  |                     |
|                 | - address : text                  | Store information about address of restaurant                     |                     |
|                 | - city_id : int                   | Store information about city where the restaurant is located      |                     |
|                 | - coordinate : point              | Store coordinate location of the restaurant                       |                     |
|                 | - password : varchar (225)        | Store password information of the restaurant's account            |                     |    
| **food**        | - food_id : int                   | Store unique id for each food                                     |                     |
|                 | - restaurant_id : int             | Store unique id for each restaurant                               |                     |
|                 | - food_name : varchar (225)       | Store information about the food name                             |                     |
|                 | - price : numeric                 | Store information about the food's price                          |                     |

<span style="color:blue">This is a blue text description.</span>

