-------create table------
--create mainShop
create table mainShop( 
mainId int unique not null primary key,
mainName varchar(255) unique not null );

--insert main shop
insert into mainShop(mainId,mainName) values
(1,'UNION');
drop table mainShop;

--create mainshoplist
create table mainShopList( 
MainId int,
MainName varchar(255),
branchshopId int primary key not null unique,
branchShopName varchar(255) unique,  
phNo varchar(255) unique, 
fax varchar(255) unique
)
drop table mainshoplist;

--insert mainShopList
insert into mainShopList(MainId,branchshopId,branchshopname,phNo,fax) values 
(1,1,'Makishi','090-090-090','010-010-010'),
(1,2,'tsuboya','080-080-080','020-020-020'),
(1,3,'tomari','070-070-070','030-030-030');

--join mainShop and mainShopList
select mainshop.mainId,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax
from mainshop
join mainShopList
on mainshop.mainId = mainShopList.MainId;

--branchshoplist
create table branchShop(
MainId int,
MainName varchar(255),
branchshopId int,
branchshopname varchar(255) not null,
staff_id bigint unique primary key,
staff_name varchar(255) unique
);
 drop table branchshop;

--insert branchshoplist
insert into branchShop(mainId,branchshopid,branchshopname,staff_id,staff_name) values 
(1,1,'Makishi',6,'momonosuke');
select * from branchShop;

--join mainShop and mainShopList and branchshop
select mainShop.mainid,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchShop.staff_id,
branchShop.staff_name
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid;

--create product
CREATE TABLE product ( 
  MainId int,
  MainName varchar(255),
  branchshopid int,
  branchshopname varchar(255),
  staff_id int,
  staff_name varchar(255),
  productId  bigint primary key unique,
  productName varchar(255) unique not null, 
  productQuan int,
  productPrice DECIMAL(10, 2), 
  productPriceTax DECIMAL(5, 2), 
  productTotal_exclude_tax DECIMAL(10, 2),
  productTotal_include_tax decimal(10, 2)
  ) 
  drop table product;

  -- insert product name,price and tax
  INSERT INTO product 
  (mainid,branchShopId,staff_id,productId,productName,productQuan,productPrice,productPriceTax) VALUES
  (1,1,1,1,'orange', 1, 300.00, 0.08),-- Assuming tax rate of 8%
  (1,1,1,2,'mango',1,1200.00, 0.08),
  (1,1,1,3,'banana',1,150.00,0.08),
  (1,1,1,4,'apple',1,100.00,0.08),
  (1,1,1,5,'guava',1,400.00,0.08),
  (1,1,1,6,'pineapple',1,500.00,0.08),
  (1,1,1,7,'lychee',1,600.00,0.08),
  (1,1,1,8,'strawberry',1,700.00,0.08),
  (1,1,1,9,'grape',1,800.00,0.08),
  (1,1,1,10,'kiwi',1,400.00,0.08);

  --update products and calculate excludeTax and inculdeTax 
  UPDATE product SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax);

  --------can join here
--join mainShop and mainShopList and branchshop and product
select mainShop.mainid,
mainShop.mainName,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchShop.staff_id,
branchShop.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_include_tax
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on mainshoplist.branchshopid = branchshop.branchshopid
join product on branchshop.branchshopid = product.branchshopid;

--can join here
--create customer
create table customer (
    MainId int,
    MainName varchar(255),
    branchshopid int,
    branchshopname varchar(255),
    phno varchar(255),
    fax varchar(255),
    staff_id bigint,
    staff_name varchar(255),
    transaction_id bigint primary key unique ,
    customerId bigint,
    productId bigint,
    productName varchar(255),
    productQuan int,
    productPrice decimal(10, 2),
    productPriceTax decimal(5, 2),
    productTotal_exclude_tax decimal(10, 2),
    productTotal_include_tax decimal(10, 2)
  )
  drop table customer;


--insert customer
insert into customer
(MainId,branchshopid,staff_id,customerId,transaction_id,productId,productQuan) values 
(1,1,6,1,1,1,3);

--update customer info
UPDATE customer SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax);

--join

--can join this
-- --join mainShop and mainShopList and branchshop and product and customer
select mainShop.mainid,
mainShop.mainName,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchShop.staff_id,
branchShop.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_exclude_tax,
product.productTotal_include_tax,
customer.transaction_id,
customer.customerid,
customer.productid,
customer.productname,
customer.productquan,
customer.productprice,
customer.productpricetax,
customer.producttotal_exclude_tax,
customer.producttotal_include_tax
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid
join product on branchshop.branchshopid = product.branchshopid
join customer on product.branchshopid  = customer.branchshopid;


