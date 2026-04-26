 1. Project Overview

This Power BI dashboard was built as part of the Practical Exam on Power BI The dashboard provides a comprehensive, interactive view of student academic performance, attendance patterns, and behavioral trends across multiple grades, subjects, and academic terms.
The project demonstrates proficiency in all five key areas evaluated in the exam: Data Modeling & Cleaning, DAX Calculations, Visualizations & Storytelling, Slicers & Interactivity, and Optional Features (Mobile Layout).

2. Dataset Information
Four datasets were used in this project, all provided by Red & White Skill Education:
| Table | Rows | Columns | Key Fields |
|---|---|---|---|
| Students | 1,000 | 5 | StudentID, Class, Section |
| Scores | 30,000 | 6 | Subject, ExamType, Term |
| Attendance | 100,000 | 4 | Date, Status, Reason |
| Behavior | 6,500 | 4 | BehaviorType, Notes |

Key dataset facts: 1,000 unique students across 12 classes (Grades 1–12) and 3 sections (A, B, C). Students have scores across 5 subjects (Math, Science, English, History, Geography), 3 exam types (Unit Test, Mid Term, Final Exam), and 3 academic terms. Attendance spans 100,000 records with approximately 90% average attendance rate. Behavior data covers 5 behavior types including both positive (Participative, Helpful) and negative (Disruptive, Late, Absent without notice) categories.

 3. Data Model & Relationships

The data model follows a Star Schema with Students as the central (fact) table and the three transaction tables (Scores, Attendance, Behavior) as dimension/fact tables connected via StudentID.
**Relationship Structure:**
- Students → Scores (1:Many)
- Students → Attendance (1:Many)
- Students → Behavior (1:Many)
- All relationships on StudentID field

**Data Cleaning Applied:**
- Correct data types on all columns
- Date columns parsed as Date type
- Null Reason values replaced with 'No Reason'
- Null Notes values replaced with 'No Notes'
- Added IsPresent custom column (1 for Present, 0 for Absent)


 4. DAX Measures

The following DAX measures were created in a dedicated 'Measures' table to keep the model organized:

| Measure Name | DAX Formula | Purpose |
|---|---|---|
| % Score | DIVIDE(SUM(Score), SUM(MaxScore), 0) | Percentage score per student/subject |
| Avg Score | AVERAGE(Scores[Score]) | Overall average score KPI |
| Attendance % | COUNTROWS(FILTER(...))/COUNTROWS(...)*100 | Percentage of days attended |
| Behavior Count | COUNTROWS(Behavior) | Total behavior incidents |
| Performance Category | SWITCH(TRUE(), pct>=0.8, "High"...) | High / Medium / Low classification |
| Total Students | DISTINCTCOUNT(Students[StudentID]) | Unique student count KPI |
| Pass Rate % | Students with score >= 40% | Percentage passing threshold |



 5. Dashboard Pages & Visualizations

The dashboard is structured across 3 main pages plus 2 supporting pages (Drillthrough & Tooltip).

Page 1 — Overview Dashboard
- 4 KPI Cards: Total Students (1,000), Average Score, Average Attendance %, Pass Rate %
- Clustered Bar Chart: Average Score by Subject, grouped by Class — shows which subjects perform best per grade
- Line Chart: Score trend across Term 1, Term 2, Term 3 — reveals improvement or decline over the year
- Data Table: Student-level scores with conditional formatting (Green ≥80%, Orange 40–79%, Red <40%)

Page 2 — Academic Analysis
- Stacked Column Chart: Scores by ExamType across Terms
- Matrix Visual: Student rows × Subject columns with average score — heatmap style performance grid
- Pie Chart: Distribution of Performance Categories (High/Medium/Low) across all students

Page 3 — Behavioral Analysis
- Donut Chart: Behavior types distribution (Disruptive vs Participative vs Helpful vs Late vs Absent without notice)
- Stacked Bar Chart: Behavior counts by BehaviorType, grouped by Class
- Line Chart: Behavior incidents over time — shows behavioral trends across the academic year
- Table: Student-wise behavior summary

