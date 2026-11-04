-- ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
--	 C H A P T E R   1 
--	"the story starts..."
-- ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄




-- 21/10/2026 starting T-SQL Fundamentals
-- 🚀 ==========================================
-- 🎯 SQL LEARNING JOURNEY
-- 💪 Every query makes me better!
-- 🧠 Learn | Practice | Improve
-- 🏆 Future Data Engineer
-- 🚀 ==========================================
USE TSQLV6;

DROP TABLE IF EXISTS dbo.Employees;

CREATE TABLE dbo.Employees (
    empid     INT          NOT NULL,
    firstname VARCHAR (30) NOT NULL,
    lastname  VARCHAR (30) NOT NULL,
    hiredate  DATE         NOT NULL,
    mgrid     INT          NULL,
    ssn       VARCHAR (30) NOT NULL,
    salary    MONEY        NOT NULL
);

SELECT *
FROM   Employees;

-- 🚀 ==========================================
--PRIMARY KEY CONSTRAINT
-- 🚀 ==========================================
/*
1. enforces the uniqueness of rows 
2. disallows NULLs in the constraint attribute
3. each unique combination of values can appear only once in the table
4. an attempt to define aprimary key constraint on acolumn that allows NULLs will be rejected by the RDBMS
5. each table can have only one primary key
*/
USE TSQLV6;

SELECT *
FROM   dbo.Employees;

ALTER TABLE dbo.Employees
    ADD CONSTRAINT PK_Employees PRIMARY KEY (empid);

-- 🚀 ==========================================
--UNIQUE CONSTRAINTS
-- 🚀 ==========================================
-- 
-- YOU CAN DEFINE MULTIPLE UNIQUE CONSTRAINTS WITHIN THE SAME TABLE
-- NOT RESTRICTED TO COLUMNS DEFINED AS NOT NULL 
ALTER TABLE dbo.employees
    ADD CONSTRAINT unq_employees_ssn UNIQUE (ssn);

/*
 as with a primary key constraint sql server create unique index behind the scene
 as physical mechanism to enforce the logical unique constraint
*/
CREATE UNIQUE INDEX idx_ssn_notnull
    ON dbo.employees(ssn) WHERE ssn IS NOT NULL;

--🚀 ================================
--		FOREIGN KEY CONSTRAINT
--🚀 ================================
/*
foreign key enforces REFRENTIAL INTEGRITY
defined on one or more attributes in whats called
REFERENCING TABLE 
and points to --> candidate key [PRIMARY KEY OR UNIQUE CONSTRAINT] attributes 
in whats called REFERENCED TABLE
the foreign key's purpose is to restrict the values allowed in the foreign key
columns to those that exist in the referenced columns
*/
-- droping the table 
DROP TABLE IF EXISTS dbo.orders;

-- creating the table
CREATE TABLE dbo.orders (
    orderid  INT          NOT NULL,
    empid    INT          NOT NULL,
    custid   VARCHAR (10) NOT NULL,
    ordersts DATETIME2    NOT NULL,
    qty      INT          NOT NULL,
    CONSTRAINT pk_orders PRIMARY KEY (orderid)
);

-- enforce the integrity by adding  foreign key constraint
-- SSMS has a built-in formatter. [Select your code and press Ctrl + K, then Ctrl + Q.]
ALTER TABLE dbo.orders
    ADD CONSTRAINT fk_orders_employees FOREIGN KEY (empid) REFERENCES dbo.employees (empid);

SELECT *
FROM   Employees;

SELECT *
FROM   orders;

-- to restrict the values supported by the mgrid column in the employees table 
-- to the value that exist in the empid column of the same table 
-- you can add so by adding the following foreign key


ALTER TABLE dbo.employees
    ADD CONSTRAINT fk_mgr_emp FOREIGN KEY (mgrid) REFERENCES dbo.employees (empid);




   /*
   if you try to delete any rows from employees table and there is related rows in the orders table 
   the RDBMS WILL REJECT ---> CALLED [NO ACTION]





The preceding two examples are basic definitions of foreign 
keys that enforce a referential action called no action.

No action means that attempts to delete rows from the referenced
table or update the referenced candidate key attributes will be 
rejected if related rows exist in the referencing table. 


For example,
if you try to delete an employee row from the Employees table when there 
are related orders in the Orders table, the RDBMS will reject such an
attempt and produce an error.


You can define the foreign key with actions that will compensate 
for such attempts (to delete rows from the referenced table or 
update the referenced candidate key attributes when related rows
exist in the referencing table).



You can define the options 


ON DELETE and ON UPDATE with actions 

such as  [CASCADE, SET DEFAULT  and SET NULL] as part of the foreign key definition.

CASCADE means 
that the operation (delete or update) will be cascaded to related 
rows.

For example, ON DELETE CASCADE means that when you delete a 
row from the referenced table, the RDBMS will delete the related 
rows from the referencing table.


SET DEFAULT and SET NULL mean 
that the compensating action will set the foreign key attributes 
of the related rows to the column's default value or NULL, respectively. 


Note that regardless of which action you choose, 
the referencing table will have orphaned rows only in the case of the exception with
NULLs in the referencing column that I mentioned earlier. 
Parent rows with no related child rows are always allowed.

   
   */