--create transactions
CREATE TABLE transactions (
mainid int,
mainname varchar(255),
branchshopid int,
branchshopname VARCHAR(255),
branchshopphno varchar(255),
fax VARCHAR(255),
staff_id BIGINT,
staff_name VARCHAR(255),
transaction_id BIGINT ,
date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
customerid BIGINT not null PRIMARY KEY unique,
productid BIGINT,
productname VARCHAR(255),
productquan INT,
productprice DECIMAL(10, 2),
productpricetax DECIMAL(5, 2),
producttotal_exclude_tax DECIMAL(10, 2),
producttotal_include_tax DECIMAL(10, 2),
paymentRecieve DECIMAL(10,2),
paymentChanges DECIMAL(10,2)
);

drop table transactions;

--insert into transactions
insert into transactions (
  mainid,
  branchShopId,
  staff_id,
  customerId,
  productId,
  productquan,
  transaction_id,
  paymentrecieve
  )
values
(1, 1, 6, 1, 1, 2, 1,2000.00) ;
-- -- (1, 1, 6, 1, 2, 1, 1),
-- -- (1, 1, 6, 1, 3, 1, 1),
-- -- (1 ,1, 6, 1, 4, 1, 1),


--upadate transaction total price,payment and change
UPDATE transactions SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax),
  paymentchanges = paymentrecieve - producttotal_include_tax;

---- --join mainShop and mainShopList and branchshop and product and customer and transaction
select mainShop.mainid,
mainShop.mainName,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchShop.staff_id,
branchShop.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_exclude_tax,
product.productTotal_include_tax,
customer.transaction_id,
customer.customerid,
customer.productid,
customer.productname,
customer.productquan,
customer.productprice,
customer.productpricetax,
customer.producttotal_exclude_tax,
customer.producttotal_include_tax,
transactions.productquan,
transactions.paymentRecieve,
transactions.paymentChanges
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid
join product on branchshop.branchshopid = product.branchshopid
join customer on product.branchshopid  = customer.branchshopid
join transactions on customer.branchshopid = transactions.branchshopid;



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


提出物：
　１．ER図
　２．テーブル定義書
　３．作成したSQLスクリプト（例：テーブル作成、データ挿入、クエリ）
　４．クエリの実行結果とそれに対する感想（わかったこと・難しかったところ・工夫したところ　など）
１．ER図　ー＞添付画像
２．テーブル定義書　ー＞SQL文で載せます
３．作成したSQLスクリプト ->テーブル作成はテーブル定義書と同じです
 
store
create table
  public.store (
    id_store bigint generated by default as identity,
    name text not null,
    constraint store_pkey primary key (id_store)
  ) tablespace pg_default;
 
orders
create table
  public.orders (
    id_orders bigint generated by default as identity,
    voucher_number timestamp with time zone not null default now(),
    table_number smallint null,
    constraint orders_pkey primary key (id_orders)
  ) tablespace pg_default;
 
anorder
create table
  public.anorder (
    id_anorder bigint generated by default as identity,
    id_orders bigint not null,
    id_menu bigint null,
    constraint anorder_pkey primary key (id_anorder)
  ) tablespace pg_default;
 
menu
create table
  public.menu (
    id_menu bigint generated by default as identity,
    name text not null,
    price bigint null,
    constraint menu_pkey primary key (id_menu)
  ) tablespace pg_default;
 
staff
create table
  public.staff (
    id_staff bigint generated by default as identity,
    name text not null,
    constraint staff_pkey primary key (id_staff)
  ) tablespace pg_default;
 
account
create table
  public.account (
    id_account bigint generated by default as identity,
    id_store bigint null,
    id_staff bigint not null,
    id_orders bigint null,
    amount bigint null,
    date timestamp without time zone null default now(),
    constraint account_pkey primary key (id_account)
  ) tablespace pg_default;
 
３．作成したSQLスクリプト 
４．クエリの実行結果とそれに対する感想　ー＞下にクエリと感想を書きます。
 
SELECT
  account.id_account,
  store.name as store_name,
  staff.name as staff_name,
  account.id_orders,
  order_summary.voucher_number,
  order_summary.table_number,
  total_price as amount,
  account.date
FROM
  account
LEFT JOIN
  store ON account.id_store = store.id_store
LEFT JOIN
  staff ON account.id_staff = staff.id_staff
JOIN
  (
    SELECT
      orders.id_orders,
      orders.voucher_number,
      orders.table_number,
      SUM(menu.price) AS total_price
    FROM
      orders
    JOIN
      anorder ON orders.id_orders = anorder.id_orders
    JOIN
      menu ON anorder.id_menu = menu.id_menu
    GROUP BY
      orders.id_orders
  ) AS order_summary ON order_summary.id_orders = account.id_orders;
 
工夫をしたのはこのクエリです。注文メニューの合計を求めるサブクエリを作って、それをaccount（会計）テーブルにJOINしています。まずは、領収書を発行するのに必要な最小限のデータを、上記クエリで作ってみました。
https://github.com/dianess/sql-challenge.git
