# SQL Practice Problems - by Sylvia Moestl Vasilik

## Intermediate Problems

**20. For this problem, we’d like to see the total number of products in each category. Sort the results by the total number of products, in descending order.**
```SQL
SELECT
	CategoryName,
	COUNT(ProductID) AS TotalProducts
FROM Products p
LEFT JOIN Categories c
	ON p.CategoryID = c.CategoryID
GROUP BY CategoryName
ORDER BY TotalProducts DESC
```
**Result:**

| CategoryName   | TotalProducts |
|----------------|---------------|
| Confections    | 13            |
| Beverages      | 12            |
| Condiments     | 12            |
| Seafood        | 12            |
| Dairy Products | 10            |
| Grains/Cereals | 7             |
| Meat/Poultry   | 6             |
| Produce        | 5             |

**21. In the Customers table, show the total number of customers per Country and City.**
```SQL
SELECT
	Country,
	City,
	COUNT(CustomerID) AS TotalCustomers
FROM Customers
GROUP BY Country, City
ORDER BY TotalCustomers DESC
```
**Result:**

| Country     | City            | TotalCustomers |
|-------------|-----------------|----------------|
| UK          | London          | 6              |
| Mexico      | México D.F.     | 5              |
| Brazil      | Sao Paulo       | 4              |
| Brazil      | Rio de Janeiro  | 3              |
| Spain       | Madrid          | 3              |
| Argentina   | Buenos Aires    | 3              |
| France      | Paris           | 2              |
| USA         | Portland        | 2              |
| France      | Nantes          | 2              |
| Portugal    | Lisboa          | 2              |
| Finland     | Oulu            | 1              |
| Italy       | Reggio Emilia   | 1              |
| France      | Reims           | 1              |
| Brazil      | Resende         | 1              |
| Austria     | Salzburg        | 1              |
| Venezuela   | San Cristóbal   | 1              |
| USA         | San Francisco   | 1              |
| USA         | Seattle         | 1              |
| Spain       | Sevilla         | 1              |
| Norway      | Stavern         | 1              |
| France      | Strasbourg      | 1              |
| Germany     | Stuttgart       | 1              |
| Italy       | Torino          | 1              |
| France      | Toulouse        | 1              |
| Canada      | Tsawassen       | 1              |
| Canada      | Vancouver       | 1              |
| France      | Versailles      | 1              |
| USA         | Walla Walla     | 1              |
| Poland      | Warszawa        | 1              |
| USA         | Butte           | 1              |
| Brazil      | Campinas        | 1              |
| Venezuela   | Caracas         | 1              |
| Belgium     | Charleroi       | 1              |
| Ireland     | Cork            | 1              |
| UK          | Cowes           | 1              |
| Germany     | Cunewalde       | 1              |
| USA         | Elgin           | 1              |
| USA         | Eugene          | 1              |
| Germany     | Frankfurt a.M.  | 1              |
| Switzerland | Genève          | 1              |
| Austria     | Graz            | 1              |
| Finland     | Helsinki        | 1              |
| Venezuela   | I. de Margarita | 1              |
| USA         | Kirkland        | 1              |
| Denmark     | Kobenhavn       | 1              |
| Germany     | Köln            | 1              |
| USA         | Lander          | 1              |
| Germany     | Leipzig         | 1              |
| France      | Lille           | 1              |
| Germany     | Mannheim        | 1              |
| France      | Marseille       | 1              |
| Sweden      | Luleå           | 1              |
| France      | Lyon            | 1              |
| Canada      | Montréal        | 1              |
| Germany     | München         | 1              |
| Germany     | Münster         | 1              |
| Germany     | Aachen          | 1              |
| USA         | Albuquerque     | 1              |
| USA         | Anchorage       | 1              |
| Denmark     | Århus           | 1              |
| Spain       | Barcelona       | 1              |
| Venezuela   | Barquisimeto    | 1              |
| Italy       | Bergamo         | 1              |
| Germany     | Berlin          | 1              |
| Switzerland | Bern            | 1              |
| USA         | Boise           | 1              |
| Sweden      | Bräcke          | 1              |
| Germany     | Brandenburg     | 1              |
| Belgium     | Bruxelles       | 1              |

**22. What products do we have in our inventory that should be reordered? Order the results by ProductID.**
```SQL
SELECT
	ProductID,
	ProductName,
	UnitsInStock,
	ReorderLevel
FROM Products
WHERE UnitsInStock < ReorderLevel
ORDER BY ProductID
```
**Result:**

