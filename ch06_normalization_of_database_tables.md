---
marp: true
theme: default
class: 
size: 16:9
paginate: true
footer: 國立陽明交通大學 電子與光子學士學位學程
headingDivider: 1
style: |
  section::after {
    content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
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
    color: lightskyblue;  
  }

  .brown-text {
    color: brown;  
  }

  .small-text {
    font-size: 0.80rem;
  }
---
# Chapter6: Normalization of Database Tables
- Good database design must be matched to good table structures. 
- Learn to evaluate and design good table structures to **control data redundancies** thereby avoiding data anomalies.
- The process that yields such desirable results is known as **normalization**.

# Self-Taught Resource
https://www.databasestar.com/mysql-database/
https://www.databasestar.com/database-design/
https://www.databasestar.com/programmer-jokes/
https://www.databasestar.com/vip/
https://youtube.com/@decomplexify?si=I5sEMNUZOJcSpiCX


# Database Tables and Normalization
- <span class="blue-text">**Normalization**</span> is a process for adjusting table structures to <span class="brown-text">**minimize data redundancies**</span> 
  - Reduce data anomalies
  - Assigns attributes to tables based on functional dependency
- Normalization goes through a series of stages called normal forms
![bg right:50% w:100%](https://www.c-sharpcorner.com/UploadFile/nipuntomar/normalization-and-its-types/Images/Norm.gif)

# Why Normalize a Database
- Prevent the same data from being stored in more than one place (insert anomaly)
- Prevent updates being made to some data but not others (update anomaly)
- Prevent data not being deleted when it is supposed to be, or from data being lost when it is not supposed to be (delete anomaly)
- Ensure the data is accurate
- Reduce the storage space that a database takes up
- Ensure the queries on a database run as fast as possible

# Data Redundancies Issues - A Sample Table
<style scoped>
table {
  font-size: 20px;
}
</style>
Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry

- Attributes: student names, paid fees, registered classes
- It is not a normalized table, and there are a few issues with this

# Data Redundancies Issues - Insert Anomaly
- If we want to add a new student but did not know their course name
<style scoped>
table {
  font-size: 20px;
}
</style>
Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry
5|Jared Oldham|0|?

- We would be adding incomplete data to our table, which can cause issues when trying to analyze this data.

# Data Redundancies Issues - Update Anomaly
- If the class Biology 1 was changed to “Intro to Biology”. We would have to query all of the columns that could have this Class field and rename each one that was found.

<style scoped>
table {
  font-size: 20px;
}
</style>
Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry

- There’s a risk that we miss out on a value, which would cause issues.
- Ideally, we would only update the value once, in one location.

# Data Redundancies Issues - Delete Anomaly
- If Susan Johnson quits and her record needs to be deleted from the system. We could delete her row

<style scoped>
table {
  font-size: 20px;
}
</style>
Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
**3**|**Susan Johnson**|**400**|**Medicine**|**Biology 2**		
4|Matt Long|850|Dentistry

- But, if we delete this row, we lose the record of the Biology 2 class, because it’s not stored anywhere else. The same can be said for the Medicine course.
- We should be able to delete one type of data or one record without having impacts on other records we don’t want to delete.

# A Sample Report Layout
![bg right:70% w:90%](files/image/CTable06_01.jpg)

# Poor Table Structure
![bg right:60% w:90%](files/image/CFig06_01.jpg)
- Data inconsistency
- Difficult to update
- Data redundant

# Enough Normalization
- From a structural point of view, higher normal forms are better than lower normal forms
- For most purposes in business database design, 3NF is as high as you need to go in the normalization process
- Denormalization produces a lower normal form to increase performance but greater data redundancy

# The Need for Normalization
- Database designers commonly use normalization in the following two situations:
  - When designing a new database structure
  - To analyze the relationship among the attributes within each entity and determine if the structure can be improved through normalization
- The main goal of normalization is to eliminate data anomalies by eliminating unnecessary <span class="blue-text">data redundancies</span>
- Normalization uses the concept of <span class="blue-text">functional dependencies, FD</span> to identify which attribute determines other attributes

# The Objectives of Normalization
- Each table represents a single subject
- Each row/column intersection contains only one value and not a group of values
- No data item will be unnecessarily stored in more than one table.
- Data is updated in only one place
- All non-prime attributes in a table are dependent on the primary key
- Each table has no insertion, update, or deletion anomalies
- Ensure that all tables are in at least in 3NF in business environment
- Work one table at a time, identifying FD of a table

# Normal Forms
![bg right:70% w:100%](files/image/CTable06_02.jpg)

# Normalization Base: Functional Dependency (FD)
- Normalization starts by identifying **functional dependencies** of a given table
- <span class="blue-text">FD X&rarr;Y</span>: the values of Y are determined by the values of X. (X, Y is a set of attributes)
- <span class="blue-text">X&rarr;Y is full FD </span>, if no attribute can be removed from X and still keep the dependency.
- Example: 
  - PROJ_NUM → PROJ_ NAME (read as PROJ_ NUM functionally determines PROJ_NAME)
  - Attribute PROJ_NUM is known as the determinant attribute
  - Attribute PROJ_NAME is known as the dependent attribute.

# FD Type: Partial Functional Dependency
When there is a FD in which the determinant is only part of the PK
- <span class="blue-text">X&rarr;Y is a partial FD </span> if X is a subset of PK.

Example
- Give a table having PK (A, B), there is a FD (B &rarr; C), we say it is a partial FD because B is a subset of PK 

# FD Type: Transitive Functional Dependency
When a attribute is dependent on another attribute which is not part of PK
- Transitive FD is more difficult to identify among a set of data
- They occur only when a FD exists among non-prime attributes
Example
- Given primary key: X, there are two FDs X → Z and X → Y
- After investigating, we find that there is a FD Y → Z, which can support X determine Z because (X → Y) + (Y → Z) can make (X → Z) that is, x can determine the value of Z via Y. 
- Y → Z signals that there is a <span class="blue-text">transitive FD</span> because Y is not a PK.

# Why Do We Do Database Normalization?
![bg right:70% w:100%](https://cdn.hackr.io/uploads/posts/attachments/1666888816mdnYlrMoEE.png)

# Conversion to First Normal Form (1NF)
A table in 1NF means
- All key attributes are well defined 
- There are no repeating groups
- All attributes are dependent on the primary key

Converting to 1NF starts with three steps
1. Eliminate the repeating groups 
2. Identify the primary key 
3. Identify all dependencies

# Conversion to First Normal Form (1NF) - Supplement
- Row order do not convey any information
- There is no mixed data types within a column

# 1NF Step1 - Eliminate Repeating Groups
Repeating group: a group of entries existing for a single key value

<div class="grid">
    <img src="files/image/CFig06_01.jpg" alt="">
    <img src="files/image/CFig06_02.jpg" alt="">
</div> 

# 1NF Step2 - Identify PK 
PK: an identifier composed of one or more attributes that uniquely identifies a row
<span class="brown-text">PROJ_NUM + EMP_NUM</span>

![bg right:70% w:100%](files/image/CFig06_02.jpg)

# 1NF Step3 - Identify all Dependencies
According to PK (PROJ_NUM, EMP_NUM), we can find a dependency exist (PROJ_NUM, EMP_NUM) → (PROJ_NAME, EMP_NAME, JOB_CLASS, CHG_HOUR, HOURS) and derive it into two partial FD and one transitive FD
- Partial FD: PROJ_NUM → PROJ_NAME (because PROJ_NUM is a part of PK)
- Partial FD: EMP_NUM → EMP_NAME, JOB_CLASS, CHG_HOUR, <span class="brown-text">(not HOURS)</span> (because EMP_NUM is a part of PK)
- Transitive FD: JOB_CLASS → CHG_HOUR (because JOB_CLASS is not part of PK )

# Dependency Diagram
Dependency diagram shows all dependencies found within given table structure
![bg right:70% w:90%](files/image/CFig06_03.jpg)

# After 1NF
- All relational tables satisfy 1NF requirements
  - All key attributes are defined
  - There are no repeating groups in the table
  - All attributes are dependent on the primary key
- Some tables may contain partial and transitive FDs

# Conversion to Second Normal Form (2NF)
A table in the second normal form means
- it is in 1NF
- it does not include partial FD

Conversion to 2NF occurs only when the 1NF has a composite primary key
- If the 1NF has a single-attribute primary key, then the table is automatically in 2NF

Converting to 2NF starts with two steps
1. Make new tables to eliminate partial FD
2. Reassign corresponding dependent attributes

# 2NF Step1 - Make New Tables to Eliminate Partial FD
- Separate composite PK (PROJ_NUM + EMP_NUM) into different PKs
  - PK1: PROJ_NUM
  - PK2: EMP_NUM
  - PK3: PROJ_NUM + EMP_NUM
- Create tables based on new PK
  - Table1: PROJECT, PK is PROJ_NUM
  - Table2: EMPLOYEE, PK is EMP_NUM
  - Table3: ASSIGNMENT, PK is PROJ_NUM + EMP_NUM

# 2NF Step2 - Reassign Corresponding Dependent Attributes
- Table PROJECT(**PROJ_NUM**, PROJ_NAME)
- Table EMPLOYEE(**EMP_NUM**, EMP_NAME, JOB_CLASS, CHG_HOUR)
- Table ASSIGNMENT(**PROJ_NUM**, **EMP_NUM**, <span class="brown-text">ASSIGN_HOUR</span>)
(any attributes that are not dependent in partial FD will remain in the original table)

# Dependency Diagram
![bg right:70% w:90%](files/image/CFig06_04.jpg)

# After 2NF
- All relational tables satisfy 2NF requirements
  - it is in 1NF
  - it does not include partial FD
  - If the 1NF has a single-attribute primary key, then the table is automatically in 2NF
- Some tables may contain transitive FD

# Conversion to Third Normal Form (3NF)
A table in the third normal form means
- it is in 2NF
- it does not include transitive FD

Converting to 3NF starts with two steps
1. Make new tables to eliminate transitive FD 
2. Reassign corresponding dependent attributes

# 3NF Step1 - Make New Tables to Eliminate Transitive FD
A transitive FD: JOB_CLASS → CHG_HOUR 
- Make determinant (JOB_CLASS) as a PK of a new table
- Create tables based on new PK
  - Table JOB(**JOB_CLASS**, CHG_HOUR)

# 3NF Step2 - Reassign Corresponding Dependent Attributes
- Table EMPLOYEE(<u>**EMP_NUM**</u>, EMP_NAME, JOB_CLASS)
- Table JOB(<u>**JOB_CLASS**</u>, CHG_HOUR)
- Table PROJECT(<u>**PROJ_NUM**</u>, PROJ_NAME)
- Table ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**</u>, ASSIGN_HOUR)

# Dependency Diagram
![bg right:70% w:90%](files/image/CFig06_05.jpg)

# After 3NF
- it is in 2NF
- it does not include transitive FD

# Improving the design
- Normalization form only focus on avoiding data redundancy
- Beyond normalization, there are still various issues we need to address
  1. Minimize data entry errors
  2. Evaluate naming conventions
  3. Refine attribute atomicity
  4. Identify new attributes
  5. Identify new relationships
  6. Refine primary keys as required for data granularity
  7. Maintain historical accuracy
  8. Evaluate using derived attributes

# Minimize data entry errors
- When a new database designer on board, we need insert a record in EMPLOYEE table. Thus, we enter data into JOB_CLASS. 
- However, sometime we may enter either Database Designer, DB Designer or database designer. It easily makes data entry errors
- Reduce the data enter errors by adding a <span class="brown-text">surrogate key</span> JOB_CODE <br>   JOB_CODE → JOB_CLASS, CHG_HOUR 
- Table JOB(<u>**JOB_CODE**</u>, JOB_CLASS, CHG_HOUR)
- Surrogate key is an artificial key introduced by DB designer
  - simplify PK design
  - usually numeric
  - often generated automatically by DBMS

# Evaluate Naming Conventions
- CHG_HOUR changed to JOB_CHG_HOUR
- JOB_CLASS changed to JOB_DESCRIPTION
- HOURS changed to ASSIGN_HOURS

# Refine Attribute atomicity
- Atomicity: not being able to be divided into small units
- An atomic attribute is an attribute that cannot be further subdivided
- EMP_NAME divided into EMP_LNAME, EMP_FNAME, EMP_INITIAL

# Identify New attributes
- Consider if any other attributes could be added into table
- Social Security Number, Hire Date,....

# Identify New Relationships
- Add EMP_NUM attribute into PROJECT as a foreign key to keep project manager information

# Refine PKs as Required for Data Granularity (1/3)
- How often an employee reports hours work on a project and at what level of granularity (many times per day, once a day, once a week, at the end of project)
- <span class="brown-text">Granularity</span> refers to the level of detail represented by the values stored in a table’s row


- After 3NF
  ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**</u>, ASSIGN_HOUR)
