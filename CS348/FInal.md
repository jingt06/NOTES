#CHAPTER1
---

A database is an integrated collection of data, usually so large that it has to be stored on secondary storage devices such a disks or tapes

---

The advantages of using a DBMS are:

- Data independendce and efficient access
- Reducd application development time 
- Data integrity and security
- Data administration
- Concurrent access and crash recovery

---

Difference between logical and physical data independence

Logical data independence means that users are shileded from changes in the logical structure of the data, while physical data independece insulates users from changes in hte physical storage of the data.

---

Difference between exteranl, internal, and conceptual schemas.

- External schemas allows data access to be customized and authorized at the level of individual users or groups of users. 
- Conceptual (logical) schemas describes all the data taht is actually stored in the database.
- Internal (physical) schemas summarize how the relations described in the conceptual schema are actually stored on disk.

---

Responsibilities of a DBA

- Dsigning the logical and physical schemas, as well as widely-used portions of the external schema.
- Security and authorization
- Data availability and recovery fro failures
- Database tuning: The DBA is responsible for evolving the database, in particular the conceptual and phsical schemas, to ensure adequate performance as user requirements chagne

---

#CHAPTER 2

---

**Attribute**: a property of description of an entity

**Domain**: a set of possible values for an attribute

**Entity**: an object in the real world that is distinguishable for the other objects.

**Relationship**: an association among two or more entities

**One-to-many relationship**: a key constraint that indicates that one entity can be associated with many of another entitty.

**Many-tmany relationship**: a key constraint that indicates that many of one entity can be associate with many another entity.

**Participation constraint**: a participation constraint determines whether relationships must envolve certain entities. A **total participation constraint** says that ever A has a B. A ** partial participation constraint** says that every A does not have to be a B.

**Overlap constraint**: within an ISA hierachy, an overlap constraint determines whether or not two subclasses can cotain the same entity.

**Covering constraint**: whithin an ISA hierachy, a covering constraint determines where the entities in the subclasses collectively include all entities in the superclass.

**Weak entity set**: an entity that cannot be identified uniquely without considering some primary key attributes of another identifying owner entity,

**Aggregation**: a feature of the entity relationship model that allows a relationship set to participate in another idntifying owner entity.

**Role indicator**: If an entity set plays more than one role, role indicators describe the different purpose in the relationship.

---

#CHAPTER 3

---
**Relation schema**: a relation schema can be thought of as the basic information describing a table or relation. This includes a set of colum names, the data types associated with each column, and the name associated with the entire table.

**Relational database schema**: a relation database schema is a collection of relation schemas, describing one or more relations.

**Domain**: is synonymous with data type. 

**Attribute**: colums in a table.

**Attribute domain**: data type associated with a column.

**Relation instance**: a set of tuples (rows or records) that each conform to the schema of the relation

**relation cardinality**: number of tuples in the relation

**relation degree**: number of fields (columns) in the relation

---
**Primary key, candidate key and superkey**

THe **primary key** is the key selected by the DBA fro among the group of **candidate keys**, all of which uniquely identify a tuple. A **superkey** is a set of attributes that contains a key.

---

**foreign key constraints and referential integrity**

A **foreign key** constraint is a statement of the form that one or more fields of a relation, say R, together **refer** to a second relatino, say S. THat is, the values in these fields of a tuple in R are either **null**, or uniquely identify some tuple in S. Thus, these fields of R should be a key.

**foreign key constraints** are important because they provide safeguards for insuring the integrity of data. Users are alerted/thwarted when thery try to do something that does not make sense. This can help minimize errors in application programs or in data-entry.

**Referential integrity** means all foreign key constraints are enforced.

---

#CHAPTER 4
---

Every operator in relational algebra accepts one or more relaton instances as arguments and the result is always an relations instance. So the argument of one operator could be the result of another operaotor. This is important because, this makes it easy to write complex queries by simply composing the relational algebra operators.

---

**Relational completeness** means that a query language can express all the queries that can be expressed in relational algebra. It does not mean that the language can express any desired query.

---

An **unsafe** query is a query in relational calculus that has an infinite number of resutls.