| ProductID | ProductName               | UnitsInStock | ReorderLevel |
|-----------|---------------------------|--------------|--------------|
| 2         | Chang                     | 17           | 25           |
| 3         | Aniseed Syrup             | 13           | 25           |
| 11        | Queso Cabrales            | 22           | 30           |
| 21        | Sir Rodney's Scones       | 3            | 5            |
| 30        | Nord-Ost Matjeshering     | 10           | 15           |
| 31        | Gorgonzola Telino         | 0            | 20           |
| 32        | Mascarpone Fabioli        | 9            | 25           |
| 37        | Gravad lax                | 11           | 25           |
| 43        | Ipoh Coffee               | 17           | 25           |
| 45        | Rogede sild               | 5            | 15           |
| 48        | Chocolade                 | 15           | 25           |
| 49        | Maxilaku                  | 10           | 15           |
| 56        | Gnocchi di nonna Alice    | 21           | 30           |
| 64        | Wimmers gute Semmelknödel | 22           | 30           |
| 66        | Louisiana Hot Spiced Okra | 4            | 20           |
| 68        | Scottish Longbreads       | 6            | 15           |
| 70        | Outback Lager             | 15           | 30           |
| 74        | Longlife Tofu             | 4            | 5            |

**23. Now we need to incorporate these fields—UnitsInStock, UnitsOnOrder, ReorderLevel,Discontinued—into our calculation. We’ll define “products that need reordering” with the following: UnitsInStock plus UnitsOnOrder are less than or equal to ReorderLevel; The Discontinued flag is false (0).**
```SQL
SELECT
	ProductID,
	ProductName,
	UnitsInStock,
	UnitsOnOrder,
	ReorderLevel,
	Discontinued
FROM Products
WHERE (UnitsInStock + UnitsOnOrder) <= ReorderLevel AND Discontinued = 0
```
**Result:**

| ProductID | ProductName           | UnitsInStock | UnitsOnOrder | ReorderLevel | Discontinued |
|-----------|-----------------------|--------------|--------------|--------------|--------------|
| 30        | Nord-Ost Matjeshering | 10           | 0            | 15           | 0            |
| 70        | Outback Lager         | 15           | 10           | 30           | 0            |

**24.  A salesperson for Northwind is going on a business trip to visit customers, and would like to see a list of all customers, sorted by region, alphabetically. However, he wants the customers with no region (null in the Region field) to be at the end, within the same region, companies should be sorted by CustomerID.**
```SQL
SELECT TOP(10)
	CustomerID,
	CompanyName,
	Region
FROM Customers
ORDER BY 
	CASE 
        WHEN Region IS NULL THEN 1
        ELSE 0
	END, Region, CustomerID
```
**Result:**

91 rows affeted

| CustomerID | CompanyName                   | Region        |
|------------|-------------------------------|---------------|
| OLDWO      | Old World Delicatessen        | AK            |
| BOTTM      | Bottom-Dollar Markets         | BC            |
| LAUGB      | Laughing Bacchus Wine Cellars | BC            |
| LETSS      | Let's Stop N Shop             | CA            |
| HUNGO      | Hungry Owl All-Night Grocers  | Co. Cork      |
| GROSR      | GROSELLA-Restaurante          | DF            |
| SAVEA      | Save-a-lot Markets            | ID            |
| ISLAT      | Island Trading                | Isle of Wight |
| LILAS      | LILA-Supermercado             | Lara          |
| THECR      | The Cracker Box               | MT            |

**25.  Return the three ship countries with the highest average freight overall, in descending order by average freight.**
```SQL
SELECT TOP(3)
	ShipCountry,
	ROUND(AVG(Freight), 2) AS AvgFreight
FROM Orders
GROUP BY ShipCountry
ORDER BY AvgFreight DESC
```
**Result:**

| ShipCountry | AvgFreight |
|-------------|------------|
| Austria     | 184,79     |
| Ireland     | 145,01     |
| USA         | 112,88     |

**26.  We're continuing on the question above on high freight charges. Now, instead of using all the orders we have, we only want to see orders from the year 2015.**
```SQL
SELECT TOP(3)
	ShipCountry,
	YEAR(OrderDate) AS OrderYear,
	ROUND(AVG(Freight), 2) AS AvgFreight
FROM Orders
WHERE YEAR(OrderDate) = 2015
GROUP BY ShipCountry, YEAR(OrderDate)
ORDER BY AvgFreight DESC
```
**Result:**

| ShipCountry | OrderYear | AvgFreight |
|-------------|-----------|------------|
| Austria     | 2015      | 178,36     |
| Switzerland | 2015      | 117,18     |
| France      | 2015      | 113,99     |