<style scoped>
table {
  font-size: 25px;
}
</style>
PROJ_NUM|EMP_NUM|ASSIGN_HOUR
--------|-------|-----------
15|103|2.6
18|118|1.4

Report hours at the end of project

# Refine PKs as Required for Data Granularity (2/3)

- Add ASSIGN_DATE attribute
  ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**, **ASSIGN_DATE**</u>, ASSIGN_HOUR)

<style scoped>
table {
  font-size: 25px;
}
</style>
PROJ_NUM|EMP_NUM|ASSIGN_DATE|ASSIGN_HOUR
--------|-------|-----------|-----------
15|103|06-Mar-22|2.6
18|118|06-Mar-22|1.4

Report hours once a day

# Refine PKs as Required for Data Granularity (3/3)
- Add ASSIGN_NUM as a surrogate key
  ASSIGNMENT(<u>**ASSIGN_NUM**</u>, PROJ_NUM, EMP_NUM, ASSIGN_DATE, ASSIGN_HOUR)

<style scoped>
table {
  font-size: 25px;
}
</style>
ASSIGN_NUM|PROJ_NUM|EMP_NUM|ASSIGN_DATE|ASSIGN_HOUR
--------|--------|-------|-----------|-----------
1001|15|103|06-Mar-22|2.6
1002|18|118|06-Mar-22|1.4

