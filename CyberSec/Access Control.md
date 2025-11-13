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

