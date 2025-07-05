Drop tables and views if already exist
DROP VIEW IF EXISTS CustomerOrderSummary;
DROP TABLE IF EXISTS Orders;
DROP TABLE IF EXISTS Customers;

Step 1: Create Tables
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name TEXT,
    City TEXT
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    Product TEXT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

 Step 2: Insert Sample Data
INSERT INTO Customers (CustomerID, Name, City) VALUES
(1, 'Alice', 'New York'),
(2, 'Bob', 'Los Angeles'),
(3, 'Charlie', 'Chicago'),
(4, 'Diana', 'Houston');

INSERT INTO Orders (OrderID, CustomerID, Product) VALUES
(101, 1, 'Laptop'),
(102, 2, 'Phone'),
(103, 1, 'Tablet'),
(104, 1, 'Mouse');

 Step 3: Create View (with complex SELECT)
CREATE VIEW CustomerOrderSummary AS
SELECT 
    c.CustomerID,
    c.Name,
    COUNT(o.OrderID) AS TotalOrders
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name;

 Step 4: Use/View the View
SELECT * FROM CustomerOrderSummary;

 Step 5: Filter view data (example usage)
SELECT * FROM CustomerOrderSummary
WHERE TotalOrders > 1;
