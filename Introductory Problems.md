# SQL Practice Problems - by Sylvia Moestl Vasilik

## Introductory Problems

**1. Which shippers do we have?**
```SQL
SELECT 
	*	
FROM Shippers
```
**Result:**

| ShipperID | CompanyName      | Phone          |
|-----------|------------------|----------------|
| 1         | Speedy Express   | (503) 555-9831 |
| 2         | United Package   | (503) 555-3199 |
| 3         | Federal Shipping | (503) 555-9931 |

**2. In the Categories table, select only the columns, CategoryName and Description.**
```SQL
SELECT
	CategoryName,
	Description
FROM Categories
```
**Result:**

| CategoryName   | Description                                                |
|----------------|------------------------------------------------------------|
| Beverages      | Soft drinks, coffees, teas, beers, and ales                |
| Condiments     | Sweet and savory sauces, relishes, spreads, and seasonings |
| Confections    | Desserts, candies, and sweet breads                        |
| Dairy Products | Cheeses                                                    |
| Grains/Cereals | Breads, crackers, pasta, and cereal                        |
| Meat/Poultry   | Prepared meats                                             |
| Produce        | Dried fruit and bean curd                                  |
| Seafood        | Seaweed and fish                                           |

**3. We’d like to see just the FirstName, LastName, and HireDate of all the employees with the Title of Sales Representative.**
```SQL
SELECT
	FirstName,
	LastName,
	HireDate
FROM Employees
WHERE Title = 'Sales Representative'
```
**Result:**

| FirstName | LastName  | HireDate                |
|-----------|-----------|-------------------------|
| Nancy     | Davolio   | 2010-05-01 00:00:00.000 |
| Janet     | Leverling | 2010-04-01 00:00:00.000 |
| Margaret  | Peacock   | 2011-05-03 00:00:00.000 |
| Michael   | Suyama    | 2011-10-17 00:00:00.000 |
| Robert    | King      | 2012-01-02 00:00:00.000 |
| Anne      | Dodsworth | 2012-11-15 00:00:00.000 |

**4. we’d like to see the same columns as above, but only for those employees that both have the title of Sales Representative, and also are in the United States.**
```SQL
SELECT
	FirstName,
	LastName,
	HireDate
FROM Employees
WHERE Title = 'Sales Representative' AND Country = 'USA'
```
**Result:**

| FirstName | LastName  | HireDate                |
|-----------|-----------|-------------------------|
| Nancy     | Davolio   | 2010-05-01 00:00:00.000 |
| Janet     | Leverling | 2010-04-01 00:00:00.000 |
| Margaret  | Peacock   | 2011-05-03 00:00:00.000 |

**5. Show all the orders placed by the employee Steven Buchanan, who's ID is 5**
```SQL
SELECT
	OrderID,
	OrderDate
FROM Orders
WHERE EmployeeID = 5
```
**Result:**

| OrderID | OrderDate               |
|---------|-------------------------|
| 10248   | 2014-07-04 08:00:00.000 |
| 10254   | 2014-07-11 02:00:00.000 |
| 10269   | 2014-07-31 00:00:00.000 |
| 10297   | 2014-09-04 21:00:00.000 |
| 10320   | 2014-10-03 12:00:00.000 |
| 10333   | 2014-10-18 18:00:00.000 |
| 10358   | 2014-11-20 05:00:00.000 |
| 10359   | 2014-11-21 14:00:00.000 |
| 10372   | 2014-12-04 10:00:00.000 |
| 10378   | 2014-12-10 00:00:00.000 |
| 10397   | 2014-12-27 17:00:00.000 |
| 10463   | 2015-03-04 13:00:00.000 |
| 10474   | 2015-03-13 16:00:00.000 |
| 10477   | 2015-03-17 02:00:00.000 |
| 10529   | 2015-05-07 01:00:00.000 |
| 10549   | 2015-05-27 03:00:00.000 |
| 10569   | 2015-06-16 15:00:00.000 |
| 10575   | 2015-06-20 22:00:00.000 |
| 10607   | 2015-07-22 09:00:00.000 |
| 10648   | 2015-08-28 22:00:00.000 |
| 10649   | 2015-08-28 00:00:00.000 |
| 10650   | 2015-08-29 06:00:00.000 |
| 10654   | 2015-09-02 07:00:00.000 |
| 10675   | 2015-09-19 06:00:00.000 |
| 10711   | 2015-10-21 03:00:00.000 |
| 10714   | 2015-10-22 03:00:00.000 |
| 10721   | 2015-10-29 08:00:00.000 |
| 10730   | 2015-11-05 07:00:00.000 |
| 10761   | 2015-12-02 08:00:00.000 |
| 10812   | 2016-01-02 02:00:00.000 |
| 10823   | 2016-01-09 17:00:00.000 |
| 10841   | 2016-01-20 21:00:00.000 |
| 10851   | 2016-01-26 00:00:00.000 |
| 10866   | 2016-02-03 01:00:00.000 |
| 10869   | 2016-02-04 09:00:00.000 |
| 10870   | 2016-02-04 12:00:00.000 |
| 10872   | 2016-02-05 06:00:00.000 |
| 10874   | 2016-02-06 14:00:00.000 |
| 10899   | 2016-02-20 09:00:00.000 |
| 10922   | 2016-03-03 02:00:00.000 |
| 10954   | 2016-03-17 16:00:00.000 |
| 11043   | 2016-04-22 17:00:00.000 |

