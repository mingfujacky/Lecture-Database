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
  .brown-text {
    color: brown;
  }
  .blue-text {
    color: lightskyblue;  
  }

  .small-text {
    font-size: 0.50rem;
  }
---
# Chapter4: Entity Relationship (ER) Modeling
- Data modeling is the first step in database design, as a bridge between real-world objects and the database model implemented in the computer.
- It is important to illustrate data-modeling details graphically through entity relationship diagrams (ERDs) to facilitate communication.
<div class="middle-grid">
    <img src="files/image/CFig02_05.jpg" alt="">
</div>

# Entity Relationship Model
- The entity relationship model (ERM) generate ERD (ER diagram)
- The ERD represents the <span class="blue-text">external model</span> as viewed by end users
- The ERD represents the <span class="blue-text">conceptual model</span> as viewed by database designer
- ERDs describe the database’s main components:
  - Entities
  - Attributes
  - Relationships

# Entity
- An entity is an object of interest to the end user
- An entity in the ERM is a table (relation)
- In Crow’s Foot notation, an entity is represented by a rectangle
  - contains entity name
  - entity name is a noun usually written in all capital letters. It would depend on your naming convention

# Attributes
- **Attributes** are characteristics of entities
- **Required attribute** (not null) and **optional attribute** (allow null)
- Attributes must have a **domain**, the set of possible values for a given attribute
- **Identifier** and **composite identifier** is one or more attributes that uniquely identify each row.
- **Simple attribute** (age, sex) and **composite attribute** (address, phone_number)
- **Single-valued attribute** (emp_id) and **multi-valued attributes** (car_color, emp_habit)
- **Derived attribute** whose value is calculated from other attributes (working_years)

# Identifier and Composite identifier
<div class="grid">
    <img src="files/image/CFig04_02a.jpg" alt="">
</div>

- CLASS_CODE is a identifier
- (CRS_CODE, CLASS_SECTION) is a composite identifier

# Entity's Notation
<div class="grid">
    <img src="files/image/CFig04_01.jpg" alt="">
    <img src="files/image/CFig04_03.jpg" alt="">
</div>

Required attribute: bold font
PK: in a separated cell with bold and underline font

# Implementing Multi-valued Attributes
  - If necessary, replace multi-value attribute by creating several new attributes
  - If necessary, replace multi-value attribute by creating an new entity
<div class="grid">
    <img src="files/image/CFig04_04.jpg" alt="">
    <img src="files/image/CFig04_05.jpg" alt="">
</div>
<br>
<span class="brown-text">Q: What is the pros and cons between the two replacement approaches</span>

# Derived Attributes
<div class="grid">
    <img src="files/image/CFig04_06.jpg" alt="">
</div>
<br>
<span class="brown-text">Q: What attribute is proper to use derived attribute, working_year or total_amount?</span>

# Relationship
- The entities that participate in a relationship are also known as <span class="blue-text">participants</span>
- A relationship is identified by a name that describes the relationship
- The relationship name is an active or passive <span class="blue-text">verb</span>
- <span class="blue-text">Connectivity</span> describes the relationship classification: 1:1, 1:M, and M:N
- <span class="blue-text">Cardinality</span> expresses the minimum and maximum number of entity occurrences associated with one occurrence of the related entity

# Relationship's Notation
<div class="grid">
    <img src="files/image/CFig04_07.jpg" alt="">
    <img src="files/image/CFig04_08.jpg" alt="">
</div>

- (1, 4): one professor teach at least one and no more than four classes
- (1, 1): each class is taught by one and only one professor

# Existence Dependence
- An entity is classified as <span class="blue-text">strong</span> or <span class="blue-text">weak</span> based on its ability to exist independently:
  - A strong entity can exist apart from all of its related entities, it is <span class="blue-text">existence-independent</span>
  - A weak entity is <span class="blue-text">existence-dependent</span> on another related entity occurrence
- Relationship 'EMPLOYEE claims DEPENDENT', the DEPENDENT entity is existence dependent on the EMPLOYEE entity. That is, DEPENDENT has a mandatory (NOT NULL) foreign key, EMP_NUM to link with EMPLOYEE. 

# Weak Entity
- A weak entity is existence-dependent on a strong entity with a strong (identifying) relationship - requires a non-null FK from the related strong entity and form a composite PK.
  - DEPENDENT(<u><b>EMP_NUM, DEP_SID</b></u>, DEP_NAME, DEP_DOB), EMP_NUM is FK,
