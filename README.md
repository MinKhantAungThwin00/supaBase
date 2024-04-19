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