- Report hours anytime
- Lower granularity yields greater flexibility

# Maintain historical accuracy
- Add job charge per hour (ASSIGN_CHG_HOUR) into ASSIGNMENT table is important to maintain historical accuracy of the data
- JOB_CHG_HOUR in JOB and ASSIGN_CHG_HOUR in ASSIGNMENT. they may the same in a time period. 
- Due to salary raise, JOB_CHG_HOUR will be changed
- ASSIGN_CHG_HOUR keep historical data and only reflect the charge hour whey employee report hours

# Evaluate Using Derived Attributes
- For simplify coding or improve performance, database designer will introduce derived attributes
- The derived attribute ASSIGN_CHARGE comes from a transitive dependency
- (ASSIGN_HOURS + ASSIGN_CHG_HOUR) → ASSIGN_CHARGE

# The Completed Database After Design Improvement
<div class="grid">
    <img src="files/image/CFig06_06a.jpg" alt="">
    <img src="files/image/CFig06_06b.jpg" alt="">
</div> 

# Surrogate Key Considerations
- Surrogate keys are used by designers when the primary key is considered to be unsuitable
- A surrogate key is a system-defined attribute generally created and managed via the DBMS
- Usually it is a numeric value which is automatically incremented for each new row

# Higher-Level Normal Forms
- Tables in 3NF will perform suitably for business transactional databases
- Higher normal forms are sometimes useful for theoretical interest or statistical research
- Higher-level normal forms: Boyce-Codd normal form (BCNF), 4NF and 5NF

