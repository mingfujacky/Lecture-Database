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
# 資料庫管理(520007)
- 講師：林志偉
- 教材：https://github.com/mingfujacky/Lecture-Database.git
![bg right:20% w:200 Data Structure Material in Git](files/image/qrcode_lecture_database.png)

# Textbook
![bg right:50% w:50% textbook](files/image/cover_of_database_systems_14e.jpg)
- Database Systems Design, Implementation, and Management 14/E
- Coronel & Morris
- Cengage, 2023

# 課程講師 - 林志偉 (Jacky Lin)
- #### 現職: 陽明交通大學 / 學士後電子與光子學士學位學程 助理教授
- #### 學歷: 交大資訊管理博士
- #### 經歷: 台積電資訊科技(IT)
- #### 專長: 資料工程、程式設計、巨量資料分析
- #### Email: jacky.jw.lin@nycu.edu.tw

# 課程助教
- 陳宗佑 joey76171.sc13@nycu.edu.tw
- 蔡孟哲 aayy0917.sc13@nycu.edu.tw

# 生活中怎麼表達資料庫概念
[![Excel Files vs Database](https://i.ytimg.com/vi/7yYbbKyyHvw/mqdefault.jpg)](https://youtu.be/7yYbbKyyHvw?si=Y3vrhXjLHS4FGtkN)

# Database Position in 3 Tiers Architecture
![bg right 50% w 100%](files/image/3_tier_architecture.png)

[![Three tier architecture](https://i.ytimg.com/vi/G-Ks1XYGyaY/mqdefault.jpg)](https://youtu.be/G-Ks1XYGyaY?si=eM7f-0Bwsa9DYCGo)


# DBMS and Its Products
- DBMS: Database Management System
- SQL: Structured Query Language

![w:800 DBMS AND SQL](files/image/DBMS_SQL.jpg)

# 課程目標
> Introduce database design process and SQL programming.
> Use Python and MySQL to practice data manipulation and sharpen SQL skill.

# 授課方式
> 1. 課堂講解
> 2. 課間實作 (SQL相關課程時，請攜帶電腦)
> 3. 課後作業
> 4. 期中考試
> 5. 期末考試
> 6. 期末專題

# 評分方式
- (10%) 課堂參與
  > 5次點名 
  > 正常出席得 2分, 有請假單得 1分, 無故缺席得 0分
- (20%) 課後作業: 4次作業 (不受理遲交)
- (20%) 期中考試
- (20%) 期末考試
- (30%) 期末專題: 採分組進行，每5~7人一組，題目自訂
  - 期中考後一週完成分組並決定專題題目
  - 期末考前一週進行口頭報告並於期限內上傳期末專題書面報告 (不受理遲交)
> 除「成績計算」或「登錄」有誤外，請同學勿以個人理由請求調整成績

# 期中期末考試試場規定
> 1. 按照助教安排進入考場入座，不得攜帶書本及參考資料
> 2. 不得使用手機，請將手機放置在監考人員的可視範圍內，如桌上或教室前面
> 3. 攜帶學生證或其他可以確認身份的證件
> 4. 考試時間為六十分鐘

# 期末專題報告至少需包含以下內容
- **Requirements** we plan to fulfill and/or **problems** we plan to solve
- Teaming (roles)
- User requirements and business rules
- Database design (ERD, normalization, data dictionary)
- Database implementation (SQL script)
- Application briefings (systems architecture, main function screen shot) 
- Lesson learned
- Present date (06/05, 預計16組, 每組10分鐘)
- Report submission deadline: 06/19 23:59 


# Members in Project
- **End user**: define business rule and function requirements 
- **Database designer**: translate user requirements into database design
- **Database administrator**: realize database design in DBMS
- Data analyst: reporting and investigation
- Developer: develop user interface
- Project manager: team organization, schedule control and communication

# 授課大綱
[114下學期](https://timetable.nycu.edu.tw/?r=main/crsoutline&Acy=114&Sem=2&CrsNo=520007&lang=zh-tw)

# Software We Use in Class
![bg right 70% w 100%](files/image/workbench.jpg)