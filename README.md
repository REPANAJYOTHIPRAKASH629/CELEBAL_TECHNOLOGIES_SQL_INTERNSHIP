# CELEBAL_TECHNOLOGIES_SQL_INTERNS

<strong>Level A Task</strong>

CT_CSI_SQ_771
R. JYOTHI PRAKASH


1. List of all customers

```
SELECT * FROM Customers;
```


2. list of all customers where company name ending in N

```
SELECT * FROM Customers

WHERE CompanyName LIKE '%N';
```


3. list of all customers who live in Berlin or London

```
SELECT * FROM Customers

WHERE City IN ('Berlin', 'London');
```


4. list of all customers who live in UK or USA

```
SELECT * FROM Customers

WHERE Country IN ('UK', 'USA');
```


5. list of all products sorted by product name

```
SELECT * FROM Products

ORDER BY ProductName;
```


6. list of all products where product name starts with an A

```
SELECT * FROM Products

WHERE ProductName LIKE 'A%';
```



7. List of customers who ever placed an order

```
SELECT DISTINCT Customers.*

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```



8. list of Customers who live in London and have bought chai

```
SELECT DISTINCT Customers.*

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

JOIN Products ON OrderDetails.ProductID = Products.ProductID

WHERE Customers.City = 'London' AND Products.ProductName = 'Chai';
```


9. List of customers who never place an order

```
SELECT * FROM Customers

WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);
```


10. List of customers who ordered Tofu

```
SELECT DISTINCT Customers.*

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

JOIN Products ON OrderDetails.ProductID = Products.ProductID

WHERE Products.ProductName = 'Tofu';
```



11. Details of first order of the system

```
SELECT * FROM Orders

ORDER BY OrderDate

LIMIT 1;
```



12. Find the details of most expensive order date

```
SELECT Orders.OrderID, Orders.OrderDate, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalAmount

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY Orders.OrderID, Orders.OrderDate

ORDER BY TotalAmount DESC

LIMIT 1;
```

13. For each order get the OrderID and Average quantity of items in that order

```
SELECT OrderID, AVG(Quantity) AS AvgQuantity

FROM OrderDetails

GROUP BY OrderID;
```


14. For each order get the orderID, minimum quantity and maximum quantity for that order

```
SELECT OrderID, MIN(Quantity) AS MinQuantity, MAX(Quantity) AS MaxQuantity

FROM OrderDetails

GROUP BY OrderID;
```



15. Get a list of all managers and total number of employees who report to them.

```
SELECT ManagerID, COUNT(*) AS NumberOfReports

FROM Employees

WHERE ManagerID IS NOT NULL

GROUP BY ManagerID;
```


16. Get the OrderID and the total quantity for each order that has a total quantity of greater than 300
```
SELECT OrderID, SUM(Quantity) AS TotalQuantity

FROM OrderDetails

GROUP BY OrderID

HAVING TotalQuantity > 300;
```


17. list of all orders placed on or after 1996/12/31
```
SELECT * FROM Orders

WHERE OrderDate >= '1996-12-31';
```


18. list of all orders shipped to Canada
```
SELECT * FROM Orders

WHERE ShipCountry = 'Canada';
```


19. list of all orders with order total > 200
    
```
SELECT Orders.OrderID, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalAmount

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY Orders.OrderID

HAVING TotalAmount > 200;
```


20. List of countries and sales made in each country

```
SELECT ShipCountry, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalSales

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY ShipCountry;
```


21. List of Customer ContactName and number of orders they placed

```
SELECT Customers.ContactName, COUNT(Orders.OrderID) AS NumberOfOrders

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID

GROUP BY Customers.ContactName;
```


22. List of customer contactnames who have placed more than 3 orders

```
SELECT Customers.ContactName

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID

GROUP BY Customers.ContactName

HAVING COUNT(Orders.OrderID) > 3;
```


23. List of discontinued products which were ordered between 1/1/1997 and 1/1/1998

```
SELECT DISTINCT Products.*

FROM Products

JOIN OrderDetails ON Products.ProductID = OrderDetails.ProductID

JOIN Orders ON OrderDetails.OrderID = Orders.OrderID

WHERE Products.Discontinued = 1

  AND Orders.OrderDate BETWEEN '1997-01-01' AND '1998-01-01';
```