-- 🚀 =============================
-- 🎯 SQL LEARNING JOURNEY
-- 💪 Every query makes me better!
-- 🧠 Learn | Practice | Improve
-- 🏆 Future Data Engineer
-- 🚀 =============================



--🚀 ================================
--		CHECK CONSTRAINTS
--🚀 ================================
/*

Check constraints

You can use a check constraint to define a predicate that a row 
must meet to be entered into the table or to be modified. 

For example, 
the following check constraint ensures that the salary column in the 
Employees table will support only positive values:



ALTER TABLE dbo. Employees

ADD CONSTRAINT CHK_Employees_salary

CHECK (salary > 0.00);

An attempt to insert or update a row with a nonpositive salary 
value will be rejected by the RDBMS. 

Note that a check constraint 
rejects an attempt to insert or update a row when the predicate 
evaluates to FALSE. 

The modification will be accepted when the 
predicate evaluates to either TRUE or UNKNOWN. 


For example, 
salary -1000 will be rejected, whereas salaries 50000 and 
NULL will both be accepted (if the column allowed NULLs). 



As mentioned earlier, SQL is based on three-valued logic, 
which results in two actual actions. With a check constraint, 
the row is either accepted or rejected.


When adding check and foreign key constraints, 
you can specify an option called --  WITH NOCHECK 
that tells the RDBMS you want it to bypass 
constraint checking for existing data. 

This is considered a bad practice 
because you cannot be sure your data is consistent. 
You can also disable or enable existing check and foreign key constraints.
*/



ALTER TABLE dbo.employees
    ADD CONSTRAINT chk_employees_salary CHECK (salary > 0);


--🚀 ================================
--		DEFAULT CONSTRAINTS
--🚀 ================================

 /*

Default constraints

A default constraint is associated with a particular attribute.
It's an expression that is used as the default value 
when an explicit value is not specified for the attribute when you insert a row For example,
the following code defines a default constraint for 
the orderts attribute (representing the order's time stamp)

ALTER TABLE dbo. Orders

ADO CONSTRAINT DFT_Orders_orderts

DEFAULT (SYSDATETIME()) FOR orderts;

The default expression invokes the SYSDATETIME function 
which returns the current date and time value. 
After this default expression is defined, 
whenever you insert a row into the Orders table and 
do not explicitly specify a value in the orderts attribute, 
SQL Server will  [ set the attribute value to SYSDATETIME ]

When you're done, run the following code for cleanup:

DROP TABLE IF EXISTS dbo.Orders, dbo. Employees;
*/


ALTER TABLE dbo.orders
    ADD CONSTRAINT dft_orders_ordersts DEFAULT (sysdatetime()) FOR ordersts;


--When you're done, run the following code for cleanup:

DROP TABLE IF EXISTS dbo.orders, dbo.Employees;


/* =============================================
   🏆 MILESTONE UNLOCKED: CHAPTER 1 COMPLETED
   ============================================= */

PRINT '================================================';
PRINT '          CHAPTER 1 COMPLETED!                  ';
PRINT '================================================';
PRINT '';
PRINT 'I am not just learning SQL.';
PRINT 'I am building my future, one query at a time.';
PRINT '';
PRINT 'Every error makes me stronger.';
PRINT 'Every challenge sharpens my skills.';
PRINT 'Every chapter brings me closer to mastery.';
PRINT '';
PRINT 'I WILL NOT QUIT.';
PRINT 'I WILL KEEP LEARNING.';
PRINT 'I WILL BECOME A SQL MASTER!';
PRINT '';
PRINT 'Next chapter: BRING IT ON! ';
PRINT '================================================';

/*
   Remember:
   Great data engineers are not born.
   They are built through consistency, curiosity,
   patience, and thousands of queries.

   ONE CHAPTER DOWN.
   A LIFETIME OF GROWTH AHEAD.
*/


/*==============================================================
  MILESTONE: T-SQL FUNDAMENTALS — CHAPTER 1 COMPLETED
  STATUS   : SUCCESS
==============================================================*/

SELECT
    CONVERT(VARCHAR(16), SYSDATETIME(), 120) AS CompletionDateTime,
    'T-SQL Fundamentals' AS CourseName,
    'Chapter 1' AS CompletedMilestone,
    'SUCCESS' AS Status;

/*==============================================================
  "Every query brings me closer to mastery.
   Every chapter builds my future."
==============================================================*/


    🎉--------------------------------------------------------🎉
 🎉--2026-10-21 17:29	T-SQL Fundamentals	Chapter 1	SUCCESS--🎉
 🎉--2026-10-21 17:29	T-SQL Fundamentals	Chapter 1	SUCCESS--🎉
 🎉--2026-10-21 17:29	T-SQL Fundamentals	Chapter 1	SUCCESS--🎉
 🎉--2026-10-21 17:29	T-SQL Fundamentals	Chapter 1	SUCCESS--🎉
    🎉--------------------------------------------------------🎉

