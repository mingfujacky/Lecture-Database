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
# Chapter 1: Database Systems
- Organizations use data to keep track of their day-to-day operations. Such data is used to generate information, which in turn is the basis for good decisions. 
- Data is likely to be managed most efficiently when it is stored in a database.

# Why Database
- Databases evolved from the need to manage **large amounts** of data in an **organized and efficient** manner
- Databases is everywhere
![bg right:60% w:600 Database is everywhere](files/image/CFig01_01.jpg)


# Data versus Information
- Information is the result of processing raw data to reveal the meaning of data
- **Data management** is a discipline that focuses on the proper generation, storage, and retrieval of data
![bg right:60% w:750 Data vs Information](files/image/CFig01_02.jpg)

# Introducing the Database
- A **database** is a collection of related data.
  - represent a **mini-world** to reflect some aspect of the real world
  - **logically coherent** collection of data with some inherent meaning
  - is designed, built, and populated with data for **a specific purpose**
- A **database management system (DBMS)** is a collection of programs that manages the database **structure** and **controls access** to the data stored in the database. Here, the database refers to a **shared, integrated** computer structure.
- Examples of DBMS: MySQL, Microsoft SQL Server, Oracle Database, MongoDB, Cassandra, Neo4j, ...

# Role and Advantages of DBMS
- DBMS presents the end user with a single, integrated view of the data in the database
- DBMS advantages:
  - Improved data sharing
  - Improved data security
  - Better data integration
  - Minimized data inconsistency
  - Improved data access
![bg right:40% w:500 DBMS role](files/image/CFig01_04.jpg)

# Types of DBMS
- by # of users: single-user, multiple-user 
- by location: centralized, distributed, cloud
- by time sensitive: online transaction processing (OLTP), online analytical processing (OLAP)
- by data characteristics: SQL store structured data, NoSQL store unstructured and semi-structured data

# Why Should We Learn Database Design
- **Database design** refers to the activities that focus on the design of the database structure that will be used to store and manage end-user data
- Poorly designed databases can lead to slow performance, data integrity issues, security vulnerabilities, and challenges in scaling applications.

![w:800 poor database design](files/image/CFig01_05.jpg)

# Application Design Process
- <span class="brown-text">Requirements & Analysis</span>
 <span class="small-text">Discover users requirements, analyze what data should be maintained</span>
- <span class="brown-text">Data / Database design</span>
  - <span class="small-text">Conceptual model</span>
  - <span class="small-text">Choice of a DBMS</span>
  - <span class="small-text">Logical model</span>
  - <span class="small-text">Physical model</span>
- <span class="brown-text">System design</span>: <span class="small-text">design system functionality and user interface</span>
- <span class="brown-text">Implementation</span>: <span class="small-text">realize algorithms and physical data model on running environment and optimize performance</span>

![bg right:30% w:400](https://techforumugm.files.wordpress.com/2020/03/dd01.png?w=816&h=352&crop=1)

# Database Design Process
![bg right:60% w:90%](files/image/database_design_process.jpg)

# A Good Database Design Following Database Design Process
![bg right:50% w:600 poor database design](files/image/CFig01_06.jpg)

# Database System Environment
Collect, store, manage, and use of data within a database environment, including:
- <span class='small-text'>Hardware</span>
- <span class='small-text'>Software</span>
- <span class='small-text'>People</span>
- <span class='small-text'>Procedures</span>
- <span class='small-text'>Data</span>

![bg right:55% w:100% database system environment](files/image/CFig01_10.jpg)

# DBMS Functions
- Data dictionary management to store definitions of data elements and their relationships
- Data storage management
- Security management
- Transaction management and concurrent control
- Backup and recovery management
- Data integrity management
- SQL languages (structured query language)
- Database communication API (application programming interfaces)
![bg right:30% w 80% data dictionary](files/image/fig_data_dictionary.png)

# Disadvantages of DBMS
- Increased costs
- Management complexity
- Maintaining expenditure (operation expertise and man power)
- Vendor dependency (vendor lock-in)
- Frequent upgrade/replacement cycles

# Database Professional Career
<style scoped>
table {
  font-size: 25px;
}
</style>
Job Title|Description|Sample Skills Required
---------|-----------|----------------------
Developer | Develop application | Programming, SQL
DBA| Design, manage DBMS | DBMS fundamentals, SQL
Database Designer | Design data models | Domain knowledge, data modeling, DBMS fundamentals, SQL
Data Security Officer | Enforce data security rules| DBMS fundamentals, data security
Data Analyst / Data Scientist| Analyze varied data to generate insights and prediction| Data analysis, statistics, SQL / programming, ML / AI, data visualization

# When Not to Use a DBMS
- When costs can not be justified: H/W, S/W, operations  
- When a DBMS may be unnecessary: simple applications, limited users
- When a DBMS may be infeasible: embedded systems
- When no DBMS may suffice: real-time requests, complexity of data, special operation

# Review Questions
- What is a database?
- What is a DBMS?
-	Which is NOT the advantage of using a DBMS?
(A) Improve data sharing (B) Reduce hardware cost (C) Enhanced data security
(D) Minimize data inconsistency
- What is NOT the main components of a database system environment?
(A) Hardware (B) Internet connection (C) Data (D) Procedures


