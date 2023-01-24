# SQL Practice Problems - by Sylvia Moestl Vasilik

## Advanced Problems

**32. We want to send all of our high-value customers a special VIP gift. We're defining high-value customers as those who've made at least 1 order with a total value (not including the discount) equal to $10,000 or more. We only want to consider orders made in the year 2016.**
```SQL
SELECT
	o.CustomerID,
	c.CompanyName,
	o.OrderID,
	SUM(d.Quantity * d.UnitPrice) AS TotalAmount
FROM Orders o
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Customers C
	ON o.CustomerID = c.CustomerID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName, o.OrderID
HAVING SUM(d.Quantity * d.UnitPrice) > 10000
ORDER BY TotalAmount DESC
```
**Result:**

| CustomerID | CompanyName                  | OrderID | TotalAmount |
|------------|------------------------------|---------|-------------|
| QUICK      | QUICK-Stop                   | 10865   | 17250,00    |
| SAVEA      | Save-a-lot Markets           | 11030   | 16321,90    |
| HANAR      | Hanari Carnes                | 10981   | 15810,00    |
| KOENE      | Königlich Essen              | 10817   | 11490,70    |
| RATTC      | Rattlesnake Canyon Grocery   | 10889   | 11380,00    |
| HUNGO      | Hungry Owl All-Night Grocers | 10897   | 10835,24    |


**33. The manager has changed his mind. Instead of requiring that customers have at least one individual orders totaling $10,000 or more, he wants to define high-value customers as those who have orders totaling $15,000 or more in 2016. How would you change the answer to the problem above?**
```SQL
SELECT
	o.CustomerID,
	c.CompanyName,
	SUM(d.Quantity * d.UnitPrice) AS TotalAmount
FROM Orders o
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Customers C
	ON o.CustomerID = c.CustomerID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName
HAVING SUM(d.Quantity * d.UnitPrice) > 15000
ORDER BY TotalAmount DESC
```
**Result:**

| CustomerID | CompanyName                  | TotalAmount |
|------------|------------------------------|-------------|
| SAVEA      | Save-a-lot Markets           | 42806,25    |
| ERNSH      | Ernst Handel                 | 42598,90    |
| QUICK      | QUICK-Stop                   | 40526,99    |
| HANAR      | Hanari Carnes                | 24238,05    |
| HUNGO      | Hungry Owl All-Night Grocers | 22796,34    |
| RATTC      | Rattlesnake Canyon Grocery   | 21725,60    |
| KOENE      | Königlich Essen              | 20204,95    |
| FOLKO      | Folk och fä HB               | 15973,85    |
| WHITC      | White Clover Markets         | 15278,90    |

**34. Change the above query to use the discount when calculating high-value customers. Order by the total amount which includes the discount.**
```SQL
SELECT
	o.CustomerID,
	c.CompanyName,
	ROUND(SUM(d.Quantity * d.UnitPrice),2) AS TotalWithoutDiscount,
	ROUND(SUM(d.Quantity * d.UnitPrice * (1 - d.Discount)),2) AS TotalWithDiscount
FROM Customers c
LEFT JOIN Orders o
	ON c.CustomerID = o.CustomerID
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName
HAVING SUM(d.Quantity * d.UnitPrice * (1 - d.Discount)) > 10000
ORDER BY TotalWithDiscount DESC
```
**Result:**

| CustomerID | CompanyName                  | TotalWithoutDiscount | TotalWithDiscount |
|------------|------------------------------|----------------------|-------------------|
| ERNSH      | Ernst Handel                 | 42598,90             | 41210,65          |
| QUICK      | QUICK-Stop                   | 40526,99             | 37217,32          |
| SAVEA      | Save-a-lot Markets           | 42806,25             | 36310,11          |
| HANAR      | Hanari Carnes                | 24238,05             | 23821,2           |
| RATTC      | Rattlesnake Canyon Grocery   | 21725,60             | 21238,27          |
| HUNGO      | Hungry Owl All-Night Grocers | 22796,34             | 20402,12          |
| KOENE      | Königlich Essen              | 20204,95             | 19582,77          |
| WHITC      | White Clover Markets         | 15278,90             | 15278,9           |
| FOLKO      | Folk och fä HB               | 15973,85             | 13644,07          |
| SUPRD      | Suprêmes délices             | 11862,50             | 11644,6           |
| BOTTM      | Bottom-Dollar Markets        | 12227,40             | 11338,55          |

**35. At the end of the month, salespeople are likely to try much harder to get orders, to meet their month-end quotas. Show all orders made on the last day of the
month. Order by EmployeeID and OrderID.**
```SQL
SELECT
	EmployeeID,
	OrderID,
	OrderDate
FROM Orders
WHERE OrderDate = EOMONTH(OrderDate )
ORDER BY EmployeeID, OrderID
```
**Result:**

