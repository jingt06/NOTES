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

---

#CHAPTER 5

---

**Impedance mismatch** between SQL and many host languages such as C or Java arises because SQL operates on *sets*, and there is no clean abstraction for sets in a host language.

Variables in a host language must first be declared between **EXRC SQL BEGIN DECLARE SECTION** and **EXEC SQL END DECLARE SECTION** commands. Once variable are declared, they can be used by prefixing the variable name with a colon (:)

**WHENEVER** command in SQL allows for easy error and exception checking after an embedded SQL statement is executed. WHENEVER checks the value of SQLSTATE for a sepcfied error. If an error has occurred, the WHENEVER command will transfer control to specified section of error handling code.

**Cursors** provided a mechanism for retrieving rows one at a time from a relation. A **curor** is the abstraction that is missing from most host languages, cuasing an **inpedance misatch**

---

**Strengths and weaknesses of the trigger mechanism**

A **triger** is a procedure that is automatically invoked in response to a specified change to the database. THe advantages of the trigger mechanism inclusde the ability to perform an action based on the result of a query condition. The set of actions that can be taken is a super set of teh actions taht integrity constraints can take. Actions can include invoking new update, or insert queries, perfomr data definition statements to create new table or views, or alter securtiy policies. Triggers can also be executed before or after a change is made to the database.

**disadvantages**: added complexity when trying to match database modifications to trigger events. Also, integrity constraints are incorporated into database performance optimization; it is more difficult for a database to perfomr automatic optimization with triggers. If database consistency is the primary goal, then integrity constraints offer the same power as triggers. Integrity constraints are often easier to understand than triggers.

---

#CHAPTER 6

---

**Cursor** enables individual row access of a relation by positioning itselfat a row and reading its content.

**Embedded SQL** refers to the usage of SQL commands within a host program 

**JDBC**stands for JAVA DataBase Connectivity and is an interface that allows a JAVA program to easily connect to any database system. 

**SQLJ** is a tool that allows SQL to be embedded directly into a JAVA program.

---

**Difference between JDB and SQLJ, Why do they both exist**

SQLJ provides embedded SQL statements. These SQL statements are static in nature and thus are preprocessed and precompiled. For instance, syntax checking and schema checking are done at compile time. JDBC allows dynamic queries that are checked at runtim. SQLJ is easier to use than JDBC and is often a better option for static queries. FOr dynamic queries, JDBC must still be used.

---

**Stored procedure and why it is useful**

Stored procedures are programs that run on the database server and can be called with a single SQL statemnt. THeyare usefull in situations where the processing should be done on the server, code writing and maintenance is simplified, because the client programs do not have to duplicate the application logic. Stored procedures can also be used to reduce network communication; the results of a stored procedure can be analyzed and kept on the database server.

---

**How JDBC/SQLJ works**

|Steps| JDBC|SQLJ|
|---|---|---|
|connect to a database|involves the creation of a **Connection object**. Parameters for the connection are specified using a JDBC URL that contains things like the network address of the database server and teh username and password for connection.| SQLJ makes calls to the same JDBC driver for connecting to a data source and uses the same type of JDBC URL|
|Start, commit, abort transactions|If the *autocommit* flag is set, each SQL statement is treated as a separate transaciton. If the flag is turned off, there is a commit() function call that will actually commit the transaction.|if *autocommit* is not set, transactions are committed by passing a **COMMIT SQL** statemnt to DBMS|
|Call a stored procedure|called from JDBC using the CallableStatement class with the SQL command {CALL *StoredProcedureName*}|SQLJ also uses Call *StoredProcedureName* to execute stored prodecures at teh DBMS|

---

**Compare execption handling and handling of warning in embedded SQLm dynamic SQL, JDBC and SQLJ**

- **Embedded SQL**: the SQLSTATE is used to check for errors after each embedded SQL statment is executed. If an error has occurred, program control is transferred to a separated statment. This is done during the precompilation step for static queries.
- **Dynamic SQL**: For dynamic SQL, the SQL statemtn can change at runtime and thus the rror handling must also occur at runtime.
- **JDBC**: In JDBC, programmers can use the try... catch syntax to handle exceptions of type **SQLExceptioin**. The **SQLWarning** class is used for problems not as severe as erros. They are not caught in the try...catch statment and must be checked independently with a getWarnings() function call.
- **SQLJ**: SQLJ uses the same mechanisms as JDBC to catch error and warnings

---

**Why do we need precompiler to translate embedded SQL and SQLJ?**

Embedded SQL and SQLJ use static queries, they allow compile-time syntax checking and schema validation. SQL statements of there types are written using a simplified syntax; the precompiler will translate that syntax into the equivalent JDBC calls. With pure JDBC, the SQL statements are fully dynamic and a preprocessor cannot be used since the SQL may change at run time.

---

#CHAPTER 16

---

**transaction**: an execution of a user program, and is seen by the DBMS as a series or list of actions. It includes reads and writes of database objects, whereas actions ain ordianry program could involve user inputm acces to network devices, user interface drawing, etc.

