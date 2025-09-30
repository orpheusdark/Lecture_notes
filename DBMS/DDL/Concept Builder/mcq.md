## Question 1
**Which SQL query is used to insert multiple records into the `Employee` table?**

**Correct Answer:**
```sql
INSERT INTO Employee (Emp_name, Street, City) VALUES 
('Adam', 'Spring', 'Pittsfield'), 
('Brooks', 'Senator', 'Brooklyn');
````

---

## Question 2

**Which SQL statement will create a table `Employee` with columns `Emp_name`, `Street`, and `City`?**

**Correct Answer:**

```sql
CREATE TABLE Employee (
    Emp_name VARCHAR2(30),
    Street VARCHAR2(30),
    City VARCHAR2(30)
);
```

---

## Question 3

**What SQL statement is used to insert a new employee into the `Employee` table?**

**Correct Answer:**

```sql
INSERT INTO Employee (Emp_name, Street, City) 
VALUES ('Adam', 'Spring', 'Pittsfield');
```

---

## Question 4

**Which SQL statement will create a table `Products` with `Product_id`, `Product_name`, and `Price`?**

**Correct Answer:**

```sql
CREATE TABLE Products (
    Product_id NUMBER,
    Product_name VARCHAR2(50),
    Price NUMBER
);
```

---

## Question 5

**Which SQL statement will insert multiple rows into the `Orders` table?**

**Correct Answer:**

```sql
INSERT INTO Orders (Order_id, Customer_id, Order_date) VALUES 
(1, 101, '2023-01-01'), 
(2, 102, '2023-01-02');
```

---

## Question 6

**Which SQL statement will create a `Customers` table with `Customer_id`, `Customer_name`, and `Email`?**

**Correct Answer:**

```sql
CREATE TABLE Customers (
    Customer_id NUMBER,
    Customer_name VARCHAR2(50),
    Email VARCHAR2(100)
);
```

---

## Question 7

**What SQL statement will create a `Suppliers` table with `Supplier_id` NUMBER, `Supplier_name` VARCHAR2(50), and `Contact_number` VARCHAR2(15)?**

**Correct Answer:**

```sql
CREATE TABLE Suppliers (
    Supplier_id NUMBER,
    Supplier_name VARCHAR2(50),
    Contact_number VARCHAR2(15)
);
```

---

## Question 8

**Which SQL query will create a table `Orders` with `Order_id`, `Customer_id`, and `Order_date`?**

**Correct Answer:**

```sql
CREATE TABLE Orders (
    Order_id NUMBER,
    Customer_id NUMBER,
    Order_date DATE
);
```

---

## Question 9

**What is the correct SQL syntax to insert data into the `Products` table?**

**Correct Answer:**

```sql
INSERT INTO Products (Product_id, Product_name, Price) 
VALUES (101, 'Laptop', 899.99);
```

---

## Question 10

**What SQL statement will insert a new row with `Customer_id`, `Customer_name`, and `Email` into the `Customers` table?**

**Correct Answer:**

```sql
INSERT INTO Customers (Customer_id, Customer_name, Email) 
VALUES (1, 'John Doe', 'john.doe@example.com');
```