**6. In the Suppliers table, show the SupplierID, ContactName, and ContactTitle for those Suppliers whose ContactTitle is not Marketing Manager.**
```SQL
SELECT
	SupplierID,
	ContactName,
	ContactTitle
FROM Suppliers
WHERE ContactTitle != 'Marketing Manager'
```
**Result:**

| SupplierID | ContactName                | ContactTitle                 |
|------------|----------------------------|------------------------------|
| 1          | Charlotte Cooper           | Purchasing Manager           |
| 2          | Shelley Burke              | Order Administrator          |
| 3          | Regina Murphy              | Sales Representative         |
| 5          | Antonio del Valle Saavedra | Export Administrator         |
| 6          | Mayumi Ohno                | Marketing Representative     |
| 8          | Peter Wilson               | Sales Representative         |
| 9          | Lars Peterson              | Sales Agent                  |
| 11         | Petra Winkler              | Sales Manager                |
| 12         | Martin Bein                | International Marketing Mgr. |
| 13         | Sven Petersen              | Coordinator Foreign Markets  |
| 14         | Elio Rossi                 | Sales Representative         |
| 16         | Cheryl Saylor              | Regional Account Rep.        |
| 17         | Michael Björn              | Sales Representative         |
| 18         | Guylène Nodier             | Sales Manager                |
| 19         | Robb Merchant              | Wholesale Account Agent      |
| 20         | Chandra Leka               | Owner                        |
| 21         | Niels Petersen             | Sales Manager                |
| 22         | Dirk Luchte                | Accounting Manager           |
| 23         | Anne Heikkonen             | Product Manager              |
| 24         | Wendy Mackenzie            | Sales Representative         |
| 26         | Giovanni Giudici           | Order Administrator          |
| 27         | Marie Delamare             | Sales Manager                |
| 28         | Eliane Noz                 | Sales Representative         |
| 29         | Chantal Goulet             | Accounting Manager           |

**7. In the products table, we’d like to see the ProductID and ProductName for those products where the ProductName includes the string “queso”.**
```SQL
SELECT
	ProductID,
	ProductName
FROM Products
WHERE ProductName LIKE '%queso%'
```
**Result:**

| ProductID | ProductName               |
|-----------|---------------------------|
| 11        | Queso Cabrales            |
| 12        | Queso Manchego La Pastora |

**8. Write a query that shows the OrderID, CustomerID, and ShipCountry for the orders where the ShipCountry is either France or Belgium.**
```SQL
SELECT top(10)
	OrderID,
	CustomerID,
	ShipCountry
FROM Orders
WHERE ShipCountry = 'France' OR ShipCountry = 'Belgium'
```
**Result:**

The result generates 96 rows, so I decided to only show the first 10 rows.

| OrderID | CustomerID | ShipCountry |
|---------|------------|-------------|
| 10248   | VINET      | France      |
| 10251   | VICTE      | France      |
| 10252   | SUPRD      | Belgium     |
| 10265   | BLONP      | France      |
| 10274   | VINET      | France      |
| 10295   | VINET      | France      |
| 10297   | BLONP      | France      |
| 10302   | SUPRD      | Belgium     |
| 10311   | DUMON      | France      |
| 10331   | BONAP      | France      |


**9. Orders shipping to any country in Latin America (Brazil, Mexico, Argentina, Venezuela).**
```SQL
SELECT TOP(10)
	OrderID,
	CustomerID,
	ShipCountry
FROM Orders
WHERE ShipCountry IN ('Brazil', 'Mexico', 'Argentina', 'Venezuela')
```
**Result:**

The result generates 173 rows, so I decided to only show the first 10 rows.

| OrderID | CustomerID | ShipCountry |
|---------|------------|-------------|
| 10250   | HANAR      | Brazil      |
| 10253   | HANAR      | Brazil      |
| 10256   | WELLI      | Brazil      |
| 10257   | HILAA      | Venezuela   |
| 10259   | CENTC      | Mexico      |
| 10261   | QUEDE      | Brazil      |
| 10268   | GROSR      | Venezuela   |
| 10276   | TORTU      | Mexico      |
| 10283   | LILAS      | Venezuela   |
| 10287   | RICAR      | Brazil      |

