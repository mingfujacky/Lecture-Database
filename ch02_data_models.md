---
marp: true
theme: default
class: default
size: 16:9
paginate: true
footer: 國立陽明交通大學 電子與光子學士學位學程
headingDivider: 1
style: |
  section::after {
    content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
  }
  
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .columns img {
    width: 50%;
  }
  .middle-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .middle-grid img {
    width: 75%;
  }
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }
  .grid img {
    width: 100%;
  }
  .red-text {
    color: red;
  }
  
  .blue-text {
    color: blue;  
  }

  .brown-text {
    color: brown;  
  }

  .small-text {
    font-size: 0.75rem;
  }
---
# Chapter 2: Data Models
- Data modeling is to build data models, which is the <span class="brown-text">first step</span> in the database design journey, serving as a <span class="brown-text"> bridge</span> between real-world objects and the computer database.
- One big problem of database design is that designers, programmers, and end users see data in different ways, which introduce <span class="brown-text">misunderstanding</span> and increase communication cost.
- <span class="brown-text">Database designers </span>must obtain a precise description (<span class="brown-text">data model</span>) of the data's nature and environments within the organization to reduce communication efforts.

# Data Modeling and Data Models
- Data modeling refers to the <span class="brown-text">process</span> of creating a specific data model for a determined problem domain (mini-world). 
- Data modeling is an iterative, progressive process.
- A <span class="brown-text">data model</span> is a relatively simple representation of more complex real-world objects
  - Entity (objects of interest)
  - Attribute (properties of entity)
  - Relationship (linkage between entities)
  - Constraint (restriction on data)
- A data model is a <span class="brown-text">communication tool</span> between end users and database designers, and between database designers and programmers.

# The Importance of Data Models
- Data models are a <span class="brown-text">communication tool</span>
  - End users know the business rule running in real world
  - Developers develop aps to manage data and transform data into information
  - People view data in different ways
    - Managers want a universal view of data
    - Staffs need details of data
- A good database system environment requires an overall database design based on an appropriate data model
- No appropriate data model, no good database system environment

# Data Model Basic Building Blocks
- An <span class="brown-text">entity</span> is a person, thing or event about which data will be collected and stored
- An <span class="brown-text">attribute</span> is a characteristic (property) of an entity
- A <span class="brown-text">relationship</span> describes an association among entities
  - One-to-many (1:M or 1..*): PAINTER paints PAINTING
  - Many-to-many (M:N or \*..\*): EMPLOYEE learn SKILL
  - One-to-one (1:1 or 1..1): EMPLOYEE manage STORE
- A <span class="brown-text">constraint</span> is a restriction placed on the data to help data integrity
  - An employee’s salary must have values between 6,000 and 350,000
  - Each class must have one and only one teacher

# Business Rules
- A **business rule** is a brief, precise, and unambiguous description of a policy, procedure, or principle within a specific organization
  - made from company managers, policy makers, department managers, and written procedures
  - used to define entities, attributes, relationships, and constraints
- Example: 'A customer may generate many invoices' may be translated into data model
  - Customer and invoice are objects of interest and should be represented by respective <span class="brown-text">entities</span>
  - There is a **'generate'** <span class="brown-text">relationship</span> between customer and invoice
  - The generate relationship is one-to-many (1:M)

# The Evolution of Data Models
Data models represent a lot of thought as to what a database is, what it should do, the types of structures that it should employ, and the technology that would be used to implement these structures
![bg right:55% w:700 data models evolution](files/image/CFig02_05.jpg)

# Hierarchical Models
- The hierarchical model organizes the data into a tree structure which consist of a single root node where each record is having a parent record and many child records and expands like a tree
![bg right:50% w:600 hierarchical models](files/image/hierarchical_model.png)

