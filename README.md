####DB creation - Values input###

create database ecommerce_db;

USE ecommerce_db;

CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    city VARCHAR(50)
);

CREATE TABLE Categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(100) NOT NULL
);

CREATE TABLE Suppliers (
    supplier_id INT PRIMARY KEY,
    supplier_name VARCHAR(100) NOT NULL
);

CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL
);

CREATE TABLE Shippers (
    shipper_id INT PRIMARY KEY,
    shipper_name VARCHAR(100) NOT NULL
);

CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    category_id INT,
    supplier_id INT,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (category_id)
        REFERENCES Categories(category_id),
    FOREIGN KEY (supplier_id)
        REFERENCES Suppliers(supplier_id)
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    employee_id INT,
    shipper_id INT,
    order_date DATE NOT NULL,
    FOREIGN KEY (customer_id)
        REFERENCES Customers(customer_id),
    FOREIGN KEY (employee_id)
        REFERENCES Employees(employee_id),
    FOREIGN KEY (shipper_id)
        REFERENCES Shippers(shipper_id)
);

CREATE TABLE Order_Items (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id)
        REFERENCES Orders(order_id),
    FOREIGN KEY (product_id)
        REFERENCES Products(product_id)
);

 
USE ecommerce_db;

-- 1. CUSTOMERS
INSERT INTO Customers VALUES
(1, 'Umas', 'umas@email.com', 'Chennai'),
(2, 'Kathir', 'kathir@email.com', 'Bengaluru'),
(3, 'Ashok', 'ashok@email.com', 'Hyderabad'),
(4, 'Adhav', 'adhav@email.com', 'Chennai'),
(5, 'Kanmani', 'kanmani@email.com', 'Mumbai');


-- 2. CATEGORIES
INSERT INTO Categories VALUES
(1, 'Electronics'),
(2, 'Furniture'),
(3, 'Clothing'),
(4, 'Books'),
(5, 'Toys');


-- 3. SUPPLIERS
INSERT INTO Suppliers VALUES
(1, 'TechWorld'),
(2, 'HomeStyle'),
(3, 'FashionHub'),
(4, 'BookMart'),
(5, 'EmptySupplier');


-- 4. EMPLOYEES
INSERT INTO Employees VALUES
(1, 'Arun'),
(2, 'Divya'),
(3, 'Suresh');


-- 5. SHIPPERS
INSERT INTO Shippers VALUES
(1, 'BlueDart'),
(2, 'Delhivery'),
(3, 'India Post');


-- 6. PRODUCTS
INSERT INTO Products VALUES
(101, 'Laptop', 1, 1, 60000.00),
(102, 'Mouse', 1, 1, 800.00),
(103, 'Keyboard', 1, 1, 1500.00),
(104, 'Office Chair', 2, 2, 8000.00),
(105, 'Desk', 2, 2, 12000.00),
(106, 'T-Shirt', 3, 3, 700.00),
(107, 'Jeans', 3, 3, 1800.00),
(108, 'SQL Book', 4, 4, 500.00),
(109, 'Toy Car', 5, NULL, 400.00),
(110, 'Monitor', 1, 1, 15000.00);


-- 7. ORDERS
INSERT INTO Orders VALUES
(1001, 1, 1, 1, '2026-01-10'),
(1002, 1, 2, 2, '2026-01-15'),
(1003, 2, 1, 1, '2026-02-05'),
(1004, 3, 3, 2, '2026-02-20'),
(1005, 4, 2, 1, '2026-03-12'),
(1006, 2, 1, 3, '2026-03-20');


-- 8. ORDER ITEMS
INSERT INTO Order_Items VALUES
(1001, 101, 1, 58000.00),
(1001, 102, 2, 750.00),
(1001, 103, 1, 1400.00),
(1002, 104, 2, 7800.00),
(1002, 106, 3, 650.00),
(1003, 101, 1, 57000.00),
(1003, 108, 2, 450.00),
(1004, 105, 1, 11500.00),
(1004, 107, 2, 1700.00),
(1005, 102, 1, 800.00),
(1005, 106, 2, 700.00),
(1006, 101, 1, 60000.00),
(1006, 104, 1, 8000.00);

SELECT * FROM Customers;
SELECT * FROM Orders;
SELECT * FROM Products;
SELECT * FROM Order_Items;

