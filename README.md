# Wrisk back-end developer assignment (data and reporting)

## Introduction

At Wrisk that we are building a new insurance platform and data is at the heart of it. While we cannot share our own
dataset or database schema, in the context of this assignment we will use the Northwind sample database. The Northwind
database contains the sales data for a fictitious company called “Northwind Traders”, which imports and exports
specialty foods from around the world. Originally created by Microsoft, Northwind database is an excellent tutorial
schema and has been used by Microsoft as the basis for their tutorials for decades.

The Northwind dataset includes sample data for the following.

* Suppliers: Suppliers and vendors of Northwind
* Customers: Customers who buy products from Northwind
* Employees: Employee details of Northwind traders
* Products: Product information
* Shippers: The details of the shippers who ship the products from the traders to the end-customers
* Orders and Order_Details: Sales Order transactions taking place between the customers & the company

The Northwind sample database includes 14 tables and the table relationships are showcased in the following entity
relationship diagram.

![Er Diagram](ER.png)

## Install the Northwind sample database:

### Using existing PostgreSQL instance

Use the provided sql file `nortwhind.sql` in order to populate your database.

### With Docker and docker compose

#### Pre-requirement: install docker and docker-compose

https://www.docker.com/get-started

https://docs.docker.com/compose/install/

#### 1. Run docker-compose

```bash
> docker-compose up

...
... Lots of messages...
...
Creating network "northwind_psql_default" with the default driver
Creating northwind_psql_db_1 ... done
db_1  | 2019-11-28 21:07:14.357 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db_1  | 2019-11-28 21:07:14.357 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db_1  | 2019-11-28 21:07:14.364 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db_1  | 2019-11-28 21:07:14.474 UTC [1] LOG:  database system is ready to accept connections
```

#### 2. Run psql client in the docker-compose container

Open another terminal window, and type:

````bash
> docker-compose exec db psql -U northwind_user -d northwind

psql (10.5 (Debian 10.5-1.pgdg90+1))
Type "help" for help.

postgres=# select * from us_states;
 state_id |      state_name      | state_abbr | state_region
----------+----------------------+------------+--------------
        1 | Alabama              | AL         | south
        2 | Alaska               | AK         | north
        ...
````

You can connect to the database from your local machine on port `32770` and the jdbc connection string would
be `jdbc:postgresql://localhost:32770/northwind`.

#### 3. Stop docker-compose

Stop the server that was launched by `docker compose up` via `Ctrl-C`, then remove the containers via:

```bash
docker-compose down
```

Your modifications will be persisted in the `dabata/` local folder, and can be retrieved once you
restart `docker compose up`.

## Warm up

Can you answer the following questions using SQL

* When was the first order placed?
* Which customers have placed over 10 orders?

## Programming Task

Your task is to write a program which will generate a report. Spend no more than three nights on it before delivering
your program source to us. You have an option of implementing this solution either in Kotlin or TypeScript.

Please be aware that, if asked to come for an in-person interview after this, you will be expected to talk at length
about the code you have written.

Once finished, please upload your source code (with README.md) to a private github repository and invite
michaelkay-wrisk and aharin to contribute so we can have a look.

### Business requirements

* Produce a report that shows the number of orders along with the total value of orders for the customer with id
  'SAVEA'. This report should include every month between 1996-01-01 and 1998-12-01. If they have not placed an order in
  any of the months then the number of orders and total value of orders should be 0. (Hint: we expect you to create a
  dates dimension table)

## Technical requirements

* Write a program that connects to the Northwind database and generates the report
* User of the program can request either JSON or CSV format
* Provide gradle or (yarn/npm) build scripts to allow us to run your program locally.
* User of the program can select any user id
* User of the program can select any range of months.

## Quality indicators

* Clean code
* Self documenting code
* Proper use of programming language features
* Appropriate use of third-party libraries
* Source control
* Test coverage
* Reusability considerations
* The Open/Closed principle
* Judicious use of comments

