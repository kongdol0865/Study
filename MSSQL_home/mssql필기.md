#### (25) Group by

group by 뒤에 오는거 기준으로 정렬

```mssql

```

#### (26) Having

having 절은 group by 뒤에

```mssql
select Country, count(CustomerID) AS CustomerId
from Customers
group by Country
having count(CustomerId) > 5
order by count(CustomerID) desc


SELECT b.LastName, b.FirstName, COUNT(a.OrderID) AS NumberOfOrders
FROM Orders a
JOIN Employees b ON a.EmployeeID = b.EmployeeID)
GROUP BY b.LastName, b.FirstName
HAVING COUNT(a.OrderID) > 100;
ORDER BY  COUNT(a.OrderID) desc
```



#### (27) Exists

in이랑 비슷한 개념 

//주문한 적이 있는 사용자 이름 출력하는 느낌

```mssql
select SupplierName
from Suppliers a
where exists(select * from Products b where a.SupplierID = b.SupplierID and b.UnitPrice>100)
```

#### (28) Any, all

 where 나 having 절에서 쓰임

```mssql
SELECT ProductName
FROM Products
WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
```



#### (29) Select Into

테이블을 물리적으로 백업할 때

```mssql
SELECT * INTO CustomersBackup2017
FROM Customers
where Country='Germany'

select a.CustomerID, a.CompanyName 
into CustomersBackup2017_2
from Customers a
join Orders b on a.CustomerID = b.CustomerID
```

테이블 껍데기 만들기

```mssql
SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```

#### (30) Insert into select

select문에 해당하는 데이터를 벌크로 insert할 때 

```mssql
INSERT INTO  newtable (CompanyName, City, Country)
SELECT CompanyName, City, Country FROM Suppliers;

delete newtable
INSERT INTO  newtable (CompanyName, City, Country)
SELECT CompanyName, City, Country FROM Suppliers
where Country='Germany'

```

#### (31)Null functions

isnull() : 연산할 때 isnull 필수

```mssql
select UnitPrice
	, 
	 UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0)) as SomethingAmount
from Products
```

#### (32)Stored Procedures

```mssql
create proc dbo.usp_get_customer
as
/*
	Created: 20200528
	Created by: Liah
	TEST	
		dbo.usp_get_customer

*/
begin
	SELECT * FROM dbo.Customers
end
```

새로운 세션창을 연다

```mssql
exec dbo.usp_get_customer
```

​	파라미터 하나

```mssql
create proc dbo.select_customers
@City varchar(255)
as
/*
	Created: 20200528
	Created by: Liah
	TEST	
		dbo.usp_get_customer

*/
begin
	SELECT * FROM dbo.Customers
	where City=@City
end
```

세션창 열어서

```mssql
exec dbo.select_customers 'Berlin'
exec dbo.select_customers @City='Berlin'
```

파라미터 여러개

```mssql
alter proc dbo.select_customers
@City varchar(255)
@PoastalCode varchar(255)
as
/*
	Created: 20200528
	Created by: Liah
	TEST	
		dbo.usp_get_customer

*/
begin
	SELECT * FROM dbo.Customers
	where City=@City and PoastalCode=@PoastalCode
end
```

```mssql
exec dbo.select_customers 'Berlin','12209'
```

parameter중 하나만 줬을때도 가능하게 하려면

```mssql
exec dbo.select_customers '','12209'
```

```mssql
begin
	SELECT * FROM dbo.Customers
	where City= case when @City='' then City else @City end
	and PoastalCode=case when @ PoastalCode='' then  PoastalCode else @ PoastalCode end
```

#### (33) Comments

--붙이면 주석됨

```mssql
--select all
/*
	this is block comments
*/
SELECT * FROM Customers -- WHERE City='Berlin';
```

