
===

2. Напишите запрос, отображающий идентификатор продукта и его наименование, из таблицы Production.Product для строк, содержащих "Mountain" в наименовании.

SELECT ProductID, Name, ProductNumber FROM Production.Product WHERE Name LIKE '%Mountain%';

===

3. Напишите запрос, отображаoющий идентификатор заказа, дату заказа и общую сумму заказа из таблицы Sales.SalesOrderHeader. Общая сумма заказа должна превышать 1000, при этом идентификатор продавца равняется 279 или идентификатор территории равняется 6.

SELECT SalesOrderID, OrderDate, TotalDue FROM Sales.SalesOrderHeader WHERE TotalDue > 1000 AND (SalesPersonID = 279 OR TerritoryID = 6);

===

5. Напишите запрос, используя таблицу Production.Product, для отображения описания продукции в формате "ProductID: Name”

SELECT CONCAT(ProductID, ': ', Name) AS ProductDescription FROM Production.Product;

===

6. Напишите запрос, в котором подсчитывается количество дней между датой размещения заказа и датой его доставки, используя таблицу Sales.SalesOrderHeader. В вывод включите поля: SalesOrderID, OrderDate, ShipDate.

SELECT SalesOrderID, OrderDate, ShipDate, DATEDIFF(DAY, OrderDate, ShipDate) AS DaysBetween FROM Sales.SalesOrderHeader;
