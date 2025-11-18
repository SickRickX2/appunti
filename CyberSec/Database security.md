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
	- every HTTP header must be trated as dangerous
- *Cookies*
	- they are basically headers and they come from the client -> **dangerous**
- *The database itself: second order injection*
	- The input of the application is stored in the database later, the same input may be fetched from the database and used to build another query -> **dangerous**


#### Methods of SQLi
**Ending the query**
Terminating the query properly can be cumbersome. Frrequently the problem comes from what follows the integrated user parameter. This SQL segment is part of the query and the malicious input must be crafted to handle it without generating syntax errors.
Usually the parameters include comment symbols:
- \#
- \--
**UNION query**
**Second order inject**
To perform the attack a user with a malicious name is registered.
```SQL
$user = "admin'#";
```

\$user is correctly sanitized when it is inserted in the DB.
Later on, the attacker asks to change the password of its malicious user, so the web app fetches info aboout the user from the db and uses them to perform another query:
```SQL
$q = "UPDATE users SET = pass = '".$_POST['newPass']."' 
WHERE user='".$row['user']."'";
```
If the data coming from the database is not properly sanitized, the query will be:
```SQL
$q = "UPDATE users SET pass= 'password' WHERE user='admin'#'";
```
**piggy-backed**
Target: execute an arbitrary number of distinct queries.
Query:
```SQL
$q = "SELECT id FROM users WHERE user='".$user."' AND pass='".$pass."'";
```
Inected parameters;
```SQL
$user = "'; DROP TABLE users --";
```
Query executed:
```SQL
$q = "SELECT id FROM users WHERE user =''; DROP TABLE users --' AND pass= ''";
```
*oss*: Both queries are executed

>[!warning] 
>This is strictly dependent from the method/function invoked to eprform the query.


**SQLi with missing info**
*How to know how tables and columns are named?*
- Brute forcing
- INFORMATION_SCHEMA

Information schema are metadata about the objects within database. Can be used to gather data about any tables from the available databases.

**Blind SQLi**
When systems do not allow you to see output in the form of error messages or extracted database fields whilst conductin SQL injections.

**Exploiting blind SQLi**
- *BENCHMARK* or *SLEEP* (only with MySQL >= 5) (or equivalent functions)
	- BENCHMARK (loop count, expression)
- *IF*
	- IF (expression, expr true, expr false)
- *SUBSTRING*
	- SUBSTRING(str, pos)
	- SUBSTRING(str, FROM pos)
	- SUBSTRING(str, pos, len)
	- SUBSTRING(str, FROM, pos, FOR, len)

### SQLi Countermeasures
We got 3 types:
- **Manual defensive coding practices**
- **Parameterized query insertion**
- **SQL DOM**
All of these are *Defensive coding*.

#### Defensive coding practices
Programmer must take careof *input sanitization*. Programmers are oft