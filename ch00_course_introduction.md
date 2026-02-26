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

  .small-text {
    font-size: 0.50rem;
  }
---
# 資料庫管理
- 講師：林志偉
- 教材：https://github.com/mingfujacky/Lecture-Database.git
![bg right:20% w:200 Data Structure Material in Git](files/image/qrcode_lecture_database.png)

# Textbook
![bg right:60% w:50% textbook](files/image/cover_of_database_systems_14e.jpg)
- Database Systems Design, Implementation, and Management 14/E
- Coronel & Morris
- Cengage, 2023

# 課程講師 - 林志偉 (Jacky Lin)
![bg right:30% w:300](files/image/jacky_last_day_in_tsmc.jpg)

- #### 現職: 陽明交通大學 / 學士後電子與光子學士學位學程 助理教授
- #### 學歷: 交大資訊管理博士
- #### 經歷: 台積電資訊科技(IT)
- #### 專長: 資料工程、程式設計、巨量資料分析
- #### Email: jacky.jw.lin@nycu.edu.tw

# 課程助教
- 陳宗佑 joey76171.sc13@nycu.edu.tw
- 蔡孟哲 aayy0917.sc13@nycu.edu.tw

# 生活中怎麼表達資料庫概念
[Excel Files vs Database](https://youtu.be/7yYbbKyyHvw?si=Y3vrhXjLHS4FGtkN)

# Database Position in 3 Tiers Architecture
![bg right 50% w 100%](files/image/3_tier_architecture.png)

# DBMS and Its Products
- DBMS: Database Management System
- SQL: Structured Query Language
![bg right 50% w 100%](files/image/DBMS_SQL.jpg)



# 課程規劃
- #### 課程目標
  *-* Introduce database design process and SQL programming.
  *-* Use Python and MySQL to practice data manipulation and sharpen SQL skill.
- #### 授課方式
  *-* 教材講解
  *-* 課堂 Lab 實作 (week 9, 10, 11 上課請攜帶電腦)

# 評分方式
- Attendance(10%): roll call and QA 
- Homework (20%): 4 times
- Mid-term exam (20%): closed-book exam
- Final-term exam (20%): closed-book exam
- Project (30%): 
  - 電子與光子學程: group by 3 ~ 6 members, 資財系: group by 5 ~ 6 members
  - form team by week 3
  - hand-in progress report by week 9
  - hand-in final report by week 17

# Recommended TOC of Final Report
- **Requirements** we plan to fulfill and/or **problems** we plan to solve
- Teaming (roles and peer evaluation (1~10 points))
- User requirements and business rules
- Database design (ERD, normalization, data dictionary)
- Database implementation (SQL script)
- Application briefings (systems architecture, main function screen shot) 
- Lesson learned
- Present date (專班: 05/27,  6組, 每組10分鐘, 資財: 05/28, 12組, 每組10分鐘)
- Report submission deadline: 06/15 (Sunday) 23:59 


# Members in Project
- **End user**: define business rule and function requirements 
- **Database designer**: translate user requirements into database design
- **Database administrator**: realize database design in DBMS
- Data analyst: reporting and investigation
- Developer: develop user interface
- Project manager: team organization, schedule control and communication

# 時時實際操作
<br>
"我鼓勵你使用鍵盤手動複製這些程式，而不是直接將其原始程式碼複製貼上到新檔案中；這有助於你對程式產生「肌肉記憶」，並迫使你在鍵入時考慮每一行。"

![bg right:30% w:300 遞迴演算法大師親授面試心法](https://i3.momoshop.com.tw/1721136961/goodsimg/0013/030/254/13030254_R.jpg)

# 授課大綱
[113下學期](https://timetable.nycu.edu.tw/?r=main/crsoutline&Acy=113&Sem=2&CrsNo=520015&lang=zh-tw)

# Database Design Process
![bg right 70% w 100%](files/image/database_design_process.jpg)

# Software We Use in Class
![bg right 70% w 100%](files/image/workbench.jpg)

# 加簽順序
- 資財系 > 雙主修輔系資財系 > 管科系、運管系 > 跨域(財金跨域) > 一般
- 五年級 > 四年級 > 三年級 > 二年級 