| EmployeeID | OrderID | OrderDate               |
|------------|---------|-------------------------|
| 1          | 10461   | 2015-02-28 00:00:00.000 |
| 1          | 10616   | 2015-07-31 00:00:00.000 |
| 2          | 10583   | 2015-06-30 00:00:00.000 |
| 2          | 10686   | 2015-09-30 00:00:00.000 |
| 2          | 10989   | 2016-03-31 00:00:00.000 |
| 2          | 11060   | 2016-04-30 00:00:00.000 |
| 3          | 10432   | 2015-01-31 00:00:00.000 |
| 3          | 10988   | 2016-03-31 00:00:00.000 |
| 3          | 11063   | 2016-04-30 00:00:00.000 |
| 4          | 10343   | 2014-10-31 00:00:00.000 |
| 4          | 10522   | 2015-04-30 00:00:00.000 |
| 4          | 10584   | 2015-06-30 00:00:00.000 |
| 4          | 10617   | 2015-07-31 00:00:00.000 |
| 4          | 10725   | 2015-10-31 00:00:00.000 |
| 4          | 11061   | 2016-04-30 00:00:00.000 |
| 4          | 11062   | 2016-04-30 00:00:00.000 |
| 5          | 10269   | 2014-07-31 00:00:00.000 |
| 6          | 10317   | 2014-09-30 00:00:00.000 |
| 7          | 10490   | 2015-03-31 00:00:00.000 |
| 8          | 10399   | 2014-12-31 00:00:00.000 |
| 8          | 10460   | 2015-02-28 00:00:00.000 |
| 8          | 10491   | 2015-03-31 00:00:00.000 |
| 8          | 10987   | 2016-03-31 00:00:00.000 |
| 9          | 10687   | 2015-09-30 00:00:00.000 |

**36. The Northwind mobile app developers are testing an app that customers will use to show orders. In order to make sure that even the largest orders will show up correctly on the app, they'd like some samples of orders that have lots of individual line items. Show the 10 orders with the most line items, in order of total line items.**
```SQL
SELECT TOP(10)
	OrderID,
	COUNT(OrderID) AS TotalOrdersByOrderID
FROM OrderDetails
GROUP BY OrderID
ORDER BY COUNT(OrderID) DESC
```
**Result:**

| OrderID | TotalOrdersByOrderID |
|---------|----------------------|
| 11077   | 25                   |
| 10657   | 6                    |
| 10847   | 6                    |
| 10979   | 6                    |
| 10273   | 5                    |
| 10294   | 5                    |
| 10309   | 5                    |
| 10324   | 5                    |
| 10325   | 5                    |
| 10337   | 5                    |

**37. The Northwind mobile app developers would now like to just get a random assortment of orders for beta testing on their app. Show a random set of 2% of all orders.**
```SQL
SELECT TOP 2 PERCENT
	OrderID
FROM Orders
ORDER BY NewID()
```
**Result:**

| OrderID |
|---------|
| 10689   |
| 10403   |
| 10892   |
| 10961   |
| 10757   |
| 10543   |
| 10835   |
| 10641   |
| 10937   |
| 10359   |
| 10701   |
| 10349   |
| 10710   |
| 10913   |
| 10940   |
| 10907   |
| 11037   |

**38. Janet Leverling, one of the salespeople, has come to you with a request. She thinks that she accidentally double-entered a line item on an order, with a different ProductID, but the same quantity. She remembers that the quantity was 60 or more. Show all the OrderIDs with line items that match this, in order of OrderID.**
```SQL
SELECT
	OrderID,
	Quantity
FROM OrderDetails
WHERE Quantity >=60
GROUP BY OrderID, Quantity
HAVING COUNT(*) > 1
```
**Result:**

| OrderID | Quantity |
|---------|----------|
| 10263   | 60       |
| 10263   | 65       |
| 10990   | 65       |
| 10658   | 70       |
| 11030   | 100      |

**39. Based on the previous question, we now want to show details of the order, for orders that match the above criteria.**
```SQL
WITH cte AS(
SELECT
	OrderID,
	Quantity
FROM OrderDetails
WHERE Quantity >=60
GROUP BY OrderID, Quantity
HAVING COUNT(*) > 1
)
SELECT
	OrderID,
	ProductID,
	UnitPrice,
	Quantity,
	Discount
FROM OrderDetails
WHERE OrderID IN (SELECT OrderID FROM cte)
ORDER BY OrderID, Quantity
```
**Result:**

| OrderID | ProductID | UnitPrice | Quantity | Discount |
|---------|-----------|-----------|----------|----------|
| 10263   | 16        | 13,90     | 60       | 0,25     |
| 10263   | 30        | 20,70     | 60       | 0,25     |
| 10263   | 24        | 3,60      | 65       | 0        |
| 10263   | 74        | 8,00      | 65       | 0,25     |
| 10658   | 60        | 34,00     | 55       | 0,05     |
| 10658   | 21        | 10,00     | 60       | 0        |
| 10658   | 40        | 18,40     | 70       | 0,05     |
| 10658   | 77        | 13,00     | 70       | 0,05     |
| 10990   | 34        | 14,00     | 60       | 0,15     |
| 10990   | 21        | 10,00     | 65       | 0        |
| 10990   | 55        | 24,00     | 65       | 0,15     |
| 10990   | 61        | 28,50     | 66       | 0,15     |
| 11030   | 29        | 123,79    | 60       | 0,25     |
| 11030   | 5         | 21,35     | 70       | 0        |
| 11030   | 2         | 19,00     | 100      | 0,25     |
| 11030   | 59        | 55,00     | 100      | 0,25     |


