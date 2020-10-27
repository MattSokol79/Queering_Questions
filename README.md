Q1 - How many orders in NWDB?
Query:
```sql
SELECT COUNT(OrderID) FROM Orders 
```

Response:
830

Q2 - How many orders where the Ship City is Rio de Janeiro
Query:
```sql
SELECT COUNT(OrderID) FROM Orders WHERE ShipCity = 'Rio de Janeiro';
```

Response:
34

Q3 - Select all orders where the Ship City is Rio de Janeiro or Reims?
Query:
```sql
SELECT COUNT(OrderID) FROM Orders WHERE ShipCity = 'Rio de Janeiro' OR ShipCity = 'Reims';
```

Response:
39

Q4 - Select all of the entries where the Company Name has a 'z' or a 'Z' in the table of Customers
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

Q5 - 
