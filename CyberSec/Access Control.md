*Goal*: Protect confidentiality and integrity of information. Control what a subject can do to prevent damage to the system. Regulate the operations that can be executed by a subject on data and resources. Typically provided as part of operatings systems and of database management systems.

Definitions:

>[!note] NISTIR 7298
>*the process of granting or denying specific requests to:*
>1)  obtain and use information and related information processing services;
>*and*
>2) enter specific physical facilities”

>[!note] RFC 4949
>"*A process by which use of system resources is regulated according to a security policy and is permitted only by authorized entities (users, programs, processes, or other systems) according to that policy*"

### Capabilities
Takes a subject oriented approach to access control. It defines, for each subject, the list of the objects for which has non-empty access control rights, together with the specific rights for each subject.
>[!example] Example:

#### Extended access control matrix
Considers the ability of one subject to transfer rights, create another subject and to have ‘owner’ access right to that subject.

METTERE FOTO SLIDES

### Mandatory Access Control
Each subject and each object is assigned a security class. In the simplest formulation, security classes form a strict hierarchy and are referred to as **security levels**.
- A subject is said to have *security clearence* of a given level
- An object is said to have a *security classification* of a given level

The security classes control the manner by which a subject ,ay access an object

### Multilevel security (MLS)
The model defined **4** access modes:
- **read** -> the subject is allowed only to read access the object
- **append** ->the subject is allowed only write access to the object
- **write** -> the subject is allowed both read and write access to the object
- **execute** -> the subject is allowed neither read nor write access to the object but may invoke the object for execution
Confidentiality is achieved if a subject at a high level *may not convey information* to a subject at a lower level
	unless that flow accurately reflects the will of an authorized user as revealed by an **authorized declassification**

>[!note] Multilevel security confidentiality
>- **No read up**: A subject can only read an object or less or equal security level
>- **No write down**: a subject can only write into an objec of greater or equal security level

### Role-based Access Control
- Define roles and then specify access control rights for these roles, rather than for subjects directly
![[Pasted image 20251113193826.png]]
>[!note] RBAC Goals
>- Describe organizational access control **policies**
>- Based on job function
>	- A user's permissions are determined by his roles than by identity or clearence
>- Increase flexibility/scalability in policy administration 
>	- easy to meet new security requirements
>	- reduce errors in administration
>	- reduce cost of administration

![[Pasted image 20251113194123.png|600]]

Roles are defined based on job functions and permissions are defined based on job authority and responsabilities within a role. 
Users have access to objects based on the assigned role.

#### RBAC1: Role Hierarchy
Some roles subsume others:
- many operations are common to large number of roles
Thi suggests a hierarchy of roles, it reflects an organization's role structure. *Inheritance among role*