**40. Here's another way of getting the same results as in the previous problem, using a derived table instead of a CTE. However, there's a bug in this SQL. It returns 20 rows instead of 16. Correct the SQL. Problem SQL:**
```SQL
SELECT
	OrderDetails.OrderID,
	ProductID,
	UnitPrice,
	Quantity,
	Discount
FROM OrderDetails
	JOIN(
		SELECT DISTINCT
			OrderID
		FROM OrderDetails
		WHERE Quantity >= 60
		GROUP BY OrderID, Quantity
		HAVING COUNT(*) > 1
	) PotentialProblemOrders
		ON PotentialProblemOrders.OrderID = OrderDetails.OrderID
	ORDER BY OrderID, ProductID
```
**Result:**

| OrderID | ProductID | UnitPrice | Quantity | Discount |
|---------|-----------|-----------|----------|----------|
| 10263   | 16        | 13,90     | 60       | 0,25     |
| 10263   | 24        | 3,60      | 65       | 0        |
| 10263   | 30        | 20,70     | 60       | 0,25     |
| 10263   | 74        | 8,00      | 65       | 0,25     |
| 10658   | 21        | 10,00     | 60       | 0        |
| 10658   | 40        | 18,40     | 70       | 0,05     |
| 10658   | 60        | 34,00     | 55       | 0,05     |
| 10658   | 77        | 13,00     | 70       | 0,05     |
| 10990   | 21        | 10,00     | 65       | 0        |
| 10990   | 34        | 14,00     | 60       | 0,15     |
| 10990   | 55        | 24,00     | 65       | 0,15     |
| 10990   | 61        | 28,50     | 66       | 0,15     |
| 11030   | 2         | 19,00     | 100      | 0,25     |
| 11030   | 5         | 21,35     | 70       | 0        |
| 11030   | 29        | 123,79    | 60       | 0,25     |
| 11030   | 59        | 55,00     | 100      | 0,25     |

Note the Distinct keyword, added after the Select in the derived table. This gives us only distinct rows in the output, which avoids the problem with duplicate OrderIDs.

**41. Some customers are complaining about their orders arriving late. Which orders are late?**
```SQL
SELECT 
	OrderID,
	CAST(OrderDate AS DATE) AS OrderDate,
	CAST(RequiredDate AS DATE) AS RequiredDate,
	CAST(ShippedDate AS DATE) AS ShippedDate
FROM Orders
WHERE ShippedDate >= RequiredDate
ORDER BY OrderID
```
**Result:**

| OrderID | OrderDate  | RequiredDate | ShippedDate |
|---------|------------|--------------|-------------|
| 10264   | 2014-07-24 | 2014-08-21   | 2014-08-23  |
| 10271   | 2014-08-01 | 2014-08-29   | 2014-08-30  |
| 10280   | 2014-08-14 | 2014-09-11   | 2014-09-12  |
| 10302   | 2014-09-10 | 2014-10-08   | 2014-10-09  |
| 10309   | 2014-09-19 | 2014-10-17   | 2014-10-23  |
| 10380   | 2014-12-12 | 2015-01-09   | 2015-01-16  |
| 10423   | 2015-01-23 | 2015-02-06   | 2015-02-24  |
| 10427   | 2015-01-27 | 2015-02-24   | 2015-03-03  |
| 10433   | 2015-02-03 | 2015-03-03   | 2015-03-04  |
| 10451   | 2015-02-19 | 2015-03-05   | 2015-03-12  |
| 10483   | 2015-03-24 | 2015-04-21   | 2015-04-25  |
| 10515   | 2015-04-23 | 2015-05-07   | 2015-05-23  |
| 10523   | 2015-05-01 | 2015-05-29   | 2015-05-30  |
| 10545   | 2015-05-22 | 2015-06-19   | 2015-06-26  |
| 10578   | 2015-06-24 | 2015-07-22   | 2015-07-25  |
| 10593   | 2015-07-09 | 2015-08-06   | 2015-08-13  |
| 10596   | 2015-07-11 | 2015-08-08   | 2015-08-12  |
| 10660   | 2015-09-08 | 2015-10-06   | 2015-10-15  |
| 10663   | 2015-09-10 | 2015-09-24   | 2015-10-03  |
| 10687   | 2015-09-30 | 2015-10-28   | 2015-10-30  |
| 10705   | 2015-10-15 | 2015-11-12   | 2015-11-18  |
| 10709   | 2015-10-17 | 2015-11-14   | 2015-11-20  |
| 10726   | 2015-11-03 | 2015-11-17   | 2015-12-05  |
| 10727   | 2015-11-03 | 2015-12-01   | 2015-12-05  |
| 10749   | 2015-11-20 | 2015-12-18   | 2015-12-19  |
| 10777   | 2015-12-15 | 2015-12-29   | 2016-01-21  |
| 10779   | 2015-12-16 | 2016-01-13   | 2016-01-14  |
| 10788   | 2015-12-22 | 2016-01-19   | 2016-01-19  |
| 10807   | 2015-12-31 | 2016-01-28   | 2016-01-30  |
| 10816   | 2016-01-06 | 2016-02-03   | 2016-02-04  |
| 10827   | 2016-01-12 | 2016-01-26   | 2016-02-06  |
| 10828   | 2016-01-13 | 2016-01-27   | 2016-02-04  |
| 10847   | 2016-01-22 | 2016-02-05   | 2016-02-10  |
| 10924   | 2016-03-04 | 2016-04-01   | 2016-04-08  |
| 10927   | 2016-03-05 | 2016-04-02   | 2016-04-08  |
| 10960   | 2016-03-19 | 2016-04-02   | 2016-04-08  |
| 10970   | 2016-03-24 | 2016-04-07   | 2016-04-24  |
| 10978   | 2016-03-26 | 2016-04-23   | 2016-04-23  |
| 10998   | 2016-04-03 | 2016-04-17   | 2016-04-17  |