- A weak entity always has a **mandatory participation** to a strong entity (every row of the weak entity must be associated with one row of a strong entity because of non-null FK).

# Strong Entity
- A strong entity has a PK that uniquely identifies each record without depending on other entity.
- EMPLOYEE(<u><b>EMP_NUM</b></u>, EMP_LNAME, EMP_FNAME, EMP_INITIAL, EMP_DOB, EMP_HIREDATE)

# Example of Strong and Weak Entities
Considering two entities: EMPLOYEE (strong) and DEPENDENT (weak)
- DEPENDENT is weak because it has no sufficient PK by itself at the beginning
  - DEPENDENT(<u><b>DEP_SID</b></u>, DEP_NAME, DEP_DOB, EMP_NUM), EMP_NUM is FK, but when two employee is couple, their children will be duplicated
  - DEP_SID alone cannot uniquely identify a dependent.
- Need expand PK of DEPENDENT by combining EMP_NUM
  - DEPENDENT(<u><b>EMP_NUM, DEP_SID</b></u>, DEP_NAME, DEP_DOB) to build a strong (identifying) relationship with EMPLOYEE to uniquely identify each dependent.
- DEP_NUM is better than DEP_SID in terms of privacy
  - DEPENDENT(<u><b>EMP_NUM, DEP_NUM</b></u>, DEP_NAME, DEP_DOB), EMP_NUM is non-null FK

# Illustrate Relationship Between Weak & Strong Entity
<div class="middle-grid">
    <img src="files/image/CFig04_11.jpg" alt="">
    <img src="files/image/CFig04_12.jpg" alt="">
</div> 

# Relationship Strength
- <u>Relationship strength</u> can be strong or weak based on how to define PK of a related entity. 
- To implement a relationship, the PK of one entity (parent entity, normally on the “one” side of 1:M relationship) appears as a FK in the related entity (child entity, mostly the entity on the “many” side of 1:M relationship) to link two entities. 
  - <span class="blue-text"> Non-identifying(weak) Relationships </span>: if the PK of the "M side" entity does <u>NOT</u> contain a PK of the '1 side' entity
  - <span class="blue-text"> Identifying (strong) Relationships</span>: when the PK of the "M side" entity contains the PK of the "1 side" entity

# Illustration of Relationship Strength

<div class="middle-grid">
    <img src="files/image/CFig04_09.jpg" alt="">
    <img src="files/image/CFig04_10.jpg" alt="">
</div> 

- dotted line shows weak relationships; solid line shows strong relationships

# Implementation Strong / Weak Relationship in DBMS
- Use a strong relationship when:
	•	The M-side entity is conceptually a part of the 1-side.
	•	The M-side object should be destroyed when the 1-side is destroyed (e.g., an employee’s dependant).
- Use a weak relationship when:
	•	The M-site entity can exist independently of the 1-side.
	•	The M-side object should not be deleted if the 1-side is deleted (e.g., an employee and a department).

# The Order to Load Tables Under 1:M Relationship 
- Keep in mind that the order in which the tables are created and loaded is very important.
- In the “COURSE generates CLASS” relationship, the COURSE table must be created before the CLASS table. After all, it would not be acceptable to have the CLASS table’s foreign key refer to a COURSE table that did not yet exist.
- Load the data of the “1” side first in a 1:M relationship to avoid the possibility of referential integrity errors.

# Relationship Participation
- Relationship participation is either <span class="blue-text">optional or mandatory</span>.
- Because of the bidirectional nature of relationships, it is necessary to determine the connectivity as well as max and min cardinalities of the relationship from COURSE to CLASS and from CLASS to COURSE. 
- **Optional participation** means that some rows may not participate into the relationship
- **Mandatory participation** means that each row must participate into the relationship

# Illustration of Relationship Participation

<div class="middle-grid">
    <img src="files/image/CFig04_13.jpg" alt="">
    <img src="files/image/CFig04_14.jpg" alt="">
    <img src="files/image/CFig04_15.jpg" alt="">
</div> 

# Relationship Degree
<div class="middle-grid">
    <img src="files/image/CFig04_16.jpg" alt="">
</div> 

# Recursive Relationship
<div class="middle-grid">
    <img src="files/image/CFig04_19.jpg" alt="">
    <img src="files/image/CFig04_20.jpg" alt="">
</div> 

# Associative (Composite) Entities
- The ER model uses the associative entity to represent an M:N relationship between two or more entities
- It is also called a composite or bridge entity and is a 1:M relationship with the parent entities
- It is composed of the primary key attributes of each parent entity
- The composite entity may also contain additional attributes that play no role in connective process

