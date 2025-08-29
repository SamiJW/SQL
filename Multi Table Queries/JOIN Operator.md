## Use the JOIN operator to address the business task of an online bookstore

## Business Task
The executive team would like some insight on the customer base including ordering patterns, best-sellers, and sales. 

### Entity Relationship Diagram
<img width="820" height="997" alt="BookstoreERD drawio" src="https://github.com/user-attachments/assets/77551ebc-0302-4971-bc75-8841cd3bc5dc" />


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
| :---------- | ----------: |
| 355         | 200         |
| 185         | 128         |
| 312         | 78          |
| 869         | 62          |
| 426         | 51          |
| 288         | 27          |
| 508         | 17          |

| Header 1 | Header 2 | Header 3 |
| :------- | :------: | -------: |
| Data A1  | Data B1  | Data C1  |
| Data A2  | Data B2  | Data C2  |