**42. Some salespeople have more orders arriving late than others. Maybe they're not following up on the order process, and need more training. Which salespeople have the most orders arriving late?**
```SQL
SELECT 
	o.EmployeeID,
	e.LastName,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders o
JOIN Employees e
	ON o.EmployeeID = e.EmployeeID
WHERE ShippedDate >= RequiredDate
GROUP BY o.EmployeeID, e.LastName
ORDER BY TotalLateOrders DESC
```
**Result:**

| EmployeeID | LastName  | TotalLateOrders |
|------------|-----------|-----------------|
| 4          | Peacock   | 10              |
| 3          | Leverling | 5               |
| 8          | Callahan  | 5               |
| 9          | Dodsworth | 5               |
| 7          | King      | 4               |
| 2          | Fuller    | 4               |
| 1          | Davolio   | 3               |
| 6          | Suyama    | 3               |

**43. Andrew, the VP of sales, has been doing some more thinking about the problem of late orders. He realizes that just looking at the number of orders arriving late for each salesperson isn't a good idea. It needs to be compared against the total number of orders per salesperson.**
```SQL
WITH LateOrders AS(
SELECT 
	o.EmployeeID,
	e.LastName,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders o
JOIN Employees e
	ON o.EmployeeID = e.EmployeeID
WHERE ShippedDate >= RequiredDate
GROUP BY o.EmployeeID, e.LastName
),
TotalOrders AS (
SELECT 
	o.EmployeeID,
	e.LastName,
	COUNT(OrderID) AS TotalOrders
FROM Orders o
JOIN Employees e
	ON o.EmployeeID = e.EmployeeID
GROUP BY o.EmployeeID, e.LastName
)
SELECT
	l.EmployeeID,
	l.LastName,
	t.TotalOrders,
	l.TotalLateOrders
FROM LateOrders l 
JOIN TotalOrders t
	ON l.EmployeeID = t.EmployeeID
```
**Result:**

| EmployeeID | LastName  | TotalOrders | TotalLateOrders |
|------------|-----------|-------------|-----------------|
| 1          | Davolio   | 123         | 3               |
| 2          | Fuller    | 96          | 4               |
| 3          | Leverling | 127         | 5               |
| 4          | Peacock   | 156         | 10              |
| 6          | Suyama    | 67          | 3               |
| 7          | King      | 72          | 4               |
| 8          | Callahan  | 104         | 5               |
| 9          | Dodsworth | 43          | 5               |


**44. There's an employee missing in the answer from the problem above. Fix the SQL to show all employees who have taken orders.**
```SQL
WITH TotalOrders AS (
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY EmployeeID
),
LateOrders AS(
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders
WHERE ShippedDate >= RequiredDate 
GROUP BY EmployeeID
)
SELECT
	t.EmployeeID,
	e.LastName,
	t.TotalOrders,
	l.TotalLateOrders
FROM TotalOrders t
LEFT JOIN LateOrders l
	ON t.EmployeeID = l.EmployeeID
LEFT JOIN Employees e
	ON t.EmployeeID = e.EmployeeID
```
**Result:**

| EmployeeID | LastName  | TotalOrders | TotalLateOrders |
|------------|-----------|-------------|-----------------|
| 1          | Davolio   | 123         | 3               |
| 2          | Fuller    | 96          | 4               |
| 3          | Leverling | 127         | 5               |
| 4          | Peacock   | 156         | 10              |
| 5          | Buchanan  | 42          | NULL            |
| 6          | Suyama    | 67          | 3               |
| 7          | King      | 72          | 4               |
| 8          | Callahan  | 104         | 5               |
| 9          | Dodsworth | 43          | 5               |


**45. Continuing on the answer for above query, let's fix the results for row 5 - Buchanan. He should have a 0 instead of a Null in LateOrders.**
```SQL
WITH TotalOrders AS (
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY EmployeeID
),
LateOrders AS(
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders
WHERE ShippedDate >= RequiredDate 
GROUP BY EmployeeID
)
SELECT
	t.EmployeeID,
	e.LastName,
	t.TotalOrders,
	CASE
		WHEN l.TotalLateOrders IS NULL THEN 0
		ELSE l.TotalLateOrders
	END TotalLateOrders
FROM TotalOrders t
LEFT JOIN LateOrders l
	ON t.EmployeeID = l.EmployeeID
LEFT JOIN Employees e
	ON t.EmployeeID = e.EmployeeID
```
**Result:**

