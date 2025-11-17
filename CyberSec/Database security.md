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
>- *Relation*
>	- table/file
>- *Tuple*
>	- row/record
>- *Attribute*
>	- Column/field
>
>**Primary key** -> uniquely identifies a row, consists of one or more column names
>**Foreign key** -> links one table to attributes in another
>**View/virtual table** -> result of a query that returns selected rows and columns from one or more tables. Views are often used for security purposes.


### Structured Query Language (SQL)
Standardized language to define schema, manipulated, and query data in relational databse. Several similar versions of ANSI/ISO standard. All follow the same basic syntax and semantics.

### SQL Injection Attacks (SQLi)
One of the most prevakent and dangerous network-based security threats. Designed to exploit the nature of Web application pages. Sends malicious SQL commands to the databse server. Most comon attack goal is *bulk extraction of data*.

>[!tip] 
>Depending on the environment SQL injecion can also be exploited to:
>- Modiffy or delete data
>- Execute arbitrary operating system commands
>- Launch DDOS attacks

### Injection Technique
The SQLi attack typically works by prematurely terminating a text string appending a new command.

>[!note] SQLi Attack Avenues
>- *User input*
>- *Server variables*
>- *Second order injection*
>- *Cookies*
>- *Physical user input*

## Inband Attacks
Uses the same communication channel for injecting SQL code and retrieving results.
The retrieved data are presented directly in application Web page.
- **Tautology**: Injects code in one or more conditional statements so that they always evaluate to true
- **End of line comment**: Legitimate code that follows a particular field are nullified through usage of end of line commnets.
- **Piggybacked queries**: The attacker adds additional queries beyond the intended query, piggybacking the attack on top of a legitimate request
## Inferential Attack
There is no actual transfer of data, but the attacker is able to reconstruct the information by sending particular requests and observing the resulting behavior of the website/database server.
- *Illegal/logically incorrect queries*
	- This attack lets an attacker gather important information about the type and structure of the backend databse of a Web application
	- The attack is considered a preliminary, information-gathering step for other attacks
- *Blind SQL injection*
	- Allows attackers to infer the data present in a database system even when the system is sufficently secure to not display any erroneous information back to the attacker
- *Out of Band Attack*
	- Data are retrieved using a different channel
	- This can be used when there are limitations on information retrieval, but outbount connectivity from the database server is lax

**SQL Injection**
Many web applications require the ability to store structured data and use a *database*. We have a **SQLi** when it is possible to modify the syntax of the query by altering the application input.

SQLi *causes*:
- missing input validation
- application-generated queries contains user-fed input

**SQL sinks** (where to inject our SQL code)
- *User Input*
	- GET/POST parameters
	- many client-side technologies communicate with the server through GET/POST
- *HTTP Headers*
	- every HTTP head