**10. For all the employees in the Employees table, show the FirstName, LastName, Title, and BirthDate. Order the results by BirthDate, so we have the oldest employees first.**
```SQL
SELECT
	FirstName,
	LastName,
	Title,
	BirthDate
FROM Employees
ORDER BY BirthDate
```
**Result:**

| FirstName | LastName  | Title                    | BirthDate               |
|-----------|-----------|--------------------------|-------------------------|
| Margaret  | Peacock   | Sales Representative     | 1955-09-19 00:00:00.000 |
| Nancy     | Davolio   | Sales Representative     | 1966-12-08 00:00:00.000 |
| Andrew    | Fuller    | Vice President, Sales    | 1970-02-19 00:00:00.000 |
| Steven    | Buchanan  | Sales Manager            | 1973-03-04 00:00:00.000 |
| Laura     | Callahan  | Inside Sales Coordinator | 1976-01-09 00:00:00.000 |
| Robert    | King      | Sales Representative     | 1978-05-29 00:00:00.000 |
| Michael   | Suyama    | Sales Representative     | 1981-07-02 00:00:00.000 |
| Janet     | Leverling | Sales Representative     | 1981-08-30 00:00:00.000 |
| Anne      | Dodsworth | Sales Representative     | 1984-01-27 00:00:00.000 |

**11. In the output of the query above, showing the Employees in order of BirthDate, we see the time of the BirthDate field, which we don’t want. Show only the date portion of the BirthDate field.**
```SQL
SELECT
	FirstName,
	LastName,
	Title,
	CAST (BirthDate AS DATE) AS BirthDate
FROM Employees
ORDER BY BirthDate
```
**Result:**

| FirstName | LastName  | Title                    | BirthDate  |
|-----------|-----------|--------------------------|------------|
| Margaret  | Peacock   | Sales Representative     | 1955-09-19 |
| Nancy     | Davolio   | Sales Representative     | 1966-12-08 |
| Andrew    | Fuller    | Vice President, Sales    | 1970-02-19 |
| Steven    | Buchanan  | Sales Manager            | 1973-03-04 |
| Laura     | Callahan  | Inside Sales Coordinator | 1976-01-09 |
| Robert    | King      | Sales Representative     | 1978-05-29 |
| Michael   | Suyama    | Sales Representative     | 1981-07-02 |
| Janet     | Leverling | Sales Representative     | 1981-08-30 |
| Anne      | Dodsworth | Sales Representative     | 1984-01-27 |

**12. Show the FirstName and LastName columns from the Employees table, and then create a new column called FullName.**
```SQL
SELECT
	FirstName,
	LastName,
	CONCAT(FirstName, ' ', LastName) AS FullName
FROM Employees
```
**Result:**

| FirstName | LastName  | FullName         |
|-----------|-----------|------------------|
| Nancy     | Davolio   | Nancy Davolio    |
| Andrew    | Fuller    | Andrew Fuller    |
| Janet     | Leverling | Janet Leverling  |
| Margaret  | Peacock   | Margaret Peacock |
| Steven    | Buchanan  | Steven Buchanan  |
| Michael   | Suyama    | Michael Suyama   |
| Robert    | King      | Robert King      |
| Laura     | Callahan  | Laura Callahan   |
| Anne      | Dodsworth | Anne Dodsworth   |

**13. In the OrderDetails table, we have the fields UnitPrice and Quantity. Create a new field, TotalPrice. In addition, show the OrderID, ProductID, UnitPrice,
and Quantity. Order by OrderID and ProductID.**
```SQL
SELECT TOP(10)
	OrderID,
	ProductID,
	UnitPrice,
	Quantity,
	(UnitPrice * Quantity) AS TotalPrice
FROM OrderDetails
ORDER BY OrderID, ProductID
```
**Result:**

The result generates 2155 rows, so I decided to only show the first 10 rows.

| OrderID | ProductID | UnitPrice | Quantity | TotalPrice |
|---------|-----------|-----------|----------|------------|
| 10248   | 11        | 14,00     | 12       | 168,00     |
| 10248   | 42        | 9,80      | 10       | 98,00      |
| 10248   | 72        | 34,80     | 5        | 174,00     |
| 10249   | 14        | 18,60     | 9        | 167,40     |
| 10249   | 51        | 42,40     | 40       | 1696,00    |
| 10250   | 41        | 7,70      | 10       | 77,00      |
| 10250   | 51        | 42,40     | 35       | 1484,00    |
| 10250   | 65        | 16,80     | 15       | 252,00     |
| 10251   | 22        | 16,80     | 6        | 100,80     |
| 10251   | 57        | 15,60     | 15       | 234,00     |