| EmployeeID | LastName  | TotalOrders | TotalLateOrders |
|------------|-----------|-------------|-----------------|
| 1          | Davolio   | 123         | 3               |
| 2          | Fuller    | 96          | 4               |
| 3          | Leverling | 127         | 5               |
| 4          | Peacock   | 156         | 10              |
| 5          | Buchanan  | 42          | 0               |
| 6          | Suyama    | 67          | 3               |
| 7          | King      | 72          | 4               |
| 8          | Callahan  | 104         | 5               |
| 9          | Dodsworth | 43          | 5               |

**46. Now we want to get the percentage of late orders over total orders.**
```SQL
WITH TotalOrders AS (
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY EmployeeID
),
LateOrders AS(
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders
WHERE ShippedDate >= RequiredDate 
GROUP BY EmployeeID
)
SELECT
	t.EmployeeID,
	e.LastName,
	t.TotalOrders,
	CASE
		WHEN l.TotalLateOrders IS NULL THEN 0
		ELSE l.TotalLateOrders
	END TotalLateOrders,
	(IsNull(TotalLateOrders, 0) * 1.00) / TotalOrders AS PercentLateOrders
FROM TotalOrders t
LEFT JOIN LateOrders l
	ON t.EmployeeID = l.EmployeeID
LEFT JOIN Employees e
	ON t.EmployeeID = e.EmployeeID
```
**Result:**

| EmployeeID | LastName  | TotalOrders | TotalLateOrders | PercentLateOrders |
|------------|-----------|-------------|-----------------|-------------------|
| 1          | Davolio   | 123         | 3               | 0.0243902439024   |
| 2          | Fuller    | 96          | 4               | 0.0416666666666   |
| 3          | Leverling | 127         | 5               | 0.0393700787401   |
| 4          | Peacock   | 156         | 10              | 0.0641025641025   |
| 5          | Buchanan  | 42          | 0               | 0.0000000000000   |
| 6          | Suyama    | 67          | 3               | 0.0447761194029   |
| 7          | King      | 72          | 4               | 0.0555555555555   |
| 8          | Callahan  | 104         | 5               | 0.0480769230769   |
| 9          | Dodsworth | 43          | 5               | 0.1162790697674   |

**47. So now for the PercentageLateOrders, we get a decimal value like we should. But to make the output easier to read, let's cut the PercentLateOrders off at 2 digits to the right of the decimal point.**
```SQL
WITH TotalOrders AS (
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY EmployeeID
),
LateOrders AS(
SELECT 
	EmployeeID,
	COUNT(OrderID) AS TotalLateOrders
FROM Orders
WHERE ShippedDate >= RequiredDate 
GROUP BY EmployeeID
)
SELECT
	t.EmployeeID,
	e.LastName,
	t.TotalOrders,
	CASE
		WHEN l.TotalLateOrders IS NULL THEN 0
		ELSE l.TotalLateOrders
	END TotalLateOrders,
	CONVERT(
		DECIMAL(10,2),
			(IsNull(TotalLateOrders, 0) * 1.00) / TotalOrders) AS PercentLateOrders
FROM TotalOrders t
LEFT JOIN LateOrders l
	ON t.EmployeeID = l.EmployeeID
LEFT JOIN Employees e
	ON t.EmployeeID = e.EmployeeID
```
**Result:**

| EmployeeID | LastName  | TotalOrders | TotalLateOrders | PercentLateOrders |
|------------|-----------|-------------|-----------------|-------------------|
| 1          | Davolio   | 123         | 3               | 0.02              |
| 2          | Fuller    | 96          | 4               | 0.04              |
| 3          | Leverling | 127         | 5               | 0.04              |
| 4          | Peacock   | 156         | 10              | 0.06              |
| 5          | Buchanan  | 42          | 0               | 0.00              |
| 6          | Suyama    | 67          | 3               | 0.04              |
| 7          | King      | 72          | 4               | 0.06              |
| 8          | Callahan  | 104         | 5               | 0.05              |
| 9          | Dodsworth | 43          | 5               | 0.12              |

**48. Andrew Fuller, the VP of sales at Northwind, would like to do a sales campaign for existing customers. He'd like to categorize customers into groups, based
on how much they ordered in 2016. Then, depending on which group the customer is in, he will target the customer with different sales materials.
The customer grouping categories are 0 to 1,000, 1,000 to 5,000, 5,000 to 10,000, and over 10,000. Order the results by CustomerID.**
```SQL
WITH cte AS(
SELECT
	o.CustomerID,
	c.CompanyName,
	SUM(d.Quantity * d.UnitPrice) AS TotalAmount
FROM Orders o
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Customers C
	ON o.CustomerID = c.CustomerID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName
)
SELECT TOP(10)
	*,
	CASE
		WHEN TotalAmount <= 1000 THEN 'Low'
		WHEN TotalAmount <= 5000 THEN 'Medium'
		WHEN TotalAmount <= 10000 THEN 'High'
		WHEN TotalAmount > 10000 THEN 'Very High'
		ELSE 'NoGroup'
	END Categories
FROM cte
ORDER BY CustomerID
```
**Result:**

