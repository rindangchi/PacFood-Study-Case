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
| driver | Tostore detailed information about driver who partnered with PacFood | 

- Identify tables based on features and limitations
  - Restaurant, userm and drivers only domicile in Indonesia --> need to create validation table to store data about cities in Indonesia
  - Drivers can update their coordinates --> need to create table that can store coordinate logs
  - Each restaurant has at least one menu --> need to create table that store menu data

| Table Name  | Description   |
| ------------- | ------------- |
| city | To store name of city in Indonesia|
| driver_coordinate | To store logs of driver coordinate position|
| food | To store food data sold by restaurants | 
  




