## 1. Provide a list of customers and their addresses.
````sql
SELECT 
    first_name || ' ' || last_name AS customer_name, 
    street_address || ' ' || city || ', ' || "STATE" || ' ' || zip_code AS customer_address
FROM customers 
ORDER BY customer_name ASC;
````
Since State is a reserved keyword, it was necessary to use delimiters "" on the column name along with minding case sensitivity.   
Customer names are ascending in alphabetical order.

### Results: 
<img width="587" height="481" alt="image" src="https://github.com/user-attachments/assets/aac3001b-96d6-4030-9834-030cc0b0bd07" />   
   
***   
   
## 2. Provide a list of employees and their managers.
````sql
SELECT 
    e.first_name || ' ' || e.last_name AS employee_name,
    m.first_name || ' ' || m.last_name AS manager_name
FROM employees m 
JOIN employees e    
    ON e.manager_id = m.employee_id
ORDER BY employee_name ASC;
````
### Results:
<img width="282" height="337" alt="image" src="https://github.com/user-attachments/assets/aac9afc5-33d8-4185-86aa-ba4de1a10b06" />