- 81 rows were affeted, showing only the top 10

| CustomerID | CompanyName                        | TotalAmount | Categories |
|------------|------------------------------------|-------------|------------|
| ALFKI      | Alfreds Futterkiste                | 2302,20     | Medium     |
| ANATR      | Ana Trujillo Emparedados y helados | 514,40      | Low        |
| ANTON      | Antonio Moreno Taquería            | 660,00      | Low        |
| AROUT      | Around the Horn                    | 5838,50     | High       |
| BERGS      | Berglunds snabbköp                 | 8110,55     | High       |
| BLAUS      | Blauer See Delikatessen            | 2160,00     | Medium     |
| BLONP      | Blondesddsl père et fils           | 730,00      | Low        |
| BOLID      | Bólido Comidas preparadas          | 280,00      | Low        |
| BONAP      | Bon app'                           | 7185,90     | High       |
| BOTTM      | Bottom-Dollar Markets              | 12227,40    | Very High  |

**50. Based on the above query, show all the defined CustomerGroups, and the percentage in each. Sort by the total in each group, in descending order.**
```SQL
WITH cte AS(
SELECT
	o.CustomerID,
	c.CompanyName,
	SUM(d.Quantity * d.UnitPrice) AS TotalAmount
FROM Orders o
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Customers C
	ON o.CustomerID = c.CustomerID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName
),
GroupCategories AS (
SELECT
	*,
	CASE
		WHEN TotalAmount <= 1000 THEN 'Low'
		WHEN TotalAmount <= 5000 THEN 'Medium'
		WHEN TotalAmount <= 10000 THEN 'High'
		WHEN TotalAmount > 10000 THEN 'Very High'
		ELSE 'NoGroup'
	END Categories
FROM cte
)
SELECT
	g.Categories,
	COUNT(*) AS TotalInGrooup,
	COUNT(*)*1.0 / (SELECT COUNT(*) FROM GroupCategories) AS PercentageInGroup
FROM GroupCategories g
GROUP BY g.Categories
ORDER BY TotalInGrooup DESC
```
**Result:**

| Categories | TotalInGrooup | PercentageInGroup |
|------------|---------------|-------------------|
| Medium     | 35            | 0.432098765432    |
| Low        | 20            | 0.246913580246    |
| High       | 13            | 0.160493827160    |
| Very High  | 13            | 0.160493827160    |

**51. Andrew, the VP of Sales is still thinking about how best to group customers, and define low, medium, high, and very high value customers. He now wants complete flexibility in grouping the customers, based on the dollar amount they've ordered. He doesn’t want to have to edit SQL in order to change the boundaries of the customer groups.
How would you write the SQL?
There's a table called CustomerGroupThreshold that you will need to use. Use only orders from 2016.**
```SQL
WITH cte AS(
SELECT
	o.CustomerID,
	c.CompanyName,
	SUM(d.Quantity * d.UnitPrice) AS TotalAmount
FROM Orders o
LEFT JOIN OrderDetails d
	ON o.OrderID = d.OrderID
LEFT JOIN Customers C
	ON o.CustomerID = c.CustomerID
WHERE YEAR(o.OrderDate) = 2016 
GROUP BY o.CustomerID, c.CompanyName
)
SELECT TOP(10)
	c.CustomerID,
	c.CompanyName,
	c.TotalAmount,
	g.CustomerGroupName
FROM cte c
JOIN CustomerGroupThresholds g
	ON c.TotalAmount BETWEEN g.RangeBottom AND g.RangeTop
ORDER BY c.CustomerID
```
**Result:**

- 81 rows were affeted, showing only the top 10

| CustomerID | CompanyName                        | TotalAmount | CustomerGroupName |
|------------|------------------------------------|-------------|-------------------|
| ALFKI      | Alfreds Futterkiste                | 2302,20     | Medium            |
| ANATR      | Ana Trujillo Emparedados y helados | 514,40      | Low               |
| ANTON      | Antonio Moreno Taquería            | 660,00      | Low               |
| AROUT      | Around the Horn                    | 5838,50     | High              |
| BERGS      | Berglunds snabbköp                 | 8110,55     | High              |
| BLAUS      | Blauer See Delikatessen            | 2160,00     | Medium            |
| BLONP      | Blondesddsl père et fils           | 730,00      | Low               |
| BOLID      | Bólido Comidas preparadas          | 280,00      | Low               |
| BONAP      | Bon app'                           | 7185,90     | High              |
| BOTTM      | Bottom-Dollar Markets              | 12227,40    | Very High         |

**52. Some Northwind employees are planning a business trip, and would like to visit as many suppliers and customers as possible. For their planning, they’d like
to see a list of all countries where suppliers and/or customers are based.**
```SQL
SELECT Country FROM Suppliers
UNION
SELECT Country FROM Customers
ORDER BY Country
```
**Result:**

| Country     |
|-------------|
| Argentina   |
| Australia   |
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
| Japan       |
| Mexico      |
| Netherlands |
| Norway      |
| Poland      |
| Portugal    |
| Singapore   |
| Spain       |
| Sweden      |
| Switzerland |
| UK          |
| USA         |
| Venezuela   |