24. List of employee firsname, lastName, superviser FirstName, LastName

```
SELECT e.FirstName AS EmployeeFirstName, e.LastName AS EmployeeLastName,

       s.FirstName AS SupervisorFirstName, s.LastName AS SupervisorLastName

FROM Employees e

LEFT JOIN Employees s ON e.ManagerID = s.EmployeeID;
```


25. List of Employees id and total sale condcuted by employee

```
SELECT Orders.EmployeeID, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalSales

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY Orders.EmployeeID;
```


26. list of employees whose FirstName contains character a

```
SELECT * FROM Employees

WHERE FirstName LIKE '%a%';
```


27. List of managers who have more than four people reporting to them.

```
SELECT ManagerID

FROM Employees

GROUP BY ManagerID

HAVING COUNT(*) > 4;
```


28. List of Orders and ProductNames29. List of orders place by the best customer

```
SELECT Orders.OrderID, Products.ProductName

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

JOIN Products ON OrderDetails.ProductID = Products.ProductID;
```


30. List of orders placed by customers who do not have a Fax number

```
SELECT Orders.*

FROM Orders

JOIN Customers ON Orders.CustomerID = Customers.CustomerID

WHERE Customers.Fax IS NULL;
```


31. List of Postal codes where the product Tofu was shipped

```
SELECT DISTINCT Orders.ShipPostalCode

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

JOIN Products ON OrderDetails.ProductID = Products.ProductID

WHERE Products.ProductName = 'Tofu';
```


32. List of product Names that were shipped to France

```
SELECT DISTINCT Products.ProductName

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

JOIN Products ON OrderDetails.ProductID = Products.ProductID

WHERE Orders.ShipCountry = 'France';
```


33. List of ProductNames and Categories for the supplier 'Specialty Biscuits, Ltd.

```
SELECT Products.ProductName, Categories.CategoryName

FROM Products

JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID

JOIN Categories ON Products.CategoryID = Categories.CategoryID

WHERE Suppliers.CompanyName = 'Specialty Biscuits, Ltd.';
```


34. List of products that were never ordered

```
SELECT * FROM Products

WHERE ProductID NOT IN (SELECT DISTINCT ProductID FROM OrderDetails);
```


35. List of products where units in stock is less than 10 and units on order are 0.

```
SELECT * FROM Products

WHERE UnitsInStock < 10 AND UnitsOnOrder = 0;
```


36. List of top 10 countries by sales

```
SELECT ShipCountry, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalSales

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY ShipCountry

ORDER BY TotalSales DESC

LIMIT 10;
```


37. Number of orders each employee has taken for customers with CustomerIDs between A and AO

```
SELECT Orders.EmployeeID, COUNT(*) AS NumberOfOrders

FROM Orders

JOIN Customers ON Orders.CustomerID = Customers.CustomerID

WHERE Customers.CustomerID BETWEEN 'A' AND 'AO'

GROUP BY Orders.EmployeeID;
```


38. Orderdate of most expensive order

```
SELECT Orders.OrderDate

FROM Orders

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY Orders.OrderID, Orders.OrderDate

ORDER BY SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) DESC

LIMIT 1;
```

39. Product name and total revenue from that product

```
SELECT Products.ProductName, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalRevenue

FROM Products

JOIN OrderDetails ON Products.ProductID = OrderDetails.ProductID

GROUP BY Products.ProductName;
```


40. Supplierid and number of products offered

```
SELECT SupplierID, COUNT(*) AS NumberOfProducts

FROM Products

GROUP BY SupplierID;
```

41. Top ten customers based on their business

```
SELECT Customers.CustomerID, SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalSpending

FROM Customers

JOIN Orders ON Customers.CustomerID = Orders.CustomerID

JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID

GROUP BY Customers.CustomerID

ORDER BY TotalSpending DESC

LIMIT 10;
```



42. What is the total revenue of the company.

```
SELECT SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS TotalRevenue

FROM OrderDetails;
```

<hr></hr>
<hr></hr>

**-- Level B Task**

