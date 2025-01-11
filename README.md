
===

2. Напишите запрос, отображающий идентификатор продукта и его наименование, из таблицы Production.Product для строк, содержащих "Mountain" в наименовании.

SELECT ProductID, Name, ProductNumber FROM Production.Product WHERE Name LIKE '%Mountain%';

===

3. Напишите запрос, отображаoющий идентификатор заказа, дату заказа и общую сумму заказа из таблицы Sales.SalesOrderHeader. Общая сумма заказа должна превышать 1000, при этом идентификатор продавца равняется 279 или идентификатор территории равняется 6.

SELECT SalesOrderID, OrderDate, TotalDue FROM Sales.SalesOrderHeader WHERE TotalDue > 1000 AND (SalesPersonID = 279 OR TerritoryID = 6);

===

4. Номер продукта в таблице Production.Product содержит дефис (-). Напишите запрос, в котором используется SUBSTRING функция и CHARINDEX функция для отображения символов из номера продукта, которые следуют после первого дефиса.

SELECT SUBSTRING(ProductNumber, CHARINDEX('-', ProductNumber) + 1, LEN(ProductNumber)) AS ProductNumberAfterDash FROM Production.Product;

===

5. Напишите запрос, используя таблицу Production.Product, для отображения описания продукции в формате "ProductID: Name”

SELECT CONCAT(ProductID, ': ', Name) AS ProductDescription FROM Production.Product;

===

6. Напишите запрос, в котором подсчитывается количество дней между датой размещения заказа и датой его доставки, используя таблицу Sales.SalesOrderHeader. В вывод включите поля: SalesOrderID, OrderDate, ShipDate.

SELECT SalesOrderID, OrderDate, ShipDate, DATEDIFF(DAY, OrderDate, ShipDate) AS DaysBetween FROM Sales.SalesOrderHeader;

===

7. Используя подзапрос, отобразите идендификатор и наименование продуктов из таблицы Production.Product, которые уже были заказаны (таблица Sales.SalesOrderDetail).

SELECT prod.ProductID, prod.Name FROM Production.Product prod WHERE prod.ProductID IN ( 
SELECT sod.ProductID FROM Sales.SalesOrderDetail sod);

===

8. Напишите запрос, который отображает количество заказов, размещенных в течении года, по каждому заказчику (таблица Sales.SalesOrderHeader). В вывод включите поля: CustomerID, общее количество заказов, год.

SELECT CustomerID, COUNT(SalesOrderID) AS TotalOrders, YEAR(OrderDate) AS OrderYear FROM Sales.SalesOrderHeader GROUP BY CustomerID, YEAR(OrderDate);

=== 

9. Напишите запрос, который возвращает количество строк детализации по каждому идентификатору заказа (поле SalesOrderID) из таблицы Sales.SalesOrderDetail. Включите только те заказы, которые имееют более 3-х детальных строк.

SELECT SalesOrderID, COUNT(*) AS DetailRowCount FROM Sales.SalesOrderDetail GROUP BY SalesOrderID HAVING COUNT(*) > 3;

===

10. Напишите запрос, который находит самый (или один из самых) продаваемый продукт и выведите общую сумму его продаж (таблица Sales.SalesOrderDetail). В вывод включите поля: ProductID, проданное количество, общая сумма продаж.

SELECT TOP 1 ProductID, SUM(OrderQty) AS TotalQuantity, SUM(LineTotal) AS TotalSales FROM Sales.SalesOrderDetail GROUP BY ProductID ORDER BY TotalQuantity DESC;

===

11. Таблица HumanResources.Employee не содержит имени сотрудника. Объедините таблицу с таблицей Person.Person по полю BusinessEntityID. Выведите поля JobTitle, BirthDate, FirstName, LastName.

SELECT emp.JobTitle, emp.BirthDate, pers.FirstName, pers.LastName FROM HumanResources.Employee emp JOIN Person.Person pers ON emp.BusinessEntityID = pers.BusinessEntityID;

===

12. Напишите запрос с использованием таблиц Sales.SalesOrderHeader, Sales.SalesOrderDetail и Production.Product для выборки общего количества заказанной продукции по идентификатору продукта (Production.Product.ProductID) и дате заказа (Sales.SalesOrderHeader.OrderDate).

SELECT prod.ProductID, so.OrderDate, SUM(soDetail.OrderQty) AS TotalOrderedQuantity FROM Sales.SalesOrderHeader so 
JOIN 
    Sales.SalesOrderDetail soDetail ON so.SalesOrderID = soDetail.SalesOrderID
JOIN 
    Production.Product prod ON soDetail.ProductID = prod.ProductID
GROUP BY prod.ProductID, so.OrderDate ORDER BY prod.ProductID, so.OrderDate;

===
