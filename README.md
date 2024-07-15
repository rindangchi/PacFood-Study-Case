# Case Description

## PacFood Business Overview

PacFood is food delivery service in Indonesia which partners with many restaurants in Indonesia. PacFood already has a lot of customers around Indonesia. 

## PacFood Business Model

- Customer choose restaurant in PacFood application then start to order the food
- Restaurant will prepare the food 
- When the food is ready PacDriver will pick up the food and deliver it to customers

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

  