**14. How many customers do we have in the Customers table?**
```SQL
SELECT
	COUNT(DISTINCT CustomerID) AS TotalCustomers
FROM Customers
```
**Result:**

| TotalCustomers |
|----------------|
| 91             |

**15. Show the date of the first order ever made in the Orders table.**
```SQL
SELECT
	MIN(OrderDate) AS FirstOrderDate
FROM Orders
```
**Result:**

| FirstOrderDate          |
|-------------------------|
| 2014-07-04 08:00:00.000 |

**16. Show a list of countries where the Northwind company has customers.**
```SQL
SELECT
	DISTINCT Country
FROM Customers
```
**Result:**

| Country     |
|-------------|
| Argentina   |
| Austria     |
| Belgium     |
| Brazil      |
| Canada      |
| Denmark     |
| Finland     |
| France      |
| Germany     |
| Ireland     |
| Italy       |
| Mexico      |
| Norway      |
| Poland      |
| Portugal    |
| Spain       |
| Sweden      |
| Switzerland |
| UK          |
| USA         |
| Venezuela   |

**17. Show a list of all the different values in the Customers table for ContactTitles. Also include a count for each ContactTitle.**
```SQL
SELECT
	ContactTitle,
	COUNT(ContactTitle) AS Total
FROM Customers
GROUP BY ContactTitle
ORDER BY Total DESC
```
**Result:**

| ContactTitle                   | Total |
|--------------------------------|-------|
| Owner                          | 17    |
| Sales Representative           | 17    |
| Marketing Manager              | 12    |
| Sales Manager                  | 11    |
| Accounting Manager             | 10    |
| Sales Associate                | 7     |
| Marketing Assistant            | 6     |
| Sales Agent                    | 5     |
| Assistant Sales Agent          | 2     |
| Order Administrator            | 2     |
| Assistant Sales Representative | 1     |
| Owner/Marketing Assistant      | 1     |

**18. We’d like to show, for each product, the associated Supplier. Show the ProductID, ProductName, and the CompanyName of the Supplier. Sort by ProductID.**
```SQL
SELECT TOP(10)
	ProductID,
	ProductName,
	CompanyName
FROM Products p
LEFT JOIN Suppliers s
	ON p.SupplierID = s.SupplierID
```
**Result:**

The result generates 77 rows, so I decided to only show the first 10 rows.

| ProductID | ProductName                     | CompanyName                |
|-----------|---------------------------------|----------------------------|
| 1         | Chai                            | Exotic Liquids             |
| 2         | Chang                           | Exotic Liquids             |
| 3         | Aniseed Syrup                   | Exotic Liquids             |
| 4         | Chef Anton's Cajun Seasoning    | New Orleans Cajun Delights |
| 5         | Chef Anton's Gumbo Mix          | New Orleans Cajun Delights |
| 6         | Grandma's Boysenberry Spread    | Grandma Kelly's Homestead  |
| 7         | Uncle Bob's Organic Dried Pears | Grandma Kelly's Homestead  |
| 8         | Northwoods Cranberry Sauce      | Grandma Kelly's Homestead  |
| 9         | Mishi Kobe Niku                 | Tokyo Traders              |
| 10        | Ikura                           | Tokyo Traders              |

**19. We’d like to show a list of the Orders that were made, including the Shipper that was used. Show the OrderID, OrderDate (date only), and CompanyName of the Shipper, and sort by OrderID. In order to not show all the orders (there’s more than 800), show only those rows with an OrderID of less than 10300.**
```SQL
SELECT TOP(10)
	OrderID,
	CONVERT(date, OrderDate) AS OrderDate,
	CompanyName
FROM Orders o
LEFT JOIN Shippers s
	ON o.ShipVia = s.ShipperID
WHERE OrderID < 10300
```
**Result:**

The result generates 52 rows, so I decided to only show the first 10 rows.

| OrderID | OrderDate  | CompanyName      |
|---------|------------|------------------|
| 10248   | 2014-07-04 | Federal Shipping |
| 10249   | 2014-07-05 | Speedy Express   |
| 10250   | 2014-07-08 | United Package   |
| 10251   | 2014-07-08 | Speedy Express   |
| 10252   | 2014-07-09 | United Package   |
| 10253   | 2014-07-10 | United Package   |
| 10254   | 2014-07-11 | United Package   |
| 10255   | 2014-07-12 | Federal Shipping |
| 10256   | 2014-07-15 | United Package   |
| 10257   | 2014-07-16 | Federal Shipping |




























