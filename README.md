# SQL-practice

### SQL Practice №3 | The computer store

#### Relational Schema 

![Computer-store-db](https://user-images.githubusercontent.com/69513400/130349372-8618bcfd-3b2e-435d-86b0-98f7e1c8477e.png)

#### Table creation code

``` sql
CREATE TABLE Manufacturers (
	Code INTEGER PRIMARY KEY NOT NULL,
	Name CHAR(50) NOT NULL 
);

CREATE TABLE Products (
	Code INTEGER PRIMARY KEY NOT NULL,
	Name CHAR(50) NOT NULL ,
	Price REAL NOT NULL ,
	Manufacturer INTEGER NOT NULL 
		CONSTRAINT fk_Manufacturers_Code REFERENCES Manufacturers(Code)
);
```

#### Sample dataset

``` sql
INSERT INTO Manufacturers (Code, Name) VALUES (1, 'Sony');
INSERT INTO Manufacturers (Code, Name) VALUES (2, 'Creative Labs');
INSERT INTO Manufacturers (Code, Name) VALUES (3, 'Hewlett-Packard');
INSERT INTO Manufacturers (Code, Name) VALUES (4, 'Iomega');
INSERT INTO Manufacturers (Code, Name) VALUES (5, 'Fujitsu');
INSERT INTO Manufacturers (Code, Name) VALUES (6, 'Winchester');
INSERT INTO Manufacturers (Code, Name) VALUES (7, 'Bose');
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (1, 'Hard drive', 240, 5);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (2, 'Memory', 120, 6);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (3, 'ZIP drive', 150, 4);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (4, 'Floppy disk', 5, 6);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (5, 'Monitor', 240, 1);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (6, 'DVD drive', 180, 2);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (7, 'CD drive', 90, 2);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (8, 'Printer', 270, 3);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (9, 'Toner cartridge', 66, 3);
INSERT INTO Products (Code, Name, Price, Manufacturer) VALUES (10, 'DVD burner', 180, 2);
```

#### Exercises

1. Select the names of all the products in the store.

2. Select the names and the prices of all the products in the store.


3. Select the name of the products with a price less than or equal to $200.


4. Select all the products with a price between $60 and $120.


5. Select the name and price in cents (i.e., the price must be multiplied by 100).


6. Compute the average price of all the products.


7. Compute the average price of all products with manufacturer code equal to 2.


8. Compute the number of products with a price larger than or equal to $180.


9. Select the name and price of all products with a price larger than or equal to $180, and sort first by price (in descending order), and then by name (in ascending order).


10. Select all the data from the products, including all the data for each product's manufacturer.


11. Select the product name, price, and manufacturer name of all the products.


12. Select the average price of each manufacturer's products, showing only the manufacturer's code.


13. Select the average price of each manufacturer's products, showing the manufacturer's name.


14. Select the names of manufacturer whose products have an average price larger than or equal to $150.


15. Select the name and price of the cheapest product.


16. Select the name of each manufacturer along with the name and price of its most expensive product.


17. Select the name of each manufacturer which have an average price above $145 and contain at least 2 different products.


18. Add a new product: Loudspeakers, $70, manufacturer 2.


19. Update the name of product 8 to "Laser Printer".


20. Apply a 10% discount to all products.


21. Apply a 10% discount to all products with a price larger than or equal to $120.

#### Answers

``` sql
1. SELECT Name FROM products2;

2. SELECT Name, Price FROM products2;

3. SELECT Name FROM products2 WHERE Price <= 200;

4. SELECT * FROM products2 WHERE Price BETWEEN 60 AND 120;

5. SELECT Name, Price * 100 FROM products2;

6. SELECT avg(Price) AS allAvgPrice FROM products2;

7. SELECT avg(Price) FROM Products2 WHERE Manufacturer = 2;

8. SELECT count(*) FROM Products2 WHERE Price >= 180;

9. SELECT Name, Price FROM Products2 WHERE Price >= 180 ORDER BY Price DESC, Name;

10. SELECT * FROM Products2 INNER JOIN Manufacturers ON Products2.Manufacturer = Manufacturers.Code;

11. SELECT Products2.Name, Price, Manufacturers.Name FROM Products2 INNER JOIN Manufacturers ON Products2.Manufacturer = Manufacturers.Code;

12. SELECT avg(Price), Manufacturer FROM Products2 GROUP BY Manufacturer;

13. SELECT avg(Price), Manufacturers.Name FROM Products2, Manufacturers WHERE Products2.Manufacturer = Manufacturers.Code GROUP BY Manufacturers.Name;

14. SELECT Manufacturers.Name, avg(Price) FROM Products2 INNER JOIN Manufacturers on Manufacturers.Code = Products2.Manufacturer group by Manufacturers.Name HAVING avg(Price) >= 150;

15. SELECT Name, Price FROM Products2 ORDER BY Price LIMIT 1;

16. SELECT Manufacturers.Name, Products2.Name, Price FROM Products2 INNER JOIN Manufacturers ON Manufacturers.Code = Products2.Manufacturer AND Products2.Price = (SELECT MAX(Price) FROM Products2 WHERE Products2.Manufacturer = Manufacturers.Code);

17. SELECT Manufacturers.Name FROM Products2 INNER JOIN Manufacturers on Manufacturers.Code = Products2.Manufacturer GROUP BY Manufacturers.Name HAVING avg(Price) >= 145 AND count(Products2.Manufacturer) >= 2;

18. INSERT INTO Products2 (Code, Name, Price, Manufacturer) VALUES (11, 'Loudspeakers', 70, 2);

19. SELECT * FROM Products2;

20. UPDATE Products2 SET Name = 'Laser Printer' WHERE Code = 8;

21. UPDATE Products2 SET Price = Price * 0.9;

22. UPDATE Products2 SET Price = Price * 0.9 WHERE Price >= 120;
```