# Illustration of Associative Entities
STUDENT has CLASS is a M:N relationship
<div class="grid">
    <img src="files/image/CFig03_23.jpg" alt="">
    <img src="files/image/CFig04_26.jpg" alt="">
</div> 

# Developing an ER Diagram
Building an ERD usually involves the following activities as a <span class="blue-text">iterative process</span>:
- Create a detailed description of the organization’s operations
  - Interview users
  - Investigate SOPs, Forms, Reports 
- Identify business rules based on the description of operations
- Identify main entities and relationships from the business rules
- Develop the initial ERD
- Identify the attributes and primary keys that adequately describe entities
- Revise and review the ERD

# Tiny College (TC) (1,2/10)
- Tiny College is divided into several schools.
  - A school is managed by a professor. 
  - Each professor can be the dean of only one school, or none of any school. 
- Each school has several departments.
  - The number of departments operated by a school is at least one to many
  - Each department belongs to only a single school
![bg right:40% w:100% CFig04_27](files/image/CFig04_27.jpg)

# Tiny College (TC) (3/10)
- Each department may offer courses.
  - Some departments that were classified as "research only," they would not offer courses; therefore, the COURSE entity would be optional to the DEPARTMENT entity.
![bg right:40% w:100% CFig04_28](files/image/CFig04_28.jpg)

# Tiny College (TC) (4/10)
- A course can be taught in several classes.
- A course may not be taught in some semester 
- A class is offered during a given semester. SEMESTER defines the year and the term that the class will be offered. 
- CLASS is optional to SEMESTER.
- CLASS is optional to COURSE.
![bg right:40% w:100% CFig04_29](files/image/CFig04_29.jpg)

# Tiny College (TC) (5/10)
- Each department should have one or more professors assigned to it. 
- One and only one of those professors chairs the department
- Not all professors are required to chair a department. 
- DEPARTMENT is optional to PROFESSOR in the "chairs" relationship.
![bg right:40% w:100% CFig04_30](files/image/CFig04_30.jpg)

# Tiny College (TC) (6/10)
- Each professor may teach up to four classes; each class is belong to a course.
- A professor may also be on a research contract and teach no classes at all.
![bg right:40% w:100% CFig04_31](files/image/CFig04_31.jpg)

# Tiny College (TC) (7/10)
- A student may enroll in several classes but take each class only once.
- Each student may enroll in up to six classes, and each class may have up to 35 students, (STUDENT and CLASS is M:N relationship ). 
- This M:N relationship must be divided into two 1:M relationships by ENROLL entity 
![bg right:40% w:100% CFig04_32](files/image/CFig04_32.jpg)

# Tiny College (TC) (8/10)
- Each department has several students whose major is offered by that department. <span class="red-text">(VAGUE!!)</span>
- Each student has only a single major associated with a single department.
- It is possible for a student not to declare a major field of study.
![bg right:40% w:100% CFig04_33](files/image/CFig04_33.jpg)

# Tiny College (TC) (9/10)
- Each student has an advisor in his or her department
- Each advisor counsels several students.
- An advisor is also a professor, but not all professors advise students.
![bg right:40% w:100% CFig04_34](files/image/CFig04_34.jpg)

# Tiny College (TC) (10/10)
- A class is taught in a room.
- Each room is located in a building.
- A building can contain many rooms. 
- Some buildings do not contain (class) rooms.
![bg right:40% w:100% CFig04_35](files/image/CFig04_35.jpg)

# Tiny College (TC) (Summary: Entities)
PROFESSOR
COURSE
STUDENT
SCHOOL
CLASS
BUILDING
DEPARTMENT
SEMESTER
ROOM
ENROLL (the associative entity between STUDENT and CLASS)

# Summary: Components of ERM
![bg right:70% w:100% CTable04_04](files/image/CTable04_04.jpg)

# Summary: Completed ERD
![bg right:70% w:60% CFig04_36](files/image/CFig04_36.jpg)

# Database Design Challenges: Conflicting Goals
- Database designers must often make design compromises that are triggered by conflicting <span class='blue-text'>GOALS</span>
  - Database design must conform to design standards
  - High processing speed may limit the number and complexity of logically desirable relationships
- However, a design that meets all requirements and design conventions are the most important goals

# Review Questions
- What is the difference between weak entity and strong entity?
- What is the difference between weak (non-identifying) and identifying (strong) relationship?
- How to translate M:N relationship in ERM?

# Homework #B
資料庫課程作業(B)