**Atomicity**: a transaction executes when all actions of the transaction are completed fullym or none are.

**Consistency**: Transaction begin with a 'consistent' database, and finish with a 'consistent' database. 

**Isolation**: ensures that a transaction can run independently, without considering any side effects that other concurrently running transactions might have.

**Durability**: once a transaction commits, the data should persist in the database even if the system crashes before the data is written to non-volatile storage.

**schedule**: a series of (possibly overlapping) transactions

**blind write**: writes to an object without ever reading the object

**dirty read**: transaction reads a database object without ever reading the object

**unrepeatable read**: transaction is unable to read the same object value more than once, even thought the transaction has not modified the value.

**serializable schedule**: a schedule whose effect on any consistent database instance is identical to taht of some complete serial schedule over set of committed transactions.

**recoverable schedule**: transaction can commit only after all other transactions whose changes it has read have committed.

**Avoid-cascading-aborts**: transactions only read the chagnes of committed transactions. Such a schedule is not only recoverable, aborting a transaction can be accomplished without cascading the abort to other transactions.

---

**Strict 2 parse lock** is the most widely used locking protocol where
 
1. A transaction requests a shared/exclusive lock on the object before it reads/modifies the object
2. All locks held by a transaction are releasesd when the transaction is completed

---

**Phantom problem**

Phantom problem is a situation where a strasaction retrieves a collections of objects twice but sees different results, even though it does not modify any of these objects itself and follows the strict 2PL protocol. The problem usually arises in dynammic databases where a transaction cannot assume it has locked all objects of a given type. The phantom problem will not occur if all set of objects are locked.

---

**Locking trashing** occurs when the database system reaches to a point where adding another new active transaction actually reduces throughput due to competition for locking among all active transactions. Empirically,locking trashing is seen to occur hwne 30% of active transactions are blocked.

If the number of **read-write** transcations is increased, the database system throughput will inscrease until it reaches the trashing point; then it will decrease since read-write transactions require exclusive locks, thus resulting in less concurrent execution.

If the number of read-only transaction is increased, the database system througput will also increase since read-only transactions require only shared locks. So we are able to have more concurrency and execut more transactiosn in a given tim.

**Trhoughput can be increased in three ways**

- By locking the smallest sized objects possible.
- By reducing the tiem that transaction hold locks
- By reducing hot spots, a database object that is frequently accessed and modifed.

---

**ISOLATION LEVEL**

|Level|Dirty Read| Unrepeatable read| Phaontom problem|
|---|---|---|---|
|READ UNCOMMITTED| YES|YES|YES|
|READ COMMITTED| NO|YES|YES|
|REAPEATABLE READ| NO|NO|YES|
|SERIALIZABLE|NO|NO|NO|

A **SERIALIZABLE** transaction achieves the highest degree of isolation from the effects of other transactions. It obtains locks before reading or writing objects, locks on sets of obejcts taht it requires to be unchanged and hold them until the end. Thus it is immune to all theree phenomena above.

A **REPEATABLE READ** transaction sets the same locks as a SERILIZABLE transaction, execpt that it locks only objects, not sets of objects.

A **READ COMMITTED** transaction obtains exclusive locks before writing objects and holds therse locks until the end. It also obtains shared lock before reading, but it releases it immediately. Thus it only immune to dirty read.

A **READ UNCOMMITTED** transaction can never make any lock requests, thus it is vulnerable to dirty read, unrepeatabel read nad phantom problem.

---

#CHAPTER 20

---

A **workload description** include the following

- A list of queries and their frequencies
- A lsit of updates and their frequencies
- Performance goals for each type of query and update

---

**GUILDELINES**

1. Whether to Index (guildeline 1): Do not build an index unless some query include the query components of updates benefits from it. Whenever possiblem choose indexes that speed up more than one query
2. Choice of search key (guildeline 2): Attributes mentioned in WHERE clause are candidate for index
   -  an exact-match selection condition suggests hash index
   -  range sleection suggests B+ tree
3. Multi-Attribute Seach Key (guildeline 3) indexes with multiple-attribute search keys should be consided in following two situations
   - WHERE clause includes conditions more than one attributes of a realtion
   - enable index-only evaluation strategies
4. Whether to Cluster (guideline 4) At most one index on a given relation can be clustered, and clustering affects performance greatly. Choice of clustered index is important
   - do not cluster if a index only evaluation can be enabled
   - range queries are likely to benefit the most from clustering
5. Hash VS Tree Index (guildline 5) A B+ tree index is usually perferable because it supports range queries as well as equality queries. A hash index si better in the following situations:
   - The index is intended to support index nested loops join
   - There is very important equality query and no range queires  involving the search key attributes
6. Balancing the Cost of Index Maintenance (guildline 6) consider the impact of each index on the updates in the workload
   - if maintaning an index slows down frequent update operations, consider dropping the index.
   - however, adding an index may speed up a gien update operation.