# Network Models
- In the network model, the user perceives the network database as a collection of records in 1:M relationships. However, unlike the hierarchical model, the network model allows a record to have more than one parent.
![bg right:50% w:600 network model](https://media.geeksforgeeks.org/wp-content/uploads/20200727113000/network.png)

# Relational Model
The relational model’s foundation is a mathematical concept known as a relation, which is introduced by Edgar F. Codd in 1969.
- Relation: a table with columns and rows.
- Attribute: a named column of a relation.
- Domain: the set of allowable values for one or more attributes.
- Tuple: a row of a relation
![bg right:40% w:500 relational model](https://www.w3schools.in/wp-content/uploads/2016/08/Relational-Model-Terms.png?ezimgfmt=rs:503x343/rscb53/ng:webp/ngcb52)

# Relational Diagram

<style>
.grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}
.grid img {
    width: 100%;
}
</style>

<div class="grid">
    <img src="files/image/CFig02_01.jpg" alt="Linking relational tables">
    <img src="files/image/CFig02_02.jpg" alt="A relational diagram">
</div>

# Relational Model Terminology
- Relation schema
- Relational database schema
- Degree of a relation
- Cardinality of a relation
- Relation state (or relation instance)
[![Relational model terminology](https://i.ytimg.com/vi/Q45sr5p_NmQ/mqdefault.jpg)](https://youtu.be/Q45sr5p_NmQ?si=cr53etNXoX1BIpLf)

# Entity Relationship Model
- Although the relational model was a vast improvement over the hierarchical and network models, it still lacked the features that would make it an effective database design tool.
- Database designers prefer to use a graphical tool in which entities and their relationships are pictured.
- The <span class="brown-text">**entity relationship model (ERM)**</span> using *graphical representations* to model database components has become a widely accepted standard for data modeling.
- The relational data model and ERM combined to provide the foundation for tightly structured database design

# Entity Relationship Model Notation
- Entity – an entity is represented in the ERD by a rectangle (entity box)
- Attributes – each entity consists of a set of attributes that describes particular characteristics of the entity
- Relationships – relationships describe associations among data
![bg right:50% w:600 ER model](files/image/CFig02_03.jpg)

# Crow's Foot Notations
![bg right:50% w:600 Crow's Foot notation](https://discourse.omnigroup.com/uploads/default/original/2X/5/54b713a5fe9dc79b458b8afe1a5a148320ba132d.gif)

# Semantic Model
- The semantic data model organizes the data based on the meaning and logical relationships of real-world objects, which consists of entities and attributes where each record is connected by descriptive links and expands like a network of information.
![bg right:50% w:150% semantic model](https://www.gooddata.com/img/blog/_2000xauto/semantic-data-model-example.png.webp)

# Object-Oriented Model
In the object-oriented data model (OODM), both data and its relationship are contained in a single structure known as an object
- **Object**: an abstraction of a real-world entity
- **Attributes**: describe the properties of an object
- **Method**: represents a real-world action
- **Class**: a collection of similar objects with shared structure and behavior
- **Inheritance**: an object within the *class hierarchy* to inherit the attributes and methods of the classes above it. (class EMPLOYEE and CUSTOMER can be created as subclasses inherit from the class PERSON)
- OODM are typically depicted using Unified Modeling Language (UML) class diagrams

# OODM Diagram
![bg right:70% w:100%](files/image/CFig02_04.jpg)

# ERDM and O/R DBMS
- The extended relational data model (ERDM) adds many of the OO model’s features within the simpler relational database structure
- A DBMS based on the ERDM is an object/relational database management system (O/R DBMS)

# Comparison of RDBMS, OODBMS and O/R DBMS
<style scoped>
table {
  font-size: 20px;
}
</style>
Feature	|RDBMS|	OODBMS|	O/R DBMS
--------|------------------|--------------------------|-------------------
Tables & SQL	|✅ Yes	|❌ No|	✅ Yes
Objects & Classes	|❌ No	|✅ Yes|	✅ Yes
Inheritance	|❌ No|	✅ Yes|	✅ Yes
Encapsulation (Methods in DB)|	❌ No|	✅ Yes|	✅ Yes
Complex Data Types	|❌ No|	✅ Yes|	✅ Yes

Products of O/R DBMS
- <span class="small-text">PostgreSQL (most commonly used O/R DBMS)</span>
-	<span class="small-text">Oracle Database (with Object-Relational Features)</span>
- <span class="small-text">Microsoft SQL Server (limited Object-Relational capabilities)</span>

# Emerging Data Models: Big Data and NoSQL
- **Big Data** refers to a movement to find new and better ways to manage large amounts which DBMS can not manage
- Big Data characteristics (3 Vs) : volume, velocity, and variety
- NoSQL database is a large-scale distributed **database system** that stores unstructured and semi-structured data in efficient ways

# NoSQL Databases
- Schemaless
- Horizontal scalability
- Distributed data store
- Lower cost
- Non-relational
- Handle large volume of data

# RDBMS (Relational DBMS) vs NoSQL
|RDBMS|NoSQL
|-----|-----
|Structured data with a rigid schema | Unstructured, Semi-structured data with a flexible schema
|Storage in rows and columns | Data are stored in Key/Value pairs database, Columnar database, Document database, Graph Database.
|Scale up|Scale out
|SQL server, Oracle, mySQL|MongoDB, HBase, Cassandra
|SQL language|Solution-specific method

# Degrees of Data Abstraction
- External, Conceptual, Internal and Physical levels
  ![bg right:50% w:600 data abstraction levels](files/image/CFig02_06.jpg)

# External Model
- The end users’ view of the data environment
- Use **ER diagrams** to represent the external model
- The external views represent **subsets** of the database
  - Easy to scope and communicate specific data required to support targeted end users
  - Ensure **security** constraints in the database design
  ![bg right:40% w:500 external model](files/image/CFig02_07.jpg)

# Conceptual Model
- A **global view** of the entire database by the entire organization
- Use **ER diagrams** to represent the conceptual model
- Identify and high-level describe main data objects
- Independent of both software and hardware
- The term **conceptual design** refers to creating a conceptual data model by ER diagrams
  ![bg right:40% w:500 conceptual model](files/image/CFig02_08.jpg)

# Internal Model
- Use the database constructs of the chosen DBMS to match the conceptual model’s characteristics and constraints to build the internal model
- The term **logical design** refers to creating a logical data model by a set of SQL statements
- Software dependent and hardware independent
![bg right:40% w:500 internal model](files/image/CFig02_09.jpg)

# Physical Model
- Operates at the lowest level of abstraction, describing which physical storage device the data is saved and how to access the data
- The term **physical design** refers to define data storage organization, security control, performance measure
- Both software and hardware dependent

# Levels of Data Abstraction 
![bg right:65% w:800 internal model](files/image/CTable02_04.jpg)

# Relational Model vs Entity Relationship Model
ER Model first, then converted into Relational Model for DBMS implementation.

|Aspect	| ER Model	| Relational Model
|-------|-----------|-----------------
Used For|	Conceptual database design|	Logical database implementation
Representation|	ER Diagram (graphical)|	Tables (relational schema)
Elements|	Entities, Attributes, Relationships|	Tables, Attributes, Tuples
Constraints|	Cardinality in ER Diagram|	Primary/Foreign keys, SQL constraints
Conversion|	Converted to Relational Model|	Implemented in DBMS

# Naming Conventions
- Names should be descriptive and familiar to the users
- A good naming convention can 
  - Make less confusion and reduce errors
  - Promote code consistently and readability 
- Follow organization practice or develop at the start of project by considering
  - Should table name and column name be singular or plural? (student or students)
  - Should prefix tables or columns? (name or prod_name)
  - Should use capital letters for naming? (cap_cap, capCap or CapCap)
  - Which terminology should be selected? (user, person or people)

# Supplement - Naming Conventions
[![Udemy Video of naming conventions](https://i.ytimg.com/vi/xFs8H_YHqHc/mqdefault.jpg)](https://youtu.be/xFs8H_YHqHc?si=2m55anO7oxjQ6a8h)
[Naming conventions of MySQL](https://medium.com/@centizennationwide/mysql-naming-conventions-e3a6f6219efe)

# Review Questions
- Why data models are important?
- What are the data model basic building blocks
- How have the major data models evolved
- Explain NoSQL characteristics
- What are the four levels of data abstraction
- Which of the following is NOT a type of data models?
A. Relational Model
B. Hierarchical Model
C. Waterfall Model
D. NoSQL Model

# Homework #A
資料庫課程作業(A)
