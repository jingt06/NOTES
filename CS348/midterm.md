##Chapter1 
###The advantages of using a DBMS:
- **Data independence and efficient access**: database application programs are independent of the details of data representation and storge
- **Reduced application development**: DBMS provides several important functions required by applications
- **Data integrity and security**: powerful access control mechanism
- **Data administration**
- **Concurrent access and crash recovery**:supports the notion of a **tranction**

###level schema-	External Schemas – what the programs/user sees, may differ for each user   - 	“fake” schemas for abstraction to users, tables don’t actually exist-	Conceptual Schema – description of logical structure of all data in database   -	Tables and their columns-	Physical Schema – description of physical aspects, files, devices, algorithms, etc. How the data will actually be stored

###Logical VS Physical data independency
- Logical data independence means that users are shielded from changes in the logical structure of the data
- Physical data independence insulates users from changes in the physical storage of the data

###Responsibilities of a DBA
- Designing the logical and physical schemas, as well as widely-used portions of the external schema
- Security and authorization
- Data availability and recovery from failures
- Data tuning

##Chapter 3
- **Relation Schema** is a basic information describing a *table* or *relation*. Include a set of column names and the data type, eg:
   - Relation_name(col1:string, col2: int, col3 real)
   - Students(sid:string, name: string, login:sting, age:integer, gpa:real)
- **Relational Database Schema** is a collection of relation schemas, describing one or more relations
- **Domain** is synonymous with *data type*
- **Attributes** columns in a tble
- **A Relation Instance** is a set of tuples (aka *rows*, *records*) that each conform to the schema of the relation. 
- **Relation Cardinality** is the number of tuples in the relation.
- **Relation Degree** is the number of fields (or *columns*) in the relation.

