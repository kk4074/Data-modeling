# Data-modeling

Data modeling is the process of creating a visual representation of data and its relationships in a database or information system. Data modeling helps users understand the data they have, how it is organized, and how it can be used. Data modeling also helps developers design and implement efficient and reliable data solutions.

There are different types of data models, such as conceptual, logical, and physical, that vary in their level of abstraction and detail. Conceptual models provide a high-level overview of the main data entities and their relationships. Logical models specify the attributes, keys, and constraints of each data entity and their relationships. Physical models describe how the data is stored and accessed in a specific database system.


--------------------------------------------------- Companies Data models are as below ------------------------------------------------

Book my Show:

Movie data (Dimension)
1)	Movie id
2)	Movie name
3)	Genre id 
4)	Release date
5)	Language id
   
Customer data (Dimension)
1)	Customer id
2)	Customer name
3)	Joining date
4)	Location id
   
Cast data (Dimension)
1)	Actor/actress id
2)	Actor/actress name
3)	Debut date
   
Theatre details (Dimension)
1)	Theatre id
2)	Theatre name
3)	Theatre location id 
4)	Theatre capacity
5)	Establishment date
6)	Ticket price of theatre
7)	No of shows per day
8)	Seating capacity
   
Genre details (Dimension)
1)	Genre id
2)	Genre name
   
Language details (Dimension)
1)	Language id
2)	Language name
   
Location details (Dimension)
1)	Location id
2)	Location Name
   
Date ( Dimension)
1)	Date id
2)	Day of the month
3)	Month of the year 
4)	Year
5)	Day of the week
   
Booking (Fact)
1)	Booking id (PK)
2)	Customer id (FK)
3)	Location id (FK)
4)	Theatre id (FK)
5)	Movie id (FK)
6)	SPORTS_EVENT ID (FK)
7)	Concert_id (FK)
8)	Play_id (FK)
9)	Booking date id (FK)
10)	Amount 
11)	Number of tickets
12)	TME

SQL queries be like :

1.	The most popular movie genres in specific locations.
Ans :  booking table join genre id and group by genre id and get the total number of tickets booked  and rank them according to the total number of tickets booked 
Select Sum(Amount) as collections, genre name from booking bk left join movie m on (movie id) left join genre g on (genre id) group by genre id  order by collections
2.	The busiest time of the day/week for movie bookings.
Ans : select count(day_of_the_week)  from (select booking date id , Day of the week from booking left join date d on (booking date id) ) group by day_of_the_week

3.	The percentage of customers who book tickets for other events (like plays or concerts) after booking movie tickets.
Ans. Select CUSTOMER_ID from booking ba inner join booking bb on (booking date id ) and (ba.time_of_booking < bb.time_of_booking) groupby customer_id

4.	The average number of tickets booked per transaction.
Ans. Select sum(number_of_tickets)/count (*) from booking b group by 


ZOMATO/ SWIGGY :

Restaurants (Dimension)
1)	Restaurant id
2)	Restaurant name
3)	Location_id
4)	Cuisine
5)	Year_of_establishment
Customers (Dimension)
1)	Customer id
2)	Customer name
3)	Language_id
4)	Age
5)	Location_id
6)	Sign up date
Dishes (Dimension)
1)	Dish id
2)	Dish name
3)	Dish type
Locations (Dimension)
1)	Location_id(Pk)
2)	City_id(Fk)
3)	Location_name
4)	Latitude
5)	Longitude
Cities(dimension)
1)	City_id(Pk)
2)	City_name
3)	State
4)	Country
Dates(Dimension)
1)	Date_time(PK)
2)	DAY
3)	MONTH
4)	YEAR
5)	WEEKDAY
ORDERS(fact)
1)	Order_id(pk)
2)	Customer_id(fk)
3)	Date_time(fk)
4)	Location_id(fk)
5)	Delivery status
6)	Dish_id(fk)
7)	Restaurant_id(fk)
8)	Cancelation_status
9)	Amount
10)	Delivered_time
11)	Delivery_partner_id(Fk)


SQL  queris be like:

1)	The most popular restaurants in specific locations
Ans : select restaurant_name from restaurant_details where restaurant_id in (select count(order_id) , restaurant_id from orders where order_date between 1/12/2023 and 1/1/2024 group by location_id,restaurant_id  )

2)	The busiest times of day/week for food orders
       Ans : Select day_of_week,count(day_of_week) from orders  left join date_time group by day_of_week

3)	  The average order value for each customer
Ans.  Select  customer_id , sum(amount) /count(order_id) from orders group by customers 

4)	The average delivery time for each restaurant and/or delivery personnel.
Ans. select delivery_person_id , sum(delivery_time)/count(order_id) from orders group by delivery_person_id 

5)	The most commonly ordered cuisines
Ans. select cuisine , count(orders) CO from orders inner join restaurants on (restaurant_id) group by cuisine order by CO desc