**-- procedures**
-----------------------

-- Create a procedure InsertOrderDetails that takes OrderID, ProductID, UnitPrice, Quantiy, Discount as input parameters and inserts that order information in the Order Details table. 
-- After each order inserted, check the @@rowcount value to make sure that order was inserted properly. If for any reason the order was not inserted, print the messages Failed to place the
-- order. Please try again. Also your procedure should have these functionalities

-- Make the UnitPrice and Discount parameters optional

-- If no UnitPrice is given, then use the UnitPrice value from the product table.

-- If no Discount is given, then use a discount of 0.

-- Adjust the quantity in stock (UnitsInStock) for the product by subtracting the quantity sold from inventory.

-- However, if there is not enough of a product in stock, then abort the stored procedure without making any changes to the database.

-- Print a message if the quantity in stock of a product drops below its Reorder Level as a result of the update.

```
CREATE PROCEDURE InsertOrderDetails
    @OrderID int,
    @ProductID int = NULL,
    @UnitPrice money = NULL,
    @Quantity int,
    @Discount money = NULL
AS
BEGIN
    SET NOCOUNT ON;

    IF @UnitPrice IS NULL
        SELECT @UnitPrice = UnitPrice FROM Production.Product WHERE ProductID = @ProductID

    IF @Discount IS NULL
        SET @Discount = 0

    BEGIN TRANSACTION
    BEGIN TRY
        INSERT INTO Sales.OrderDetails (OrderID, ProductID, UnitPrice, OrderQty, Discount)
        VALUES (@OrderID, @ProductID, @UnitPrice, @Quantity, @Discount)

        DECLARE @UnitsInStock int = (SELECT UnitsInStock FROM Production.Product WHERE ProductID = @ProductID)
        IF @UnitsInStock < @Quantity
            RAISERROR('Not enough stock', 16, 1)

        UPDATE Production.Product
        SET UnitsInStock = @UnitsInStock - @Quantity
        WHERE ProductID = @ProductID

        IF @@ROWCOUNT = 0
            RAISERROR('Failed to place the order. Please try again.', 16, 1)

        COMMIT TRANSACTION
    END TRY
    BEGIN CATCH
        ROLLBACK TRANSACTION
        RAISERROR('Failed to place the order. Please try again.', 16, 1)
    END CATCH
END
```


-- Create a procedure UpdateOrderDetails that takes OrderID, ProductID, Unit Price, Quantity, and discount, and updates these values for that ProductID in that Order. All the parameters
-- except the OrderID and ProductID should be optional so that if the user wants to only update Quantity s/he should be able to do so without providing the rest of the values. You need 
-- also make sure that if any of the values are being passed in as NULL, then you want to retain the original value instead of overwriting it with NULL. To accomplish this, look for the
-- ISNULL() function in google or sql server books online. Adjust the UnitsInStock value in products table accordingly.

```
CREATE PROCEDURE UpdateOrderDetails
    @OrderID int,
    @ProductID int,
    @UnitPrice money = NULL,
    @Quantity int = NULL,
    @Discount money = NULL
AS
BEGIN
    SET NOCOUNT ON;

    UPDATE Sales.OrderDetails
    SET UnitPrice = ISNULL(UnitPrice, UnitPrice),
        Quantity = ISNULL(Quantity, Quantity),
        Discount = ISNULL(Discount, Discount)
    WHERE OrderID = @OrderID AND ProductID = @ProductID

    UPDATE Production.Product
    SET UnitsInStock = UnitsInStock - (SELECT Quantity FROM Sales.OrderDetails WHERE OrderID = @OrderID AND ProductID = @ProductID)
    WHERE ProductID = @ProductID

    IF @@ROWCOUNT = 0
        RAISERROR('No records found', 16, 1)
END
```


-- Create a procedure GetOrderDetails that takes OrderID as input parameter and returns all the records for that OrderID. If no records are found in Order Details table, then it should
-- print the line: "The OrderID XXXX does not exits", where XXX should be the OrderlD entered by user and the procedure should RETURN the value 1.

