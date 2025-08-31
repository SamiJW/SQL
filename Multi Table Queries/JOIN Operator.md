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

````