**53. The employees going on the business trip don’t want just a raw list of countries, they want more details. We’d like to see one column with the suppliers country and other with customers country.**
```SQL
WITH SupplierCountries AS(
SELECT 
	DISTINCT Country
FROM Suppliers
),
CustomerCountries AS(
SELECT
	DISTINCT Country
FROM Customers
)
SELECT
	s.Country As SupplierCountries,
	c.Country AS CustomerCountry
FROM SupplierCountries s
FULL OUTER JOIN Customers c
	ON s.Country = c.Country
GROUP BY s.Country, c.Country
```
**Result:**

| SupplierCountries | CustomerCountry |
|-------------------|-----------------|
| NULL              | Argentina       |
| NULL              | Austria         |
| NULL              | Belgium         |
| NULL              | Ireland         |
| NULL              | Mexico          |
| NULL              | Poland          |
| NULL              | Portugal        |
| NULL              | Switzerland     |
| NULL              | Venezuela       |
| Australia         | NULL            |
| Brazil            | Brazil          |
| Canada            | Canada          |
| Denmark           | Denmark         |
| Finland           | Finland         |
| France            | France          |
| Germany           | Germany         |
| Italy             | Italy           |
| Japan             | NULL            |
| Netherlands       | NULL            |
| Norway            | Norway          |
| Singapore         | NULL            |
| Spain             | Spain           |
| Sweden            | Sweden          |
| UK                | UK              |
| USA               | USA             |

**54. The output of the above is improved, but it’s still not ideal. What we’d really like to see is the country name, the total suppliers, and the total customers.**
```SQL
WITH SupplierCountries AS (
SELECT 
	Country, 
	Count(*) AS Total
FROM Suppliers 
GROUP BY Country
),
CustomerCountries AS (
SELECT 
	Country, 
	Count(*) AS Total
FROM Customers 
GROUP BY Country
)
SELECT
	 ISNULL(SupplierCountries.Country, CustomerCountries.Country) AS Country,
	 ISNULL(SupplierCountries.Total,0) AS TotalSuppliers,
	 ISNULL(CustomerCountries.Total,0) AS TotalCustomers
FROM SupplierCountries
	FULL OUTER JOIN CustomerCountries
		ON CustomerCountries.Country = SupplierCountries.Country
```
**Result:**

| Country     | TotalSuppliers | TotalCustomers |
|-------------|----------------|----------------|
| Argentina   | 0              | 3              |
| Australia   | 2              | 0              |
| Austria     | 0              | 2              |
| Belgium     | 0              | 2              |
| Brazil      | 1              | 9              |
| Canada      | 2              | 3              |
| Denmark     | 1              | 2              |
| Finland     | 1              | 2              |
| France      | 3              | 11             |
| Germany     | 3              | 11             |
| Ireland     | 0              | 1              |
| Italy       | 2              | 3              |
| Japan       | 2              | 0              |
| Mexico      | 0              | 5              |
| Netherlands | 1              | 0              |
| Norway      | 1              | 1              |
| Poland      | 0              | 1              |
| Portugal    | 0              | 2              |
| Singapore   | 1              | 0              |
| Spain       | 1              | 5              |
| Sweden      | 2              | 2              |
| Switzerland | 0              | 2              |
| UK          | 2              | 7              |
| USA         | 4              | 13             |
| Venezuela   | 0              | 4              |

**55. Looking at the Orders table—we’d like to show details for each order that was the first in that particular country, ordered by OrderID. So, we need one row per ShipCountry, and CustomerID, OrderID, and OrderDate should be of the first order from that country.**
```SQL
WITH CTE as(
SELECT 
	ShipCountry,
	CustomerID,
	OrderID,
	CONVERT(DATE, OrderDate) AS OrderDate,
	ROW_NUMBER() OVER (PARTITION BY ShipCountry ORDER BY ShipCountry, OrderID) AS OrderNumber
FROM Orders
)
SELECT 
	ShipCountry,
	CustomerID,
	OrderID,
	OrderDate
FROM CTE
WHERE OrderNumber = 1
```
**Result:**

| ShipCountry | CustomerID | OrderID | OrderDate  |
|-------------|------------|---------|------------|
| Argentina   | OCEAN      | 10409   | 2015-01-09 |
| Austria     | ERNSH      | 10258   | 2014-07-17 |
| Belgium     | SUPRD      | 10252   | 2014-07-09 |
| Brazil      | HANAR      | 10250   | 2014-07-08 |
| Canada      | MEREP      | 10332   | 2014-10-17 |
| Denmark     | SIMOB      | 10341   | 2014-10-29 |
| Finland     | WARTH      | 10266   | 2014-07-26 |
| France      | VINET      | 10248   | 2014-07-04 |
| Germany     | TOMSP      | 10249   | 2014-07-05 |
| Ireland     | HUNGO      | 10298   | 2014-09-05 |
| Italy       | MAGAA      | 10275   | 2014-08-07 |
| Mexico      | CENTC      | 10259   | 2014-07-18 |
| Norway      | SANTG      | 10387   | 2014-12-18 |
| Poland      | WOLZA      | 10374   | 2014-12-05 |
| Portugal    | FURIB      | 10328   | 2014-10-14 |
| Spain       | ROMEY      | 10281   | 2014-08-14 |
| Sweden      | FOLKO      | 10264   | 2014-07-24 |
| Switzerland | CHOPS      | 10254   | 2014-07-11 |
| UK          | BSBEV      | 10289   | 2014-08-26 |
| USA         | RATTC      | 10262   | 2014-07-22 |
| Venezuela   | HILAA      | 10257   | 2014-07-16 |