```
CREATE PROCEDURE GetOrderDetails
    @OrderID int
AS
BEGIN
    SET NOCOUNT ON;

    IF NOT EXISTS (SELECT 1 FROM Sales.OrderDetails WHERE OrderID = @OrderID)
        PRINT 'The OrderID ' + CONVERT(varchar(10), @OrderID) + ' does not exist'
    ELSE
        SELECT * FROM Sales.OrderDetails WHERE OrderID = @OrderID

    RETURN 1;
END
```


-- Create a procedure DeleteOrderDetails that takes OrderID and ProductID and deletes that from Order Details table. Your procedure should validate parameters. It should retum an error
-- code (-1) and print a message if the parameters are invalid. Parameters are valid if the given order ID appears in the table and if the given product ID appears in that order.

```
CREATE PROCEDURE DeleteOrderDetails
    @OrderID int,
    @ProductID int
AS
BEGIN
    SET NOCOUNT ON;

    IF NOT EXISTS (SELECT 1 FROM Sales.OrderDetails WHERE OrderID = @OrderID AND ProductID = @ProductID)
        RAISERROR('Invalid parameters', -1, 1)
    ELSE
        DELETE FROM Sales.OrderDetails WHERE OrderID = @OrderID AND ProductID = @ProductID

    RETURN 0;
END
```


**-- Functions**
-----------------

-- Review SQL Server date formats on this website and then create following functions

-- http://www.sql-server-helper.com/tips/date-formats.aspx

-- Create a function that takes an input parameter type datetime and returns the date in the format MM/DD/YYYY. For example if I pass in 2006-11-21 23:34:05.920', the output of the
--  functions should be 11/21/2006

```
CREATE FUNCTION FormatDate_MMDDYYYY (@datetime datetime)
RETURNS varchar(10)
AS
BEGIN
    RETURN CONVERT(varchar(10), CONVERT(date, @datetime), 101)
END
```


-- Create a function that takes an input parameter type datetime and returns the date in the fonnat YYYYMMDD

```
CREATE FUNCTION FormatDate_YYYYMMDD (@datetime datetime)
RETURNS varchar(10)
AS
BEGIN
    RETURN CONVERT(varchar(10), CONVERT(date, @datetime), 112)
END
```

**-- Views**
------------------

-- Create a view vwCustomerOrders which returns CompanyName OrderID.OrderDate, ProductID ProductName Quantity UnitPrice.Quantity od. UnitPrice

```
CREATE VIEW vwCustomerOrders AS
SELECT c.CompanyName, od.OrderID, od.OrderDate, p.ProductName, od.Quantity, od.UnitPrice
FROM Sales.OrderDetails od INNER JOIN Products p ON od.ProductID = p.ProductID INNER JOIN Sales.Orders o ON od.OrderID = o.OrderID INNER JOIN Customers c ON o.CustomerID = c.CustomerID
```


-- Create a copy of the above view and modify it so that it only returns the above information for orders that were placed yesterday

```
CREATE VIEW vwCustomerOrders_Yesterday AS
SELECT c.CompanyName, od.OrderID, od.OrderDate, p.ProductName, od.Quantity, od.UnitPrice
FROM Sales.OrderDetails od INNER JOIN Products p ON od.ProductID = p.ProductID INNER JOIN Sales.Orders o ON od.OrderID = o.OrderID INNER JOIN Customers c ON o.CustomerID = c.CustomerID
WHERE CAST(od.OrderDate AS date) = CAST(GETDATE() - 1 AS date)
```

-- Use a CREATE VIEW statement to create a view called MyProducts. Your view should contain the ProductID, ProductName, QuantityPerUnit and Unit Price columns from the Products table. It
-- should also contain the CompanyName column from the Suppliers table and the CategoryName column from the Categories table. Your view should only contain products that are 
-- not discontinued. 

```
CREATE VIEW MyProducts AS
SELECT p.ProductID, p.ProductName, p.QuantityPerUnit, p.UnitPrice, s.CompanyName, c.CategoryName
FROM Products p LEFT JOIN Suppliers s ON p.SupplierID = s.SupplierID LEFT JOIN Categories c ON p.CategoryID = c.CategoryID WHERE p.DiscontinuedDate IS NULL;
```



**-- Triggers**
-------------------

