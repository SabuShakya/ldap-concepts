# LDAP CONCEPTS #

## What is LDAP ? ##
 
LDAP-the Lightweight Directory Access Protocol is a set of protocol used for accessing and modifying centrally stored 
information over a network. It is a mature, flexible,and well-supported standards-based mechanism for interacting with 
[directory servers](#directory-serverhttpsldapcomdirectory-servers). It’s often used for authentication and storing information about users, groups, and applications.
This is used predominantly by applications for resource information lookup.

Unlike traditional databases, an LDAP database is especially suited for read, search, and browse operations instead of
write operations. It is with reads that LDAP shines.  
When you have a task that requires “write/update once, read/query many times”, you might consider using LDAP.
LDAP is designed to provide extremely fast read/query performance for a large scale of dataset. Typically, you want
to store only a small piece of information for each entry. The add/delete/update performance is relatively slower
compared with read/query because the assumption is that you don’t do “update” that often.

![Alt text](./images/ldap1.png?raw=true "Title")
[Image Reference](https://youtu.be/lp5z8HQGAH8)

## Why LDAP ?? ##

- **LDAP is lightweight**. LDAP messages are encoded with ASN.1 BER, which is a compact binary format that is very 
  efficient to encode and decode. It’s much more streamlined than something like JSON or XML over HTTP. 
  LDAP uses persistent connections for communication with a directory server(can live for hours or days or longer) 
  while other protocols use relatively short-lived connections. This can make a big difference when it comes to 
  performance and scalability because establishing a new connection is significantly more expensive than using
  one that’s already available.
  
- **LDAP is Secure**. It includes a great deal of password policy functionality, like strong encoding mechanisms 
  and constraints that can prevent users from selecting weak passwords, but it also includes support for a variety 
  of authentication types through SASL (the simple authentication and security layer), including the possibility 
  of two-factor options through mechanisms like one-time passwords. On top of that, directory servers typically 
  provide support for fine-grained access controls that restrict which entries, attributes, and values any 
  individual user can access, and in what ways.

## Uses ##
- LDAP can serve as a complete identity management solution for an organization. It can provide authentication
  and authorization services for users
- LDAP can be used to provide “yellow pages” services for an organization (for instance, users’ or employees’ 
  contact information—phone numbers, addresses, departments, and so on)
- The information stored in DNS records can be stored in LDAP. 
- User/System Groups
- Address book
- Organization Representation
- Asset Tracking
- Telephony Information Store
- User resource management
- E-mail address lookups
- Application Configuration store


## [Directory Server](https://ldap.com/directory-servers/) ##
- A Directory System Agent, or a DSA, is a type of network database that stores information represented as trees of entries.
- A directory is a specialized database specifically designed for searching and browsing, in additional to 
  supporting basic lookup and update functions.
- A server for storing resource specific information, to lookup for information.
- A directory service is a customizable information store that functions as a single point from which users can locate
  resources and services distributed throughout the network. This customizable information store also gives
  administrators a single point for managing its objects and their attributes.
  
## Basic LDAP Concepts ##

### DIT(Data Information Tree) ###
The LDAP server stores the information in a hierarchical (or a tree) form. This tree of data is the Data Information Tree.

![DIT](./images/DIT.png?raw=true "DIT")

### Entries ###
- As trees have nodes, the nodes in the DIT are called entries. 
- The information that is stored within the entry is in the form of a key-value pair. Each entry has one parent entry 
  (except for the root entry) and zero or more child entries. A child entry is a sibling of its parent’s other child entry.
- Collection of information about an entity.Each entry consists of three primary components: a distinguished name, 
  a collection of attributes, and a collection of object classes. 

Example:
![ENTRY](./images/entree.png?raw=true "Entry")

### DN(Distinguished Name) ###
- An entry’s distinguished name, often referred to as a DN, uniquely identifies that entry and its position in the 
  directory information tree (DIT) hierarchy. The DN of an LDAP entry is much like the path to a file on a filesystem.
- Generally, it is a string consisting of one or more comma-separated key-value pairs, which together uniquely 
  distinguish the node (entry) in the tree. For example, the string dc=sabu,dc=com could be the DN for the root entity.

### RDN(Relative distinguished Name) ###
- An LDAP DN consists of zero or more elements called relative distinguished names, or RDNs. Each RDN consists of 
one or more (usually just one) attribute-value pairs. For example, “uid=john.doe” represents an RDN composed of 
an attribute named “uid” with a value of “john.doe”. If an RDN has multiple attribute-value pairs, they are 
separated by plus signs, like “givenName=John+sn=Doe”.
- A string that uniquely distinguishes the entity relative to its parent is called a relative distinguished name. 
The DN uniquely identifies the entity globally, while the RDN uniquely identifies the entity among its siblings.
  
### Object Classes ###

- Object classes are schema elements that specify collections of attribute types that may be related to a particular 
  type of object, process, or other entity.
- Every entry has a structural object class, which indicates what kind of object an entry represents (e.g., whether it is 
  information about a person, a group, a device, a service, etc.), and may also have zero or more auxiliary object 
  classes that suggest additional characteristics for that entry.
- The object class is considered a container for attributes, and it will control what types of attributes can be 
  added to the entity.
  
![OBJECT CLASSES](./images/objectClass.png?raw=true "ObjectClass")

### Attributes ###

- It holds the data for entry. Each attribute has an attribute type, zero or more attribute options, and a set of
  values that comprise the actual data.
- All attributes must have an object identifier(OID) and zero or more names that can be used to reference
  attributes of that type. 
  
|Attribute Name |Alias Name |Description |Object Class|
|:---|:---|:---|:---|
|dc |domainComponent | Any part of a domain name; for example, domain.com, domain, or com |dcObject |
|o |organizationName |Organization name |organization |
|ou |organisationalUnitName |Department or any subgroup | organizationUnit |
|cn |common name | Name of the entity |person, organizationalPerson, organizationalRole, groupOfNames, applicationProcess, applicationEntity, posixAccount, device |
|sn |surname | Surname or family name |person |
|uid |userid | Username or other unique value |person, organizationalPerson, organizationalRole, groupOfNames, applicationProcess, applicationEntity, posixAccount, device |
|userPassword |- |User password for some form of access control | organization, organizationalUnit, person, dmd, simpleSecurityObject, domain, posixAccount |

![Attribute](./images/img.png?raw=true "attribute")

### LDAP Data Interchange Format (LDIF) ###
This is an ASCII file format to describe the hierarchical tree structure of LDAP data in the form of a text file.
LDAP data can be imported or exported in an LDIF file format.

### Schemas ###
A collection of rules that determines the structure and contents of the directory. The schema contains the attribute 
type definitions, objectClass definitions, and other information.
![Schemas](./images/schemas.png?raw=true "Schemas")

![Schemas](./images/schema1.png?raw=true "Schemas")

### DIT Structures Example ###
![DIT Structures](./images/DITStructure2.png?raw=true "DIT Structures")
![DIT Structures](./images/DITStructure1.png?raw=true "DIT Structures")

reference:https://learning.oreilly.com/library/view/spring-50-projects/9781788390415/7c5d9fee-7fdf-4233-b377-29c1d0d951d0.xhtml

### Placing Entries within the DIT ###

- Upon creation, each new entry must “hook into” the existing DIT by placing itself as a child of existing entry.
- Typically, the top-most entry is simply used as a label indicating the organization that the DIT is used for.
- These entries can be of whatever objectClasses desired, but usually they are constructed using domain components 
  (dc=example,dc=com for an LDAP managing info associated with example.com), locations (l=new_york,c=us for an 
  organization or segment in NY), or organizational segments (ou=marketing,o=Example_Co).
- Entries used for organization (used like folders) often use the organizationalUnit objectClass, which allows
  the use of a simple descriptive attribute label called ou=. These are often used for the general categories 
  under the top-level DIT entry (things like ou=people, ou=groups, and ou=inventory are common).

### Naming and Referencing Entries within the DIT ###
- Each entry must have an attribute or group of attributes that is unambiguous at its level in the DIT hierarchy 
  as we refer to entries by their attributes.
  
![RDNS](./images/RDNs.png?raw=true "RDNS")

### LDAP Inheritance ###
- LDAP system relates to one another is a matter of hierarchies, inheritance, and nesting.

![ObjectClassInheritance](./images/objectClassInheritance.png?raw=true "ObjectClassInheritance")
![AttributeInheritance](./images/attributeinheritance.png?raw=true "AttributeInheritance")

### LDAP Protocol Variations ###

LDAP is actually just the protocol that defines the communication interface for working with directory services.
- `ldap://` : This is the basic LDAP protocol that allows for structured access to a directory service.
- `ldaps://` : This variant is used to indicate LDAP over SSL/TLS. Normal LDAP traffic is not encrypted, although 
  most LDAP implementations support this. This method of encrypting LDAP connections is actually deprecated, and
  the use of STARTTLS encryption is recommended instead. If you are operating LDAP over an insecure network, 
  encryption is strongly recommended.
- `ldapi://` : This is used to indicate LDAP over an IPC. This is often used to connect securely with a local LDAP 
  system for administrative purposes. It communicates over internal sockets instead of using an exposed network port.

### Client/Server Model ###

![ClientServer](./images/clientserver.png?raw=true "ClientServer")

### Installing OpenLDAP ###
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04

### References ### 
- https://learning.oreilly.com/library/view/spring-50-projects/9781788390415/db32020a-1a14-44fb-b820-f202c693458b.xhtml
- Understanding the LDAP Protocol, Data Hierarchy, and Entry Components | DigitalOcean
- https://dzone.com/articles/spring-ldap
- https://dzone.com/articles/spring-data-ldap-part-2
- LDAP with spring boot security
  - https://www.youtube.com/watch?v=-wDUChgvYgU&ab_channel=JavaBrains
  - https://spring.io/guides/gs/authenticating-ldap/

For Code: https://github.com/SabuShakya/spring-ldap-crud-auth


