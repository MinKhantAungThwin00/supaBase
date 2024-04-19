# supaBase

CREATE TABLE goods (
  goodsId bigint not null unique primary key,
  goodsNme varchar(255),
  goodsPrc bigint,
  goodsTax bigint,
  goodsPlc varchar(255),
  goodsTotal float,
  goodsStrtDate timestamptz,
  goodsExpDate timestamptz
)





CREATE TABLE customers(
  cusId bigint not null unique primary key,
  cusG_id bigint,
  cusG_name varchar(255),
  cusG_quan int,
  cusG_prc bigint,
  cusG_tax bigint,
  cusG_discnt float,
  cusG_discnt_totl float,
  cusG_total bigint,
  cusPaymet varchar(255),
  cusPaid float,
  cusChanges float,
  cusCheck date
)

CREATE TABLE goods (
  goodsId bigint not null unique primary key,
  goodsQuantity int,
  goodsNme varchar(255),
  goodsPrc bigint,
  goodsTax bigint,
  goodsPlc varchar(255),
  goodsStrtDate time,
  goodsExpDate time
)



CREATE TABLE customers(
  cusId bigint not null unique primary key,
  cusVoucherNo auto increment int
  cusRegistCounterId int,
  cusG_id bigint,
  cusG_name varchar(255),
  cusG_quan int,
  cusG_prc bigint,
  cusG_tax bigint,
  cusG_discnt float,
  cusG_discnt_totl float,
  cusG_total bigint,
  cusPaymet varchar(255),
  cusPaid float,
  cusChanges float,
  cusCheck date
)



create table mainShop(
  branchShopName varchar(255) unique,
  branchShopOwner varchar(255),
  phNo varchar(255) unique,
  fax varchar(255) unique,
  startDate date
)

create table branchShop(
  staff_id int unique primary key,
  staff_name varchar(255),
  staff_counter_check_time timestamp
)

create table top(
  main varchar(255) unique primary key
)

create table mainShop(
  branchShopName varchar(255) unique,
  branchShopOwner varchar(255),
  phNo varchar(255) unique,
  fax varchar(255) unique,
  startDate date
)

Sure! Below is an example of a SQL query to create a simple table structure for a shopping mall receipt:

```sql
CREATE TABLE shopping_receipt (
    receipt_id INT PRIMARY KEY AUTO_INCREMENT,
    item_name VARCHAR(255),
    quantity INT,
    price DECIMAL(10, 2),
    total_price DECIMAL(10, 2)
);
```

This SQL query creates a table named `shopping_receipt` with the following columns:

- `receipt_id`: An integer column to uniquely identify each receipt. It's set as the primary key, and it auto-increments for each new receipt.
- `item_name`: A VARCHAR column to store the name of each item purchased.
- `quantity`: An integer column to store the quantity of each item purchased.
- `price`: A DECIMAL column to store the price per unit of each item.
- `total_price`: A DECIMAL column to store the total price for each item (quantity * price).

You can customize this table structure based on your specific requirements. For example, you might want to add columns for the date of purchase, customer information, etc., depending on the complexity of your shopping mall system.

Sure! To calculate the total price including taxes, you need to incorporate tax calculations into your SQL query. Let's assume you have a tax rate stored in your database or you can provide it directly in the query. Here's how you can modify the previous SQL query to include taxes:

```sql
CREATE TABLE shopping_receipt (
    receipt_id INT PRIMARY KEY AUTO_INCREMENT,
    item_name VARCHAR(255),
    quantity INT,
    price DECIMAL(10, 2),
    tax_rate DECIMAL(5, 2), -- New column for tax rate
    total_price_excluding_tax DECIMAL(10, 2), -- New column for total price excluding tax
    total_price_including_tax DECIMAL(10, 2) -- New column for total price including tax
);
```

In this modified table structure, I've added a new column `tax_rate` to store the tax rate for each item. I've also added two new columns: `total_price_excluding_tax` to store the total price of the items without tax, and `total_price_including_tax` to store the total price including tax.

Now, let's insert some sample data and calculate the total price including tax using a SQL query:

```sql
INSERT INTO shopping_receipt (item_name, quantity, price, tax_rate)
VALUES
    ('Item 1', 2, 10.00, 0.10), -- Assuming tax rate of 10%
    ('Item 2', 1, 20.00, 0.08), -- Assuming tax rate of 8%
    ('Item 3', 3, 15.00, 0.12); -- Assuming tax rate of 12%

UPDATE shopping_receipt
SET total_price_excluding_tax = quantity * price,
    total_price_including_tax = (quantity * price) + (quantity * price * tax_rate);

SELECT * FROM shopping_receipt;
```

In this example, we first insert sample data into the `shopping_receipt` table, including the item name, quantity, price, and tax rate. Then, we use an UPDATE statement to calculate the total price excluding tax and the total price including tax for each item using the provided tax rate. Finally, we select all columns from the `shopping_receipt` table to see the calculated results.

