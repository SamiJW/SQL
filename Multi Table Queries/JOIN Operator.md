## Use the JOIN operator to address the business task of an online bookstore

## Business Task
The executive team would like some insight on the customer base including ordering patterns, best-sellers, and sales. 

### Entity Relationship Diagram
<img width="819" height="997" alt="BookstoreERD drawio" src="https://github.com/user-attachments/assets/aad93ad0-9e1d-4636-8674-7e8791f5ae5d" />



**1. What is the total amount each customer has spent on book purchases?**

````sql
SELECT 
    c.customer_id,
    SUM(oi.unit_price * oi.quantity) AS total_spent
FROM customers c
JOIN orders o 
    ON c.customer_id = o.customer_id
JOIN order_items oi 
    ON o.order_nbr = oi.order_nbr
GROUP BY c.customer_id
ORDER BY total_spent DESC;
````
#### Results
| customer_id | total_spent |
| :---------: | :---------: |
| 355         | 200         |
| 185         | 128         |
| 312         | 78          |
| 869         | 62          |
| 426         | 51          |
| 288         | 27          |
| 508         | 17          |

#### Hm.. I think we could make these results more interesting. Let's add a column for the length of time each customer has had an account with the company.
````sql
SELECT 
    c.customer_id,
    ROUND(MONTHS_BETWEEN(TO_DATE('2025-08-31','yyyy-mm-dd'),c.account_opened)/12,2) AS customer_tenure_years,
    SUM(oi.unit_price * oi.quantity) AS total_spent
FROM customers c 
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN order_items oi
    ON o.order_nbr = oi.order_nbr
GROUP BY c.customer_id, c.account_opened
ORDER BY total_spent DESC;
````
#### Results
| customer_id | customer_tenure_years | total_spent | 
| :---------: | :-------------------: | :---------: |
| 355         | 1.25                  | 200         |
| 185         | 3.16                  | 128         |
| 312         | 2.41                  | 78          |
| 869         | 1.03                  | 62          |
| 426         | 2.03                  | 51          |
| 288         | 2.22                  | 27          |
| 508         | 4.77                  | 17          |


**2. How many orders has each customer placed?**
````sql
SELECT 
    c.customer_id,
    COUNT(DISTINCT(o.order_nbr)) AS orders_placed
FROM customers c
JOIN orders o 
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id
ORDER BY orders_placed DESC;
````
#### Results
| customer_id | orders_placed |
| :---------: | :-----------: |
| 185         | 4             |
| 869         | 3             |
| 288         | 2             |
| 508         | 2             |
| 355         | 1             |
| 426         | 1             |
| 312         | 1             |

**3. What is the sales volume of each book?**
````sql
SELECT 
    b.book_title,
    SUM(oi.quantity) AS quantity_sold
FROM order_items oi
JOIN books b 
    ON oi.book_id = b.book_id
GROUP BY b.book_title
ORDER BY quantity_sold DESC;
````
#### Results
<img width="859" height="481" alt="image" src="https://github.com/user-attachments/assets/75e427bb-6771-464b-b6ee-fa963488d88a" />
  
   

**Tip:** Notice I did not include the Book ID value but instead chose to return the Book Title. This is due to the audience to which this information is being presented. Recall this is the executive team we are addressing with our solutions. 
We should refrain from presenting too much data to keep decisions prioritized and unburdened.     
Had this been the marketing team looking to target demographics based on purchase history/ patterns, the Book ID value would hold much more utility and relevance. 

