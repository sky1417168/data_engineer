SQL（Structured Query Language，结构化查询语言）是一种用于管理和操作关系型数据库的标准语言。SQL 语言提供了丰富的命令和语法，用于数据查询、数据操纵、数据定义和数据控制。以下是一些常见的 SQL 概念和操作，以及一些实用的示例。

### SQL 基础

#### 1. 数据查询（Data Query Language, DQL）
数据查询语言主要用于从数据库中检索数据。

- **SELECT 语句**：用于从一个或多个表中检索数据。
  ```sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE condition;
  ```

- **WHERE 子句**：用于指定检索数据的条件。
  ```sql
  SELECT * FROM Employees
  WHERE Salary > 50000;
  ```

- **ORDER BY 子句**：用于对结果集进行排序。
  ```sql
  SELECT * FROM Employees
  ORDER BY Salary DESC;
  ```

- **GROUP BY 子句**：用于将结果集按一个或多个列进行分组。
  ```sql
  SELECT Department, AVG(Salary) AS AverageSalary
  FROM Employees
  GROUP BY Department;
  ```

- **HAVING 子句**：用于对分组后的结果进行过滤。
  ```sql
  SELECT Department, AVG(Salary) AS AverageSalary
  FROM Employees
  GROUP BY Department
  HAVING AVG(Salary) > 60000;
  ```

#### 2. 数据操纵（Data Manipulation Language, DML）
数据操纵语言用于插入、更新和删除数据。

- **INSERT 语句**：用于向表中插入新记录。
  ```sql
  INSERT INTO Employees (FirstName, LastName, Department, Salary)
  VALUES ('John', 'Doe', 'IT', 55000);
  ```

- **UPDATE 语句**：用于更新表中的现有记录。
  ```sql
  UPDATE Employees
  SET Salary = 60000
  WHERE EmployeeID = 1;
  ```

- **DELETE 语句**：用于删除表中的记录。
  ```sql
  DELETE FROM Employees
  WHERE EmployeeID = 1;
  ```

#### 3. 数据定义（Data Definition Language, DDL）
数据定义语言用于定义或修改数据库结构。