**27.  What is the OrderID of the order that the (incorrect) answer is missing**
```SQL
SELECT TOP(3)
	ShipCountry,
	AVG(freight) AS AvgFreight,
	MAX(Freight) AS MaxFreight,
	MIN(Freight) AS MinFreight,
	YEAR(OrderDate) AS OrderYear
FROM Orders
WHERE YEAR(OrderDate) = 2015
GROUP BY ShipCountry, YEAR(OrderDate)
ORDER BY MaxFreight DESC
```
**Result:**

| ShipCountry | AvgFreight | MaxFreight | MinFreight | OrderYear |
|-------------|------------|------------|------------|-----------|
| France      | 113,991    | 2000,00    | 0,87       | 2015      |
| Germany     | 97,3835    | 1007,64    | 0,15       | 2015      |
| Austria     | 178,3642   | 789,95     | 5,29       | 2015      |

```SQL
SELECT
	OrderID,
	Freight
FROM Orders
WHERE Freight = 2000
```
**Result:**

| OrderID | OrderDate               | Freight |
|---------|-------------------------|---------|
| 10806   | 2015-12-31 11:00:00.000 | 2000,00 |

**28.  Check the high freight charges using the last 12 months of order data**
```SQL
SELECT TOP(3)
	ShipCountry,
	AVG(Freight) AS AvgFreight
FROM Orders
WHERE OrderDate >= DATEADD(YEAR, -1, (SELECT Max(OrderDate) FROM Orders))
GROUP BY ShipCountry
ORDER BY AvgFreight DESC
```
**Result:**

| ShipCountry | AvgFreight |
|-------------|------------|
| Ireland     | 200,21     |
| Austria     | 186,4596   |
| USA         | 119,3032   |

**29.  We're doing inventory, and need to show information like the below, for all orders. Sort by OrderID and Product ID.**
```SQL
SELECT TOP(10)
	o.EmployeeID,
	e.LastName,
	o.OrderID,
	p.ProductName,
	d.Quantity
FROM Orders o
LEFT JOIN Employees e
	ON	o.EmployeeID = e.EmployeeID
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Products p
	ON d.ProductID = p.ProductID
ORDER BY o.OrderID, d.ProductID
```
**Result:**

2155 rows affected

| EmployeeID | LastName  | OrderID | ProductName                      | Quantity |
|------------|-----------|---------|----------------------------------|----------|
| 5          | Buchanan  | 10248   | Queso Cabrales                   | 12       |
| 5          | Buchanan  | 10248   | Singaporean Hokkien Fried Mee    | 10       |
| 5          | Buchanan  | 10248   | Mozzarella di Giovanni           | 5        |
| 6          | Suyama    | 10249   | Tofu                             | 9        |
| 6          | Suyama    | 10249   | Manjimup Dried Apples            | 40       |
| 4          | Peacock   | 10250   | Jack's New England Clam Chowder  | 10       |
| 4          | Peacock   | 10250   | Manjimup Dried Apples            | 35       |
| 4          | Peacock   | 10250   | Louisiana Fiery Hot Pepper Sauce | 15       |
| 3          | Leverling | 10251   | Gustaf's Knäckebröd              | 6        |
| 3          | Leverling | 10251   | Ravioli Angelo                   | 15       |

**30.  There are some customers who have never actually placed an order. Show these customers.**
```SQL
SELECT
	c.CustomerID,
	o.CustomerID
FROM Customers c
LEFT JOIN Orders o
	ON c.CustomerID = o.CustomerID
WHERE O.CustomerID IS NULL
```
**Result:**

| CustomerID | CustomerID |
|------------|------------|
| FISSA      | NULL       |
| PARIS      | NULL       |

**31.  One employee (Margaret Peacock, EmployeeID 4) has placed the most orders. However, there are some customers who've never placed an order with her. Show only those customers who have never placed an order with her.**
```SQL
SELECT
	c.CustomerID,
	o.CustomerID
FROM Customers c
LEFT JOIN Orders o
	ON c.CustomerID = o.CustomerID AND o.EmployeeID = 4
WHERE o.CustomerID IS NULL
```
**Result:**

| CustomerID | CustomerID |
|------------|------------|
| SEVES      | NULL       |
| THEBI      | NULL       |
| LAZYK      | NULL       |
| GROSR      | NULL       |
| PARIS      | NULL       |
| FISSA      | NULL       |
| SPECD      | NULL       |
| LAUGB      | NULL       |
| PRINI      | NULL       |
| VINET      | NULL       |
| FRANR      | NULL       |
| CONSH      | NULL       |
| NORTS      | NULL       |
| PERIC      | NULL       |
| DUMON      | NULL       |
| SANTG      | NULL       |

