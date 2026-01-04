# ECON485 Project 3 — Tourism Revenue & Visitor Trends
**Team 3 - Tourism Analytics Database**

## Project Overview
This project builds a tourism analytics database to track visitors, stays, and spending across regions. It supports policy, hotel management, and economic analysis with SQL-based reporting.

## Team Members
- **Project Lead:** Mert Akin — Schema design & database architecture  
- **Data Analyst:** Kaan Erdemir — Query development & performance optimization  
- **Economic Analyst:** Yaren Yamak — Business logic & economic interpretation  
- **Documentation Lead:** Oraz — AI logs, meeting notes, and presentations  

## Timeline (condensed)
| Week | Phase | Milestone | Status |
|------|-------|-----------|--------|
| 3 | Initial Planning | Team formation & GitHub setup | Complete |
| 4 | Initial Planning | Project definition & ER model | Complete |
| 5 | Design & Prototype | Normalized schema (3NF) | Complete |
| 6-7 | Design & Prototype | CRUD + initial business queries | Complete |
| 8 | Exam Week | — | N/A |
| 9 | Design & Prototype | Team presentation #2 | Complete |
| 10-11 | Final Presentation | Advanced queries, views, indexes | Complete |
| 12-14 | Final Presentation | Integration, final demo & delivery | Complete |

## Repository Structure
```
.
├─ design/
│  ├─ schema.sql
│  ├─ data_dictionary.md
│  ├─ normalization_analysis.md
│  ├─ er_diagram.sql
│  └─ er_diagram_final.png.png
├─ data/
│  ├─ csv_income_and_expenses_data.csv
│  ├─ csv_Number_of_trips_and_nights_by_age_group_of_travelers_data.csv
│  ├─ csv_2022_data.csv
│  └─ data_description.md
├─ queries/
│  ├─ 01_crud_operations.sql
│  ├─ 02_business_queries.sql
│  └─ 03_advanced_queries_views.sql
└─ docs/
   ├─ ai_logs.md
   ├─ project_definition.md
   └─ meeting_notes/
      ├─ week3_meeting.md
      ├─ week4_meeting.md
      ├─ week5_meeting.md
      ├─ week7_meeting.md
      ├─ week9_meeting.md
      ├─ week9_presentation.md
      └─ week14_meeting.md
```

## Data Overview
- All CSVs are UTF-8 with comma delimiters and preserved header/comment rows.
- See `data/data_description.md` for field-level notes and loading guidance.

## Quick Start
```bash
# Clone repository
git clone https://github.com/akinmertc/ECON-485-Project-Test.git
cd ECON-485-Project-Test

# (Optional) set up database
mysql -u root -p < design/schema.sql

# Run sample queries
mysql -u root -p tourism_db < queries/01_crud_operations.sql
```

## Current Status
- Schema, queries, and documentation are finalized.
- Data exports reflect the latest `_data` CSVs in `/data`.
- Meeting notes and AI logs are up to date with team assignments.
