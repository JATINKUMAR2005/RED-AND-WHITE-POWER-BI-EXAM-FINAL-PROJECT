# 🎓 Student Performance Analytics Dashboard (Power BI)

A complete Power BI project designed to analyze student performance using multiple datasets such as Scores, Attendance, Behavior, and Student demographics. This dashboard provides insights into academic performance, attendance trends, behavioral patterns, and identifies top-performing and at-risk students.

---

## 📂 Project Overview

This project integrates four different datasets into a unified, interactive Power BI dashboard:

- **Students**
- **Scores**
- **Attendance**
- **Behavior**

Using data modeling, DAX measures, visual analytics, drillthroughs, and tooltips, we create a complete insight system for school performance monitoring.

---

## 📁 Datasets Used

### **1. Students.csv**
Contains student demographic information.
| Column | Description |
|--------|-------------|
| StudentID | Unique ID for each student |
| Name | Student Name |
| Gender | Male/Female |
| Class | Grade level |
| Section | Section identifier |

---

### **2. Scores.csv**
Contains academic performance records.
| Column | Description |
|--------|-------------|
| StudentID | Linked to Students table |
| Subject | Subject name |
| ExamType | Exam/Test category |
| Score | Marks obtained |
| MaxScore | Maximum marks |
| Term | Term/semester |

---

### **3. Attendance.csv**
Tracks student daily attendance.
| Column | Description |
|--------|-------------|
| StudentID | Linked to Students table |
| Date | Attendance date |
| Status | Present/Absent |
| Reason | Optional reason |

---

### **4. Behavior.csv**
Logs student behavior records.
| Column | Description |
|--------|-------------|
| StudentID | Linked to Students table |
| Date | Behavior date |
| BehaviorType | Positive/Negative/Incident |
| Notes | Additional comments |

---

## 🔗 Data Model (Star Schema)

The dashboard uses a **Star Schema** for optimal performance:

markdown
Copy code
       STUDENTS (Dimension)
             │
 ┌───────────┼────────────┐
 │           │            │
SCORES ATTENDANCE BEHAVIOR
(Fact) (Fact) (Fact)

yaml
Copy code

All fact tables are connected to **Students[StudentID]** using **1-to-Many** relationships.

---

## 🧠 Key DAX Measures

### **Total Students**
```DAX
Total Students = DISTINCTCOUNT(Students[StudentID])
Total Score
DAX
Copy code
Total Score = SUM(Scores[Score])
Total Max Score
DAX
Copy code
Total Max Score = SUM(Scores[MaxScore])
Percentage Score
DAX
Copy code
Percentage Score = DIVIDE([Total Score], [Total Max Score], 0)
Attendance Percentage
DAX
Copy code
Attendance % =
VAR TotalDays = COUNTROWS(Attendance)
VAR PresentDays =
    CALCULATE(COUNTROWS(Attendance), Attendance[Status] = "Present")
RETURN
DIVIDE(PresentDays, TotalDays)
Behavior Count per Type
DAX
Copy code
Behavior Count =
COUNTROWS(Behavior)
Performance Category
DAX
Copy code
Performance Category =
SWITCH(
    TRUE(),
    [Percentage Score] >= 0.80, "High",
    [Percentage Score] >= 0.50, "Medium",
    "Low"
)
Top Student Name
DAX
Copy code
Top Student Name =
VAR TopStudent =
    TOPN(
        1,
        ADDCOLUMNS(Students, "PerfScore", [Percentage Score]),
        [Percentage Score], DESC
    )
RETURN
MAXX(TopStudent, Students[Name])
📊 Visuals Included
Dashboard Pages
Overview Dashboard

KPIs: Total Students, Avg Attendance, Avg Score

Bar chart: Avg Score by Subject

Donut: Behavior Type Distribution

Table: Student Performance with Conditional Formatting

Performance Analysis

Line chart: Score trends by Term

Bar chart: Class-wise performance

Top N Student Ranking

Attendance Insights

Monthly attendance trend

Attendance percentage by class

High/low attendance indicators

Behavior Analysis

Behavior incidents distribution

Top students with most behavior occurrences

Student Drillthrough Page

Student profile

Score trend line

Attendance trend

Behavior history

🎯 Tooltip Enhancements
A custom tooltip page includes:

Mini Score Trend (Line chart)

Mini Attendance trend (Bar chart)

Student name & key metrics

This improves user interaction and provides quick insights on hover.

🧭 Interactivity Features
Drillthrough

Tooltips

Slicers (Class, Section, Subject, Term)

Top N slider

Dynamic ranking

📐 Design Principles Used
Clean and consistent layout

Color-coded performance categories

Minimal visual clutter

High usability with navigation buttons

Optimized for storytelling

📌 Insights Summary
Identifies high, medium, low performers

Shows top subjects and weak subjects

Highlights students with low attendance

Tracks behavior trends and incident frequency

Displays top-performing student with total score

Helps teachers target students who need support

🚀 How to Use
Import the datasets into Power BI

Build the relationships in Model View

Create DAX measures listed above

Add visuals and apply formatting

Set up tooltip pages and drillthrough

Publish to Power BI Service (optional)

🏁 Conclusion
This Power BI project provides a complete 360° analysis of student performance by integrating academic scores, attendance, and behavior. It helps educators and administrators make data-driven decisions to support student success.

🧑‍💻 Author
Jaden
Power BI Analyst | Data Visualization Learner

yaml
Copy code

---

If you want, I can also create:

✔ A **project explanation PPT**  
✔ A **video script for presentation**  
✔ A **professional summary for your resume**  

Just tell me!