-- If someone cancels an order in northwind database, then you want to delete that order from the Orders table. But you will not be able to delete that Order before deleting the records 
-- from Order Details table for that particular order due to referential integrity constraints. Create an Instead of Delete trigger on Orders table so that if some one tries to delete an
-- Order that trigger gets fired and that trigger should first delete everything in order details table and then delete that order from the Orders table

```
CREATE TRIGGER trg_DeleteOrdersInsteadOfDelete ON Orders INSTEAD OF DELETE AS
BEGIN
    DELETE FROM Sales.OrderDetails WHERE OrderID IN (SELECT OrderID FROM deleted)
    DELETE FROM Orders WHERE OrderId IN (SELECT OrderId FROM deleted)
END
```


-- When an order is placed for X units of product Y, we must first check the Products table to ensure that there is sufficient stock to fill the order. This trigger will operate on the
-- Order Details table. If sufficient stock exists, then fill the order and decrement X units from the UnitsInStock column in Products. If insufficient stock exists, then refuse the order
-- (le. do not insert it) and notify the user that the order could not be filled because of insufficient stock.
 

```
CREATE TRIGGER trg_CheckInventory BEFORE INSERT ON Sales.OrderDetails AS
BEGIN
    IF EXISTS (SELECT 1 FROM Production.Product WHERE ProductId = INSERTED.ProductId AND UnitsInStock < INSERTED.Quantity)
        ROLLBACK TRANSACTION;
END;
```


<strong> Level C Task </strong>

<strong> Task 1 </strong>

```
WITH ProjectGroups AS (
    SELECT
        Task_ID,
        Start_Date,
        End_Date,
        ROW_NUMBER() OVER (ORDER BY Start_Date) - 
        ROW_NUMBER() OVER (PARTITION BY DATEADD(day, -ROW_NUMBER() OVER (ORDER BY Start_Date), Start_Date) ORDER BY Start_Date) AS Project_ID
    FROM Projects
)
SELECT 
    MIN(Start_Date) AS Start_Date,
    MAX(End_Date) AS End_Date,
    DATEDIFF(day, MIN(Start_Date), MAX(End_Date)) + 1 AS Duration
FROM ProjectGroups
GROUP BY Project_ID
ORDER BY Duration, MIN(Start_Date);
```

<strong> Task 2 </strong>

```
SELECT
    s1.Nome AS Student_Name,
    s2.Nome AS Best_Friend_Name,
    p2.Salary AS Best_Friend_Salary
FROM
    Students s1
JOIN
    Friends f ON s1.ID = f.ID
JOIN
    Students s2 ON f.Friend_ID = s2.ID
JOIN
    Packages p1 ON s1.ID = p1.ID
JOIN
    Packages p2 ON s2.ID = p2.ID
WHERE
    p2.Salary > p1.Salary
ORDER BY
    p2.Salary;
```

<strong> Task 3 </strong>

```
SELECT DISTINCT
    f1.X AS X,
    f1.Y AS Y
FROM
    Functions f1
JOIN
    Functions f2 ON f1.X = f2.Y AND f1.Y = f2.X
WHERE
    f1.X < f1.Y
ORDER BY
    f1.X;
```

<strong> Task 4 </strong>

```
SELECT
    c.contest_id,
    c.hacker_id,
    h.name,
    COALESCE(SUM(v.total_views), 0) AS total_views,
    COALESCE(SUM(v.total_unique_views), 0) AS total_unique_views,
    COALESCE(SUM(s.total_submissions), 0) AS total_submissions,
    COALESCE(SUM(s.total_accepted_submissions), 0) AS total_accepted_submissions
FROM
    Contests c
JOIN
    Hackers h ON c.hacker_id = h.hacker_id
JOIN
    Colleges co ON c.contest_id = co.contest_id
JOIN
    Challenges ch ON co.college_id = ch.college_id
LEFT JOIN
    View_Stats v ON ch.challenge_id = v.challenge_id
LEFT JOIN
    Submission_Stats s ON ch.challenge_id = s.challenge_id
GROUP BY
    c.contest_id, c.hacker_id, h.name
HAVING
    SUM(v.total_views) > 0 OR
    SUM(v.total_unique_views) > 0 OR
    SUM(s.total_submissions) > 0 OR
    SUM(s.total_accepted_submissions) > 0
ORDER BY
    c.contest_id;
```

