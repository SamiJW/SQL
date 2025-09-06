## How many customers in our database are from each state?
````sql
select 
    distinct("STATE") as customer_state,
    count(customer_id) as per_state
from customers
group by "STATE"
order by "STATE" ASC;
````

### Results:
| customer_state | per_state |
| :------------: | :-------: |
| California     | 4         |
| Deleware       | 1         |
| Florida        | 4         |
| Louisiana      | 1         |
| Maryland       | 1         |
| Nevada         | 1         |
| New Jersey     | 1         |
| North Carolina | 1         |
| Oklahoma       | 1         |
| Oregon         | 1         |
| Texas          | 1         |
| Virginia       | 2         |
