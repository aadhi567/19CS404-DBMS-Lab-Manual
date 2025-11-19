# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.
```sql
SELECT o.ord_no,
o.purch_amt,
c.cust_name,
c.city
FROM orders o
INNER JOIN customer c
  ON o.customer_id=c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="1200" height="366" alt="image" src="https://github.com/user-attachments/assets/9443fc9f-9a37-4033-bae3-5e991b7b7a61" />


**Question 2**
---
From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission

```sql
SELECT c.cust_name AS "Customer Name",
c.city,
s.name AS Salesman,
s.commission
FROM customer c
INNER JOIN salesman s
  ON c.salesman_id=s.salesman_id;
  
```

**Output:**

<img width="1201" height="762" alt="image" src="https://github.com/user-attachments/assets/6f69a8fb-1085-4447-898d-70025e385472" />


**Question 3**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission

```sql
SELECT c.cust_name AS "Customer Name",
c.city,
s.name AS Salesman,
s.city,
s.commission
FROM customer c
JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE c.city<>s.city AND s.commission>0.12;
```

**Output:**

<img width="1032" height="369" alt="image" src="https://github.com/user-attachments/assets/84e9bfeb-d0d9-4bc9-8802-648516c4eda5" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id) Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT
c.customer_id,
c.cust_name,
c.city,
c.grade,
s.salesman_id
FROM customer c
LEFT JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE s.name="Mc Lyon";
```

**Output:**

<img width="1045" height="217" alt="image" src="https://github.com/user-attachments/assets/7aa7436b-853e-41cd-b5f1-59cc4bb925c5" />


**Question 5**
---
Write an SQL query to select all columns from the 'customer' table (aliased as 'c') by performing a LEFT JOIN with the 'orders' table on the 'customer_id' column, including only those orders where the order date falls between '2012-08-01' and '2012-08-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id) 'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT
c.*
FROM customer c
LEFT JOIN orders o
  ON c.customer_id=o.customer_id
WHERE o.ord_date BETWEEN "2012-08-01" AND "2012-08-30";
```

**Output:**

<img width="1059" height="280" alt="image" src="https://github.com/user-attachments/assets/eeb676e1-601f-4711-a747-c070778e2071" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

```sql
SELECT p.first_name,s.*
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE discharge_date BETWEEN "2024-03-01" AND "2024-03-31";

```

**Output:**

<img width="1065" height="226" alt="image" src="https://github.com/user-attachments/assets/202b3d61-ac0e-49fe-adfa-f7881cc6af0f" />


**Question 7**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

```sql
SELECT p.first_name,s.*
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE p.first_name="Alice";
```

**Output:**

<img width="1061" height="217" alt="image" src="https://github.com/user-attachments/assets/c3eb539e-4f88-49a3-8f20-3991a26ad1c3" />


**Question 8**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id.

```sql
SELECT
c.cust_name,
c.city,
c.grade,
s.name AS Salesman,
s.city
FROM customer c
INNER JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE c.grade<300
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1026" height="462" alt="image" src="https://github.com/user-attachments/assets/d606931c-bc76-415e-baa7-6d10cd1a4ff3" />


**Question 9**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

```sql
SELECT s.name AS Salesman,
c.cust_name,c.city
FROM salesman s
JOIN customer c
  ON s.city=c.city;
```

**Output:**

<img width="685" height="417" alt="image" src="https://github.com/user-attachments/assets/7d639891-8625-4c2b-b3d9-d2e77e75f8c6" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.

```sql
SELECT p.first_name
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE s.surgery_date="2024-01-15";
```

**Output:**

<img width="284" height="217" alt="image" src="https://github.com/user-attachments/assets/dd08791d-504a-498a-8beb-05571849828f" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
