## Databases
Structured collection of data stored for use by one or more applications. Contains the relationships between data items and groups of data items. Can sometimes contain sensitive data that needs to be secured.
It has a query language.

>[!note] DBMS Architecture
>![[Pasted image 20251117112858.png|500]]

## Relational Databases
Table of data consisting of rows and columns
- each column holds a particular type of data
- each row contains a specific value for each column
- ideally has one column where all values are unique, forming an identifier/key for that row
Enables the creation of multiple tables linked together by a unique identifier that is present in all tables. Use a relational query language to access the database.
>[!tip] Relational Database Elements
>- Relation
>	- table/file
>- Tuple
>	- row/record
>- Attribute
>	- Column/field
>**Primary key** -> uniquely identifies a row, consists of one or more column names
>**Foreign key** -> links one t