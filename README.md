# CG-DB-AddressBook

## UC1 - Create database for addressbook service
```create database address_book_service;```
### Go to the database created
```use address_book_service;```

## UC2 - Create addressbook table with necessary details
```
create table address_book
    -> ( First_Name    varchar(30)  NOT NULL,
    ->   Last_Name     varchar(30)  NOT NULL,
    ->   Address       varchar(150) NOT NULL,
    ->   City          varchar(50)  NOT NULL,
    ->   State         varchar(50)  NOT NULL,
    ->   Zip           int(6)       NOT NULL,
    ->   Phone_Number  varchar(15)  NOT NULL,
    ->   Email         varchar(150) NOT NULL,
    ->   PRIMARY KEY   (First_Name, Phone_Number)
    -> );
```
### Viewing the address book table
```DESCRIBE address_book;```

## UC3 - Insert new contacts to address book
```
INSERT INTO address_boo VALUES (
    -> 'MK','Kavya','S4 202, ITC limited','Bhadrachalam','Telangana',507128, '8885611111','mk@gmail.com'),
    -> ('S','K','B-123','Warangal','Telangana',506004, '891967665','sk@gmail.com');
```
### View address book
```SELECT* FROM address_book;```