<strong> Task 5 </strong>

```
WITH DateRange AS (
    SELECT DATE '2016-03-01' AS submission_date
    UNION ALL
    SELECT submission_date + INTERVAL '1' DAY
    FROM DateRange
    WHERE submission_date < DATE '2016-03-15'
),
DailySubmissions AS (
    SELECT
        dr.submission_date,
        s.hacker_id,
        COUNT(s.submission_id) AS submissions_count
    FROM
        DateRange dr
    LEFT JOIN
        Submissions s ON dr.submission_date = s.submission_date
    GROUP BY
        dr.submission_date, s.hacker_id
),
UniqueHackers AS (
    SELECT
        submission_date,
        COUNT(DISTINCT hacker_id) AS unique_hackers
    FROM
        DailySubmissions
    GROUP BY
        submission_date
),
MaxSubmissions AS (
    SELECT
        submission_date,
        hacker_id,
        submissions_count
    FROM (
        SELECT
            submission_date,
            hacker_id,
            submissions_count,
            ROW_NUMBER() OVER (PARTITION BY submission_date ORDER BY submissions_count DESC, hacker_id) AS rn
        FROM
            DailySubmissions
    ) AS ranked
    WHERE
        rn = 1
)
SELECT
    u.submission_date,
    u.unique_hackers,
    m.hacker_id,
    h.name,
    m.submissions_count
FROM
    UniqueHackers u
JOIN
    MaxSubmissions m ON u.submission_date = m.submission_date
JOIN
    Hackers h ON m.hacker_id = h.hacker_id
ORDER BY
    u.submission_date;

```

<strong> Task 6 </strong>

```
WITH Points AS (
    SELECT
        MIN(LAT_N) AS min_lat,
        MIN(LONG_W) AS min_long,
        MAX(LAT_N) AS max_lat,
        MAX(LONG_W) AS max_long
    FROM
        STATION
)
SELECT
    ROUND(ABS(min_lat - max_lat) + ABS(min_long - max_long), 4) AS manhattan_distance
FROM
    Points;
```

<strong> Task 7 </strong>

```
WITH RECURSIVE Numbers AS (
    SELECT 2 AS num
    UNION ALL
    SELECT num + 1
    FROM Numbers
    WHERE num < 1000
),
PrimeNumbers AS (
    SELECT num
    FROM Numbers
    WHERE num NOT IN (
        SELECT n.num
        FROM Numbers n
        JOIN Numbers m ON m.num <= SQRT(n.num) AND n.num % m.num = 0 AND m.num > 1
    )
)
SELECT STRING_AGG(CAST(num AS VARCHAR), '&') AS prime_numbers
FROM PrimeNumbers;
```

<strong> Task 8 </strong>

```
WITH OccupationRanks AS (
    SELECT
        Name,
        Occupation,
        ROW_NUMBER() OVER (PARTITION BY Occupation ORDER BY Name) AS row_num
    FROM
        OCCUPATIONS
),
Pivoted AS (
    SELECT
        MAX(CASE WHEN Occupation = 'Doctor' THEN Name END) AS Doctor,
        MAX(CASE WHEN Occupation = 'Professor' THEN Name END) AS Professor,
        MAX(CASE WHEN Occupation = 'Singer' THEN Name END) AS Singer,
        MAX(CASE WHEN Occupation = 'Actor' THEN Name END) AS Actor
    FROM
        OccupationRanks
    GROUP BY
        row_num
)
SELECT
    Doctor,
    Professor,
    Singer,
    Actor
FROM
    Pivoted;
```

<strong> Task 9 </strong>

```
WITH NodeType AS (
    SELECT
        N,
        P,
        CASE
            WHEN P IS NULL THEN 'Root'
            WHEN N NOT IN (SELECT DISTINCT P FROM BST) THEN 'Leaf'
            ELSE 'Inner'
        END AS node_type
    FROM
        BST
)
SELECT
    N,
    node_type
FROM
    NodeType
ORDER BY
    N;
```

