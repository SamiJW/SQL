## How many states in the US has the customer base reached?
````sql
select 
    count(distinct("STATE")) as customer_state
from customers;
````
### Results:
| customer_state |
| :------------: |
| 12             |
