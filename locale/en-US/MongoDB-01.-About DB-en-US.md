# About Database?

> A database is an organized collection of structured information, or data, typically stored electronically in a computer system.
> 
> A database is usually controlled by a database management system (DBMS).
> 
> Together, the data and the DBMS, along with the applications that are associated with them, are referred to as a database system, often shortened to just database.
>
> Data within the most common types of databases in operation today is typically modeled in rows and columns in a series of tables to make processing and data querying efficient.
> 
> The data can then be easily accessed, managed, modified, updated, controlled, and organized.
> 
> Most databases use structured query language (SQL) for writing and querying data.

by [ORACLE](https://www.oracle.com/database/what-is-database/)

Simply put, it's a space for storing and managing data.

For example, you can manage data by rows and columns, as in Excel.

DBMS is a system for managing this database.

There are various DBMS.

* Oracle
* MySQL
* MariaDB
* MSSQL
* MongoDB
* PostgreSQL
* etc...

MongoDB is main DBMS in PMI.

DBMS is divided into RDBMS and NoSQL

## RDBMS vs NoSQL

### Key Feature

**RDBMS**

* Saves the data structure in the form of a table(row, col).
* The schema (data structure) is strictly defined, so all data must be stored in the same structure.
* Explicitly establish relationships between data (1:1, 1:N, N:N)

**NoSQL**

* Store data in a flexible format (documents, key-values, graphs, etc.)
* No schemaless predefined data structure is required.
* Each document can have an independent structure.
* It focuses on independent data storage rather than relationships between data.

### Scalability

**RDBMS**

* Supports vertical expansion.
* There may be limitations to large-scale data processing.

**NoSQL**

* Supports horizontal expansion.
* It is advantageous for large-scale data processing and traffic processing.

### A way of storing data

**RDBMS**

* Split the data into table units and minimize redundancy through normalization.
* You can import data by joining between tables.
* 
**NoSQL**

* Save data in document or object format.
* Allows storage of duplicate data.
* Joining is not recommended for read performance.

### Schema and flexibility

**RDBMS**

* Because the schema is fixed, the data format and structure must match the schema to add data.
* Changes require modification of the schema, which makes it less flexible.

**NoSQL**

* It's flexible and you can easily change your data structure as needed.
* Suitable for frequent changes in requirements or storing unstructured data.


### Query Language

**RDBMS**

* Use standardized structured query language (SQL) to manage data.
* You can easily handle your data by writing complex queries.

**NoSQL**

* Each database provides a unique query language.
* Optimized for simple Create, Read, Update, Delete (CRUD) tasks.


### Support Transaction

**RDBMS**

* Ensures Atomicity, Consistency, Isolation, Durability (ACID) characteristics, providing excellent data integrity and reliability.

* It is suitable if you need accurate data, such as banking, finance, and ERP systems.

**NoSQL**

* 보통 BASE(Basically Available, Soft state, Eventual consistency)를 따릅니다.

* It does not guarantee immediate consistency, but the data eventually becomes consistent over time.

* We prioritize performance and scalability.

### Use case

**RDBMS**

* When there is a lot of structured data (such as finance, inventory management, ERP, CRM) and data integrity is critical.

* Ex: MySQL, PostgreSQL, Oracle, SQL Server

**NoSQL**

* When there is a lot of unstructured data, such as real-time data processing, IoT, social networks, and log analysis, and large-scale data needs to be handled.

* Ex: MongoDB, Redis, Cassandra, DynamoDB

### 요약 표

| Feature        | 	RDBMS                                               | 	NoSQL                                          |
|----------------|------------------------------------------------------|-------------------------------------------------|
| Data model     | 	Table-based                                         | 	document, key-value, graph, Column-based       |
| Schema         | 	Fixed-schema                                        | 	Flexible Schema                                |
| Scalability    | 	Vertical expansion                                  | 	Horizontal expansion                           |
| Consistency    | 	ACID Guarantee                                      | 	BASE Guarantee                                 |
| Query Language | 	SQL                                                 | 	Unique query language per database             |
| Use Case       | 	Structured data, complex relational data processing | 	Unstructured data, large-scale data processing |