Page 4 — Student Profile (Drillthrough)
- Activated via right-click → Drill through on any student name in the main dashboard
- Shows individual student: name, class, section, gender, score trend, behavior summary, attendance %

Page 5 — Tooltip Page
- Mini dashboard displayed on hover over bar chart data points
- Shows: Avg Score, Attendance %, Behavior Count for the hovered group



6. Complete Visualization Summary

| Visual Type | Page | Fields Used | Marks |
|---|---|---|---|
| KPI Cards (4) | Overview | Total Students, Avg Score, Attendance %, Pass Rate | 15 |
| Bar Chart | Overview | Subject (Y), Avg Score (X), Class (Legend) | 15 |
| Line Chart | Academic | Term (X), % Score (Y), Subject (Legend) | 15 |
| Donut Chart | Behavioral | BehaviorType (Legend), Behavior Count (Values) | 15 |
| Table + Conditional Formatting | Overview | Student Name, Score, % Score with conditional colors | 15 |
| Matrix | Academic | Student (rows), Subject (cols), Avg Score (values) | 15 |
| Stacked Bar | Behavioral | BehaviorType, Class grouping | 15 |


7. Interactivity Features

Slicers (4 filters):
- Class Slicer (Dropdown) — Grades 1–12
- Section Slicer (Tile) — A, B, C
- Subject Slicer (Dropdown) — 5 subjects
- Term Slicer (Tile) — Term 1, Term 2, Term 3
- All slicers sync across pages

Advanced Interactivity:
- Drillthrough: Student Profile Page — right-click any student name to drill into their individual profile
- Bookmarks: Academic View / Behavioral View toggle buttons for quick navigation
- Tooltips: Mini dashboard appears on chart hover showing Avg Score, Attendance %, Behavior Count
- Cross-highlighting between visuals when clicking on a chart element
- Mobile Layout: Optimized for Power BI mobile app

 8. Key Insights Derived

- **Student Performance:** Average score across all subjects and terms is approximately 49.87%, indicating a roughly even split between passing and below-average students.
- **Attendance Patterns:** Overall attendance rate is approximately 90%, which is healthy, though individual student analysis via drillthrough reveals outliers with significantly lower attendance that correlates with lower scores.
- **Subject Performance:** Bar chart analysis reveals performance variation across Math, Science, English, History, and Geography, allowing teachers to identify which subjects need additional focus per grade.
- **Behavioral Trends:** The behavioral analysis page shows the distribution between positive (Participative, Helpful) and concerning (Disruptive, Late, Absent without notice) behaviors, enabling targeted student support.
- **Term Progression:** Line chart trend analysis shows whether students improve, decline, or remain consistent across Term 1, Term 2, and Term 3.
- **Performance Categories:** SWITCH-based DAX classifies students into High (≥80%), Medium (40–79%), and Low (<40%), enabling quick identification of at-risk students.

9. Marks Breakdown & Strategy

| Component | Marks | Key Elements to Include |
|---|---|---|
| Data Modeling & Cleaning | 10 | 4 tables loaded, correct data types, relationships, null handling |
| DAX Calculations | 10 | All 5 required measures + additional KPI measures |
| Visualizations & Storytelling | 15 | All 5 chart types present + consistent theme + titles |
| Slicers, Filters & Drillthrough | 10 | 4 slicers, drillthrough page, bookmarks, tooltips |
| Optional Features | 5 | Mobile layout created and organized |
| **TOTAL** | **50** | Full marks possible with all steps completed! |


10. Submission Contents

- StudentPerformanceDashboard.pbix — Main Power BI file with all pages, measures, and visuals
- Students.xlsx — Source data: 1,000 student records
- Scores.xlsx — Source data: 30,000 exam score records
- Attendance.xlsx — Source data: 100,000 attendance records
- Behavior.xlsx — Source data: 6,500 behavior records



