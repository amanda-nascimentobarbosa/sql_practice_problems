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

| OrderID |
|---------|
| 10263   |
| 10263   |
| 10990   |
| 10658   |
| 11030   |