# Normalization and Database Design
- Normalization should be part of the design process
- Proposed entities must meet the required normal form before table structures are created
- Principles and normalization procedures should be written when redesigning and modifying databases
- ERD should be updated through the iterative process

# Denormalization
- Important database design goals include the following:
  - Creation of normalized relations 
  - Considering processing requirements and speed
- A problem with normalization is that joining a larger number of tables takes additional input/output (I/O) operations, thereby reducing system speed
- Defects in unnormalized tables include the following:
  - Data updates are less efficient because tables are larger
  - Lead to data redundancy

# Examples of Denormalization
![bg right:60% w:90%](files/image/CTable06_06.jpg)
- STU_HRS = Credit hours earned
- STU_CLASS = Student classification (fr, so, jr, sr)

# Denormalization - Wide and Narrow Table
<div class="grid">
    <img src="files/image/CFig06_19.jpg" alt="">
    <img src="files/image/CFig06_20.jpg" alt="">
</div>

# Data Modeling Checklist
![bg right:70% w:70%](files/image/CTable06_07.jpg)

# Review Questions
- What is normalization
- When is a table in 1NF
- When is a table in 2NF
- When is a table in 3NF

# Homework #C
1. Read section 6-7 Normalization and Database Design
2. Design database schemas for Contracting Company, including but not limited to
  - Business rules
  - Evolving history of ER diagram in terms of normal forms
  - 1NF, 2NF, 3NF conversion, dependency diagram and reason
  - At least 3 sample records of each table to illustrate PK and FK among tables to demonstrate their relationships.
  - Check your design by Table 6.7 Data Modeling Checklist