- **CREATE TABLE 语句**：用于创建新表。
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      FirstName VARCHAR(50),
      LastName VARCHAR(50),
      Department VARCHAR(50),
      Salary DECIMAL(10, 2)
  );
  ```

- **ALTER TABLE 语句**：用于修改现有表的结构。
  ```sql
  ALTER TABLE Employees
  ADD COLUMN Email VARCHAR(100);
  ```

- **DROP TABLE 语句**：用于删除表。
  ```sql
  DROP TABLE Employees;
  ```

#### 4. 数据控制（Data Control Language, DCL）
数据控制语言用于管理数据库的权限和访问控制。

- **GRANT 语句**：用于授予用户或角色特定的权限。
  ```sql
  GRANT SELECT, INSERT ON Employees TO user1;
  ```

- **REVOKE 语句**：用于撤销用户或角色的权限。
  ```sql
  REVOKE SELECT, INSERT ON Employees FROM user1;
  ```

### 常见的 SQL 函数

#### 聚合函数
- **COUNT**：返回匹配指定条件的行数。
  ```sql
  SELECT COUNT(*) FROM Employees;
  ```

- **SUM**：返回指定列的总和。
  ```sql
  SELECT SUM(Salary) FROM Employees;
  ```

- **AVG**：返回指定列的平均值。
  ```sql
  SELECT AVG(Salary) FROM Employees;
  ```

- **MAX**：返回指定列的最大值。
  ```sql
  SELECT MAX(Salary) FROM Employees;
  ```

- **MIN**：返回指定列的最小值。
  ```sql
  SELECT MIN(Salary) FROM Employees;
  ```

#### 字符串函数
- **CONCAT**：连接两个或多个字符串。
  ```sql
  SELECT CONCAT(FirstName, ' ', LastName) AS FullName
  FROM Employees;
  ```

- **UPPER**：将字符串转换为大写。
  ```sql
  SELECT UPPER(FirstName) FROM Employees;
  ```

- **LOWER**：将字符串转换为小写。
  ```sql
  SELECT LOWER(FirstName) FROM Employees;
  ```

- **SUBSTRING**：提取字符串的一部分。
  ```sql
  SELECT SUBSTRING(Email, 1, 5) FROM Employees;
  ```

#### 日期和时间函数
- **NOW**：返回当前日期和时间。
  ```sql
  SELECT NOW();
  ```

- **DATE_FORMAT**：格式化日期和时间。
  ```sql
  SELECT DATE_FORMAT(HireDate, '%Y-%m-%d') FROM Employees;
  ```

- **DATEDIFF**：计算两个日期之间的差值。
  ```sql
  SELECT DATEDIFF(CURDATE(), HireDate) AS DaysWorked
  FROM Employees;
  ```

### SQL 子查询

子查询是在另一个查询内部嵌套的查询。子查询可以返回单个值、一行或多行。

- **标量子查询**：返回单个值。
  ```sql
  SELECT FirstName, LastName, Salary
  FROM Employees
  WHERE Salary > (SELECT AVG(Salary) FROM Employees);
  ```

- **行子查询**：返回一行。
  ```sql
  SELECT FirstName, LastName, Salary
  FROM Employees
  WHERE (Department, Salary) = (SELECT Department, MAX(Salary) FROM Employees GROUP BY Department);
  ```

- **列子查询**：返回多行。
  ```sql
  SELECT FirstName, LastName
  FROM Employees
  WHERE Department IN (SELECT Department FROM Departments WHERE Location = 'New York');
  ```

### SQL 联接（Joins）

联接用于将两个或多个表中的数据合并在一起。

- **INNER JOIN**：返回两个表中匹配的行。
  ```sql
  SELECT E.FirstName, E.LastName, D.DepartmentName
  FROM Employees E
  INNER JOIN Departments D ON E.Department = D.DepartmentID;
  ```

- **LEFT JOIN**：返回左表中的所有行，以及右表中匹配的行。如果没有匹配，则返回 NULL。
  ```sql
  SELECT E.FirstName, E.LastName, D.DepartmentName
  FROM Employees E
  LEFT JOIN Departments D ON E.Department = D.DepartmentID;
  ```

- **RIGHT JOIN**：返回右表中的所有行，以及左表中匹配的行。如果没有匹配，则返回 NULL。
  ```sql
  SELECT E.FirstName, E.LastName, D.DepartmentName
  FROM Employees E
  RIGHT JOIN Departments D ON E.Department = D.DepartmentID;
  ```

- **FULL OUTER JOIN**：返回两个表中的所有行。如果没有匹配，则返回 NULL。
  ```sql
  SELECT E.FirstName, E.LastName, D.DepartmentName
  FROM Employees E
  FULL OUTER JOIN Departments D ON E.Department = D.DepartmentID;
  ```

- **CROSS JOIN**：返回两个表的笛卡尔积。
  ```sql
  SELECT E.FirstName, E.LastName, D.DepartmentName
  FROM Employees E
  CROSS JOIN Departments D;
  ```

### SQL 视图

视图是一个虚拟表，其内容由查询定义。视图可以简化复杂的查询，并提供数据抽象。

- **创建视图**：
  ```sql
  CREATE VIEW HighPaidEmployees AS
  SELECT FirstName, LastName, Salary
  FROM Employees
  WHERE Salary > 60000;
  ```

- **查询视图**：
  ```sql
  SELECT * FROM HighPaidEmployees;
  ```

### SQL 事务

事务是一组 SQL 语句，这些语句作为一个整体执行，要么全部成功，要么全部失败。

- **BEGIN TRANSACTION**：开始一个事务。
  ```sql
  BEGIN TRANSACTION;
  ```

- **COMMIT**：提交事务，使所有更改生效。
  ```sql
  COMMIT;
  ```

- **ROLLBACK**：回滚事务，撤销所有更改。
  ```sql
  ROLLBACK;
  ```

### 示例：完整的 SQL 脚本

假设我们有一个员工表 `Employees` 和一个部门表 `Departments`，我们可以编写以下 SQL 脚本来创建表、插入数据、查询数据和进行联接操作。

```sql
-- 创建表
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50),
    Location VARCHAR(50)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Department INT,
    Salary DECIMAL(10, 2),
    FOREIGN KEY (Department) REFERENCES Departments(DepartmentID)
);

-- 插入数据
INSERT INTO Departments (DepartmentID, DepartmentName, Location)
VALUES (1, 'IT', 'New York'),
       (2, 'HR', 'Los Angeles');

INSERT INTO Employees (EmployeeID, FirstName, LastName, Department, Salary)
VALUES (1, 'John', 'Doe', 1, 55000),
       (2, 'Jane', 'Smith', 2, 60000),
       (3, 'Alice', 'Johnson', 1, 70000);

-- 查询数据
SELECT * FROM Employees;

-- 联接查询
SELECT E.FirstName, E.LastName, D.DepartmentName, E.Salary
FROM Employees E
INNER JOIN Departments D ON E.Department = D.DepartmentID;

-- 更新数据
UPDATE Employees
SET Salary = 65000
WHERE EmployeeID = 1;

-- 删除数据
DELETE FROM Employees
WHERE EmployeeID = 3;

-- 事务处理
BEGIN TRANSACTION;
UPDATE Employees
SET Salary = 75000
WHERE EmployeeID = 1;
COMMIT;
```