**56. There are some customers for whom freight is a major expense when ordering from Northwind. However, by batching up their orders, and making one larger order instead of multiple smaller orders in a short period of time, they could reduce their freight costs significantly.
Show those customers who have made more than 1 order in a 5 day period. The sales people will use this to help customers reduce their costs.**
```SQL
SELECT TOP(10)
	InitialOrder.CustomerID,
	InitialOrder.OrderID AS InitialOrderID,
	InitialOrder.OrderDate AS InitialOrderDate,
	NextOrder.OrderID AS NextOrderID,
	NextOrder.OrderDate AS NextOrderDate,
	DATEDIFF(dd, InitialOrder.OrderDate, NextOrder.OrderDate) AS DaysBetween
FROM Orders InitialOrder
JOIN Orders NextOrder
	ON InitialOrder.CustomerID = NextOrder.CustomerID
WHERE InitialOrder.OrderID < NextOrder.OrderID AND DATEDIFF(dd, InitialOrder.OrderDate, NextOrder.OrderDate) <= 5
ORDER BY InitialOrder.CustomerID, InitialOrder.OrderID
```
**Result:**

- 71 rows were affeted, showing only the top 10

| CustomerID | InitialOrderID | InitialOrderDate        | NextOrderID | NextOrderDate           | DaysBetween |
|------------|----------------|-------------------------|-------------|-------------------------|-------------|
| ANTON      | 10677          | 2015-09-22 20:00:00.000 | 10682       | 2015-09-25 04:00:00.000 | 3           |
| AROUT      | 10741          | 2015-11-14 10:00:00.000 | 10743       | 2015-11-17 18:00:00.000 | 3           |
| BERGS      | 10278          | 2014-08-12 14:00:00.000 | 10280       | 2014-08-14 10:00:00.000 | 2           |
| BERGS      | 10444          | 2015-02-12 11:00:00.000 | 10445       | 2015-02-13 20:00:00.000 | 1           |
| BERGS      | 10866          | 2016-02-03 01:00:00.000 | 10875       | 2016-02-06 21:00:00.000 | 3           |
| BONAP      | 10730          | 2015-11-05 07:00:00.000 | 10732       | 2015-11-06 15:00:00.000 | 1           |
| BONAP      | 10871          | 2016-02-05 19:00:00.000 | 10876       | 2016-02-09 17:00:00.000 | 4           |
| BONAP      | 10932          | 2016-03-06 01:00:00.000 | 10940       | 2016-03-11 02:00:00.000 | 5           |
| BOTTM      | 10410          | 2015-01-10 18:00:00.000 | 10411       | 2015-01-10 21:00:00.000 | 0           |
| BOTTM      | 10944          | 2016-03-12 04:00:00.000 | 10949       | 2016-03-13 13:00:00.000 | 1           |

**57. There’s another way of solving the problem above, using Window functions. We would like to see the following results.**
```SQL
WITH cte AS(
SELECT
	CustomerID,
	CONVERT(DATE, OrderDate) AS OrderDate,
	CONVERT(DATE, LEAD(OrderDate,1) OVER (PARTITION BY CustomerID ORDER BY CustomerID, OrderDate)) AS NextOrderDate
FROM Orders
--ORDER BY CustomerID, OrderID
)
SELECT
	cte.CustomerID,
	cte.OrderDate,
	cte.NextOrderDate,
	DATEDIFF(DD, cte.OrderDate, cte.NextOrderDate) AS DaysBetweenOrders
FROM cte
WHERE DATEDIFF(DD, cte.OrderDate, cte.NextOrderDate) <=5
```
**Result:**

- 69 rows were affeted, showing only the top 10

| CustomerID | OrderDate  | NextOrderDate | DaysBetweenOrders |
|------------|------------|---------------|-------------------|
| ANTON      | 2015-09-22 | 2015-09-25    | 3                 |
| AROUT      | 2015-11-14 | 2015-11-17    | 3                 |
| BERGS      | 2014-08-12 | 2014-08-14    | 2                 |
| BERGS      | 2015-02-12 | 2015-02-13    | 1                 |
| BERGS      | 2016-02-03 | 2016-02-06    | 3                 |
| BONAP      | 2015-11-05 | 2015-11-06    | 1                 |
| BONAP      | 2016-02-05 | 2016-02-09    | 4                 |
| BONAP      | 2016-03-06 | 2016-03-11    | 5                 |
| BOTTM      | 2015-01-10 | 2015-01-10    | 0                 |
| BOTTM      | 2016-03-12 | 2016-03-13    | 1                 |
