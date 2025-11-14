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
Thi suggests a hierarchy of roles, it reflects an organization's role structure. *Inheritance among roles.*
![[Pasted image 20251113194724.png|500]]

#### RBAC2: constraints
Provide a means of adapting RBAC to the specifics of administrative and security policies of an organization.
A defined relationship among roles or a condition related to roles.
Types:
- *Mutually exclusive roles*
- *Cardinality*
- *Prerequisite roles*

>[!note] Mutually exclusive roles
> A user can only be assigned to one role in the set (either during session or statically)
>.Any permission (access right) can be granted to only one role in the set.

>[!note] Cardinality
>Setting a maximum number with respect to roles

>[!note] Prerequisite roles
>Dictates that a user can only be assigned to a particular role if it is already assigned to some other specified role.

## Attributes-Based Access Control (ABAC)
Can define authorizations that express conditions on properties of both the resource and the subject. Strength is its flexibility and expressive power. Main obstacle to its adoption in real systems has been concern about the performance impact of evaluating predicates on both resource and introduction of the *eXtensible Access Control Markup Language (XAMCL)*.
There is considerable interest in applying the model to cloud services.

#### Attributes

>[!note] Subject attributes
>A subject is an active entity that causes information to flow among objects or changes the system state.
>Attributes define the identity and characteristics of the subject

>[!note] Object attributes
>An object (or resource) is a passive informarion system-related entity containing or receiving information.
>Objects have attributes that can be leveragess to make access control decisions.

>[!note] Enviroment attributes
>Describe the operational, technical and even situational enviroment or context in which the information access occurs.
>These attributes have so far been largely ignored in most access control policies.

Distinguishable because it controls access to objects by evaluating tules against the attributes of entities, operations, and the environment relevant to a request.

Relies upon the evaluation of attributes of the subject, attributes of the object, and a formal relationship or access control rule defining the allowable operations for subject-object attribute combinations in a given environment.

Systems are capable of enforcing DAC, RBAC, and MAC concepts. Allows an unlimited number of atttributes to be combined to be vombined to satisfy any access control rule.

>[!note] ABAC Policies
>A policy is a set of rules and relationships that govern allowable behavior wihtin an organization, absed on the privileges of subjects and how resources or objects are to be protected under which environment conditions.
>- Typically written from the perspective of the object that needs protecting and the privileges available to subjects.
>Privileges represent the authorized behavior of a subject and are defined by an authority and embodied in a policy.
>- Other terms commonly used isntead of privileges are: rights, authorizations and entitlements.

>[!note] ABAC vs RBAC
>In RBAC as the number of attributes increases to accomdate finer grained policies, the number roles and permissions **grows exponentially**
>$\displaystyle\prod_{k =1}^{k}\text{Range}(SA_{k})\text{ and } \prod^{M}_{m=1}\text{Range}(SA_{m})$
>
>The ABAC model deals with additional attributes in an efficient way.

>[!note] Finer grained policy example 
>