<strong> Task 10 </strong>
```
WITH EmployeeCounts AS (
    SELECT
        company_code,
        COUNT(DISTINCT CASE WHEN lead_manager_code IS NOT NULL THEN lead_manager_code END) AS lead_managers_count,
        COUNT(DISTINCT CASE WHEN senior_manager_code IS NOT NULL THEN senior_manager_code END) AS senior_managers_count,
        COUNT(DISTINCT CASE WHEN manager_code IS NOT NULL THEN manager_code END) AS managers_count,
        COUNT(DISTINCT employee_code) AS total_employees_count
    FROM
        Employee
    GROUP BY
        company_code
)
SELECT
    c.company_code,
    c.founder,
    COALESCE(ec.lead_managers_count, 0) AS lead_managers_count,
    COALESCE(ec.senior_managers_count, 0) AS senior_managers_count,
    COALESCE(ec.managers_count, 0) AS managers_count,
    COALESCE(ec.total_employees_count, 0) AS total_employees_count
FROM
    Company c
LEFT JOIN
    EmployeeCounts ec ON c.company_code = ec.company_code
ORDER BY
    c.company_code;
```

<strong> Task 11 </strong>

```
SELECT DISTINCT
    s.Name
FROM
    Students s
JOIN
    Friends f ON s.ID = f.ID
JOIN
    Packages p1 ON f.Friend_ID = p1.ID
JOIN
    Packages p2 ON s.ID = p2.ID
WHERE
    p1.Salary > p2.Salary
ORDER BY
    p1.Salary;
```
<strong> Task 12 </strong>
```
SELECT
    JobFamily,
    Country,
    SUM(CASE WHEN Country = 'India' THEN Cost ELSE 0 END) AS India_Cost,
    SUM(CASE WHEN Country = 'International' THEN Cost ELSE 0 END) AS International_Cost,
    (SUM(CASE WHEN Country = 'India' THEN Cost ELSE 0 END) / NULLIF(SUM(Cost), 0)) * 100 AS India_Percentage,
    (SUM(CASE WHEN Country = 'International' THEN Cost ELSE 0 END) / NULLIF(SUM(Cost), 0)) * 100 AS International_Percentage
FROM
    YourTable
GROUP BY
    JobFamily, Country;

```
<strong> Task 13 </strong>

```
SELECT BU, 
       MONTH, 
       SUM(Cost) AS Total_Cost, 
       SUM(Revenue) AS Total_Revenue, 
       SUM(Cost) / NULLIF(SUM(Revenue), 0) AS Cost_Revenue_Ratio
FROM YourTable
GROUP BY BU, MONTH;

```
<strong> Task 14 </strong>
```
SELECT SubBand, 
       COUNT(EmployeeID) AS Headcount, 
       (COUNT(EmployeeID) / (SELECT COUNT(*) FROM YourTable)) * 100 AS Percentage_Headcount
FROM YourTable
GROUP BY SubBand;
```

<strong> Task 15 </strong>
```
SELECT EmployeeID, Salary
FROM YourTable
FETCH FIRST 5 ROWS ONLY;
```
<strong> Task 16 </strong>
```
UPDATE YourTable
SET Column1 = Column2,
    Column2 = Column1;
```
<strong> Task 17 </strong>
```
CREATE LOGIN prakash WITH PASSWORD = 'jyothiprakash@629';
USE YourDatabaseName;
CREATE USER balaji FOR LOGIN prakash;
ALTER ROLE db_owner ADD MEMBER khizar;
```
<strong> Task 18 </strong>
```
SELECT BU, 
       MONTH, 
       SUM(Cost * EmployeeCount) / SUM(EmployeeCount) AS Weighted_Average_Cost
FROM YourTable
GROUP BY BU, MONTH;
```
<strong> Task 19 </strong>
```
SELECT CEIL(AVG(Salary) - AVG(NULLIF(SUBSTR(Salary, 1, LENGTH(Salary) - 1), 0))) AS Salary_Error
FROM YourTable;
```
<strong> Task 20 </strong>
```
INSERT INTO DestinationTable (Column1, Column2, ...)
SELECT Column1, Column2, ...
FROM SourceTable;
```
