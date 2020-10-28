# Query Tasks on the Northwind Database

## Q1 - How many orders in NWDB?
Query:
```sql
SELECT COUNT(OrderID) FROM Orders 
```

Response:
830

## Q2 - How many orders where the Ship City is Rio de Janeiro
Query:
```sql
SELECT COUNT(OrderID) FROM Orders WHERE ShipCity = 'Rio de Janeiro';
```

Response:
34

## Q3 - Select all orders where the Ship City is Rio de Janeiro or Reims?
Query:
```sql
SELECT COUNT(OrderID) FROM Orders WHERE ShipCity = 'Rio de Janeiro' OR ShipCity = 'Reims';
```

Response:
39

## Q4 - Select all of the entries where the Company Name has a 'z' or a 'Z' in the table of Customers
Query:
```sql
SELECT CompanyName FROM Customers WHERE CompanyName LIKE '%z%' OR CompanyName LIKE '%Z%'
```

Response:
6
Centro comercial Moctezuma
Lazy K Kountry Store
Magazzini Alimentari Riuniti
Queen Cozinha
Toms Spezialitäten
Wolski  Zajazd

## Q5 - We need to update all of our FAX information! This Day and age it is a must! Find me the Name of All of the companies that we 
do not have their FAX numbers! I would also like to know with whom I need to speak with, their contact numbers and what city 
they are base in.
Query:
```sql
SELECT CompanyName, ContactName, Phone, City, Fax FROM Suppliers WHERE Fax IS NULL;
```

Response: 16 names etc.

## Q6 - Re-target all Customers in Paris! Get information on these clients
Query:
```sql
SELECT * FROM Customers WHERE City = 'Paris';
``` 

Response: 2 clients with details

## Q7 - Find out from the clients in Paris which one orders the most by quantity? Top 5 clients?
Query:
```sql
SELECT 
    TOP 5 COUNT(Orders.OrderID) AS 'No. of Orders',
    Customers.CompanyName
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.City = 'Paris'
GROUP BY Customers.CompanyName
ORDER BY COUNT(Orders.OrderID) DESC;
```

Response:
2 clients


## Q8 - Find out for which clients deliveries took more than 10 days. Display the client name, contact name, all their contact details, fax as well as the number of deliveries that were overdue. Add a column named 'Number of overdue orders'.
Query:
```sql
SELECT TOP 5
    Customers.CustomerID,
    Customers.CompanyName,
    Customers.ContactName,
    Customers.Phone,
    Customers.Fax,
    Customers.Address,
    COUNT(Orders.OrderID) AS 'Overdue Orders'
FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID
INNER JOIN [Order Details] ON Orders.OrderID = [Order Details].OrderID
WHERE Orders.RequiredDate - Orders.ShippedDate > 10
GROUP BY
    Customers.CustomerID,
    Customers.CompanyName,
    Customers.ContactName,
    Customers.Phone,
    Customers.Address,
    Customers.Fax
ORDER BY COUNT(Orders.OrderID) DESC;
```
