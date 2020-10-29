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

## UC4 - Ability To Edit Existing Contact with Name
### Editing contact for given name
```UPDATE address_book SET First_name = 'Mohana' WHERE First_Name = 'MK';```
### View address book
```SELECT * FROM address_book;```

## UC5 - Ability To Delete Existing Contact with Name
```DELETE FROM address_book WHERE First_Name='S';```
### View address book
```SELECT * FROM address_book;```

## UC6 -Ability to Retrieve Person belonging to a City or State
### Contact of person belonging to particular city
```SELECT * FROM address_book WHERE City='Bhadrachalam';```
### Contact of person belonging to particular state
```SELECT * FROM address_book WHERE State='Telangana';```

## UC7 - Ability to understand the size of address book by City and State
### Count contacts By city
```
SELECT city,COUNT(city) FROM address_book GROUP BY city;
SELECT COUNT(city) FROM address_book;
```
### Count contacts By state
```
SELECT state,COUNT(state) FROM address_book GROUP BY state;
SELECT COUNT(state) FROM address_book;
```

## UC8 - Ability to retrieve entries sorted alphabetically by Person’s name for a given city
### For a given city , sort contacts in alphabetical order
```SELECT * FROM address_book WHERE city='Hyderabad' ORDER BY firstName;```

## UC9 - Ability to identify each Address Book with name and Type
### Altering table
```
ALTER table address_book add Address_Book_Name varchar(100) First;
ALTER table address_book add Type varchar(50) AFTER Address_Book_Name;
UPDATE address_book set type='Family' where first_Name='Venkat' or first_name = 'KVN';
UPDATE address_book set type='Self' where first_name='Mohana';
UPDATE address_book set Address_Book_Name='Personal' where first_Name='Venkat' or first_name = 'KVN';
UPDATE address_book set Address_Book_Name='Professional' where firstName='Mohana';
```
### View address book
```SELECT * FROM address_book;```

## UC10 - Ability to get number of contact persons(count by type)
```SELECT type,COUNT(type) FROM address_book GROUP BY type;```

## UC11 - Ability to add person to both Friend and Family
```
INSERT INTO address_book(first_Name,last_Name, Address, City, State, Zip, Phone_number, Email, Type, AddressBookName) VALUES(
    -> 'Rambabu','K','Sarapaka','Khammam','Telangana',500050,949876547,'rambabu@gmail.com','Family','Personal'),
    -> ('Rikwitha','Reddy','Lingampally','Hyderabad','AP',400097,8700849367,'pandiRik@gmail.com','Friends','Personal');
```
## UC12 - Ensure all retrieve queries done
### Creating Address Book Table
```
CREATE TABLE address_book_dictionary (
    -> address_book_id int NOT NULL AUTO_INCREMENT Primary Key,
    -> address_book_name varchar(250) NOT NULL,
    -> address_book_type varchar(150) NOT NULL
    -> );
```
### Creating Contact Table
```
CREATE TABLE Contact (
  address_book_id int NOT NULL,
  first_name varchar(150) NOT NULL,
  last_name varchar(150) NOT NULL,
  email_id varchar(150) NOT NULL Primary Key,
  foreign key(address_book_id) references address_book_dicitionary (address_book_id)
);
```
### Creating Address Table
```
CREATE TABLE Contact_Address (
  email_id varchar(150) NOT NULL references contact.email_id,
  address varchar(150) NOT NULL,
  city varchar(150) NOT NULL,
  state varchar(150) NOT NULL,
  zip int NOT NULL,
  PRIMARY KEY(email_id)
);
```
### Creating Phone Number Table
```CREATE TABLE Contact_Number (
  email_id varchar(150) NOT NULL references contact.email_id,
  phone_no varchar(15) NOT NULL,
  PRIMARY KEY(email_id)
);
```
### Inserting Data into Address Book Table
```
insert into address_book_dictionary (address_book_name, address_book_type)
    -> values('Personal', 'Family'),
    -> ('Personal', 'Friends'),
    -> ('Professional', 'Colleagues');
```
### Inserting Data into COntact Table
```
mysql> insert into contact
    -> values(1, 'Rambabu', 'K', 'ram1971@gmail.com'),
    -> (1, 'Lakshmi', 'KVN', 'lakshmi@outlook.com'),
    -> (2, 'Saaiyya', 'chai', 'saailaxmi@citi.com'),
    -> (3, 'Deeks', 'papa', 'deeksha@gmail.com');
```
### Inserting data into Address Table
```
mysql> INSERT INTO contact_address
    -> values('deeksha@gmail.com', 'Lingampally', 'Hyd', 'Telangana', 600604),
    -> ('lakshmi@outlook.com', 'Visakoderu', 'Bhimavaram,', 'AP', 500804),
    -> ('ram1971@gmail.com', 'Sarapaka', 'Bhadrachalam', 'Kerala', 700604),
    -> ('saailaxmi@citi.com', 'Pondi', 'Chennai,', 'Tamil Nadu', 407804);
```
### Inserting data intp Phone Number Table
```
INSERT INTO contact_number
    -> values('ram1971@gmail.com', '9705505031'),
    -> ('ram1971@gmail.com', '9000278444'),
    -> ('lakshmi@outlook.com', '9989456772'),
    -> ('deeksha@gmail.com', '9999999999'),
    -> ('saailaxmi@citi.com', '9999996666');
```
### Ability to Retrieve Person belonging to a City or State
```
select a.address_book_name, a.address_book_type, c.first_name, c.last_name, c.email_id, p.phone_no, d.address, d.city, d.state, d.zip
from contact c
inner join address_book_dictionary a
on c.address_book_id = a.address_book_id 
inner join contact_number p
on c.email_id = p.email_id
inner join contact_address d 
on c.email_id = d.email_id where d.city = 'Bhadrachalam';
```
### Ability to understand the size of address book by City and State
```
SELECT city,COUNT(city) FROM contact_address GROUP BY city;
SELECT state,COUNT(state) FROM contact_address GROUP BY state;
```
### Ability to retrieve entries sorted alphabetically by Person’s name for a given city
```
SELECT * FROM contacts WHERE city='Hyderabad' ORDER BY firstName;
```
select a.address_book_name, a.address_book_type, c.first_name, c.last_name, c.email_id, p.phone_no, d.address, d.city, d.state, d.zip
from contact c
inner join address_book_dictionary a
on c.address_book_id = a.address_book_id 
inner join contact_number p
on c.email_id = p.email_id
inner join contact_address d 
on c.email_id = d.email_id where d.city = 'Bhadrachalam'
order by first_name;
```
### Ability to get number of contact persons(count by type)
```
select a.address_book_type, count(c.first_name) as Person_Count 
from contact c join address_book_dictionary a 
on c.address_book_id = a.address_book_id 
where address_book_type = 'Family';
```


