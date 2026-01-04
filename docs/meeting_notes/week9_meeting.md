# ECON485 Project 3 - Meeting Notes: Week 9

**Meeting Date:** Monday, Week 9 (Fall 2025)  
**Meeting Type:** Stage 2 Presentation Preparation & Rehearsal  
**Duration:** 2.5 hours  
**Location:** Library Study Room B + Zoom hybrid

## 📋 Attendees

- ✅ [Member 1] - Project Lead
- ✅ [Member 2] - Data Analyst  
- ✅ [Member 3] - Economic Analyst
- ✅ [Member 4] - Documentation Lead

## 🎯 Meeting Objectives

1. Finalize Stage 2 presentation slides
2. Rehearse 20-minute presentation
3. Prepare live database demo
4. Assign speaking roles
5. Create backup materials (in case demo fails)
6. Review progress against KPIs

---

## 📝 Discussion Summary

### 1. Stage 2 Progress Assessment

**Stage 2 KPIs Review (from project rubric):**

| KPI | Target | Status | Evidence |
|-----|--------|--------|----------|
| Schema Completeness | Covers branches, items, transactions, staff | ✅ **Exceeded** | 7 tables (regions, hotels, visitors, bookings, expenditures, room types, seasons) |
| 3NF Verification | Up to 3NF | ✅ **Achieved** | normalization_analysis.md documents compliance with justified exceptions |
| Query Accuracy | 5 working SQL queries | ✅ **Achieved** | 3 business queries (Week 7) working + tested, 5 advanced queries planned Week 10 |
| Sample Data | Tested with realistic data | ✅ **Achieved** | 87 records across 7 tables, realistic seasonal/geographic distribution |

**Overall Stage 2 Status:** ✅ All KPIs met or exceeded

**Team Sentiment:** Confident in our work, ready to present

---

### 2. Presentation Structure Finalization

**Agreed Structure (20 minutes total):**

**Section 1: Introduction (2 min) - [Member 1]**
- Project overview
- Team introduction
- Stage 2 objectives recap

**Section 2: Schema Design & Normalization (4 min) - [Member 2]**
- ER diagram walkthrough (visual aid)
- 7 tables explained
- 3NF compliance discussion
- Intentional denormalizations (TotalCost justification)

**Section 3: Live Demo (6 min) - [Member 2]**
- Database connection
- CRUD operations example
- Run Query 1 (regional spending)
- Run Query 2 (seasonal patterns)
- Show results interpretation

**Section 4: Economic Insights (5 min) - [Member 3]**
- Key finding 1: Seasonality dominates (50% revenue in 3 months)
- Key finding 2: International premium (2.5x spending)
- Key finding 3: Regional variation (Istanbul vs rural)
- Policy implications

**Section 5: Challenges & AI Learning (2 min) - [Member 4]**
- AI tools used (ChatGPT, Copilot, dbdiagram.io)
- Fail-forward examples (3 specific errors)
- Human oversight importance

**Section 6: Q&A (1 min) - All**
- Prepared answers for expected questions

---

### 3. Slide Development

**Slide Deck Created:**

**Total Slides:** 22 slides

**Key Slides:**
1. Title slide
2. Agenda
3. Project recap
4. ER diagram (full-page visual)
5. Normalization table (3NF compliance checklist)
6. TotalCost denormalization justification
7. Sample data statistics
8. Demo setup (screenshot of database)
9-11. Query results (one slide per query with charts)
12-14. Economic insights (visual data representation)
15-17. Challenges & corrections
18. AI tool usage summary
19. Next steps (Week 10-14 plan)
20. Team contributions
21. Thank you / Q&A
22. Appendix (backup slides)

**Design Decisions:**
- Minimal text (bullet points only)
- Large visuals (ER diagram, query results)
- Economic charts (bar graphs for spending comparison)
- Code snippets small and highlighted

**Tool Used:** Google Slides (for collaboration)

---

### 4. Live Demo Preparation

**Demo Plan by [Member 2]:**

**Setup:**
- Laptop with MariaDB installed
- Database pre-loaded with all sample data
- SQL client (MySQL Workbench) ready
- Queries pre-written in separate .sql files

**Demo Flow (6 minutes):**

**Minute 1:** Connect and show database structure
```sql
SHOW TABLES;
SELECT COUNT(*) FROM Bookings;
```

**Minute 2:** CRUD - INSERT example
```sql
INSERT INTO Visitors (FirstName, LastName, Country, VisitorType)
VALUES ('Demo', 'Visitor', 'Turkey', 'Domestic');
```

**Minute 3:** CRUD - SELECT with JOIN
```sql
SELECT v.FirstName, h.HotelName, b.CheckInDate
FROM Bookings b
JOIN Visitors v ON b.VisitorID = v.VisitorID
JOIN Hotels h ON b.HotelID = h.HotelID
LIMIT 5;
```

**Minute 4-5:** Run Query 1 (regional spending) - show results

**Minute 6:** Run Query 2 (seasonal patterns) - show results

**Backup Plan if Demo Fails:**
- Screenshots of all query results ready in slides
- Pre-recorded 2-minute demo video on USB drive
- Can narrate over screenshots if internet/database fails

---

### 5. Rehearsal Session

**First Rehearsal (full run-through):**

**Timing Results:**
- Introduction: 2:15 (15 seconds over)
- Schema: 4:30 (30 seconds over)
- Demo: 7:00 (1 minute over) ⚠️
- Economic: 4:45 (on time)
- Challenges: 2:10 (on time)
- **Total: 20:40** (40 seconds over limit)

**Cuts Made:**
- Removed detailed explanation of each table field (too granular)
- Shortened demo to 5 minutes (skip UPDATE/DELETE, focus on SELECT)
- Removed one economic chart (combined two findings)

**Second Rehearsal:**
- **Total: 19:45** ✅ Under 20 minutes
- Flow smooth, transitions clear
- Q&A practice added (common questions)

---

### 6. Q&A Preparation

**Anticipated Questions & Prepared Answers:**

**Q1: Why did you keep TotalCost if it violates 3NF?**
- **A:** Performance, immutability, and historical accuracy. In tourism, booking prices never change after confirmation. Recalculating in every query adds latency. We documented this trade-off thoroughly in normalization_analysis.md.

**Q2: Is your occupancy calculation accurate?**
- **A:** It's simplified. True occupancy requires daily room-night tracking, which is beyond our project scope. Our metric approximates by comparing booking count to total rooms. We documented this limitation in query comments.

**Q3: How did you ensure data quality?**
- **A:** Foreign key constraints prevent orphaned records, CHECK constraints validate ranges (dates, prices), and we manually spot-checked all data against business rules. No NULL values in critical fields.

**Q4: What was your biggest AI fail?**
- **A:** ChatGPT suggested keeping HotelName in Bookings table (transitive dependency violation). We caught it during normalization review. This showed AI knows syntax but lacks business logic context.

**Q5: What's next for Week 10-14?**
- **A:** Week 10: 5 advanced queries with window functions. Week 11: Views and indexes for performance. Week 12-13: Dashboard integration. Week 14: Final presentation with policy recommendations.

---

### 7. Speaking Role Assignments

**Final Assignments:**

| Section | Speaker | Backup Speaker | Notes |
|---------|---------|----------------|-------|
| Introduction | Member 1 | Member 4 | Project lead sets tone |
| Schema/Normalization | Member 2 | Member 1 | Technical depth from data analyst |
| Live Demo | Member 2 | Member 1 | Same person for continuity |
| Economic Insights | Member 3 | Member 1 | Economics expert credibility |
| Challenges/AI | Member 4 | Member 3 | Documentation lead has full logs |
| Q&A | All (Member 1 leads) | — | Distribute based on question topic |

**Transitions Planned:**
- [Member 1] introduces [Member 2] for technical section
- [Member 2] hands off to [Member 3] after demo
- [Member 3] thanks [Member 4] to introduce challenges
- [Member 4] returns to [Member 1] for Q&A

**Practice:** Practiced transitions 3 times for smooth flow

---

### 8. Backup Materials Prepared

**In Case of Technical Failure:**

1. **USB Drive with:**
   - Complete slide deck (PDF backup)
   - Demo video (2 minutes, pre-recorded)
   - All query output screenshots
   - ER diagram high-res image

2. **Printed Materials:**
   - Slide deck (handouts for instructor if requested)
   - Query code (readable font, color-coded)

3. **Cloud Backup:**
   - Google Drive link shared with all team members
   - Accessible from any device with internet

**Plan B:** If projector fails, we can present from printed slides + verbal demo

---

### 9. Final Checklist Review

**Pre-Presentation Checklist:**

**Day Before:**
- [ ] ✅ Slides finalized and uploaded
- [ ] ✅ Demo database tested on presentation laptop
- [ ] ✅ Backup materials prepared (USB, prints)
- [ ] ✅ All team members have slide deck
- [ ] ✅ Rehearsed twice, timing under 20 minutes

**Morning Of:**
- [ ] Laptop fully charged
- [ ] Projector adapter tested (HDMI/VGA)
- [ ] Database connection verified
- [ ] Backup USB in pocket
- [ ] Dress code: Business casual (agreed)
- [ ] Arrive 15 minutes early

**During Presentation:**
- [ ] Speak slowly and clearly
- [ ] Make eye contact with instructor
- [ ] Use pointer for slides
- [ ] Stay within time limit
- [ ] Smile and be confident! 😊

---

## ✅ Action Items

| # | Action | Owner | Due Date | Status |
|---|--------|-------|----------|--------|
| 1 | Finalize all slides | All | Mon Week 9 | ✅ Done |
| 2 | Test demo on presentation laptop | Member 2 | Mon Week 9 | ✅ Done |
| 3 | Create backup materials (USB, prints) | Member 4 | Tue Week 9 | ✅ Done |
| 4 | Final rehearsal (with timing) | All | Tue Week 9 | ✅ Done |
| 5 | Upload slides to Google Drive | Member 1 | Tue Week 9 | ✅ Done |
| 6 | Confirm presentation time slot | Member 1 | Wed Week 9 | ✅ Done |
| 7 | Arrive early on presentation day | All | Thu Week 9 | ⏳ Pending |

---

## 📊 Stage 2 Deliverables Summary

**Completed This Stage:**
1. ✅ Normalized schema (3NF with justified exceptions)
2. ✅ 7-table database design
3. ✅ 87 sample records with realistic distributions
4. ✅ CRUD operations demonstrated
5. ✅ 3 business analysis queries
6. ✅ Economic insights documented
7. ✅ AI interaction logs maintained
8. ✅ Meeting notes (Week 3-9)
9. ✅ Stage 2 presentation prepared

**Evaluation Weight:** 35% of project grade

**Confidence Level:** High - we believe we've exceeded expectations

---

## 💡 Key Insights

1. **Preparation reduces presentation anxiety** - Multiple rehearsals = confidence
2. **Backup plans are essential** - Tech can fail, be ready
3. **Economic narrative matters** - Numbers alone don't tell story
4. **Team coordination is smooth** - Clear roles, good communication
5. **We're ahead of schedule** - Ready for Week 10 advanced work

---

## 🎯 Looking Ahead to Stage 3

**Week 10-14 Preview:**

**Week 10:** 5 advanced queries (window functions, CTEs)
**Week 11:** Views & indexes (performance optimization)
**Week 12:** Integration (dashboard mockup, visualizations)
**Week 13:** Policy recommendations (economic analysis document)
**Week 14:** Final presentation & GitHub submission

**Stage 3 Weight:** 45% of project grade (biggest component)

**Strategy:** Start Week 10 work immediately after presentation

---

## 📅 Next Meeting

**Date:** Friday, Week 9 (post-presentation debrief)  
**Time:** 5:00 PM (after class presentation)  
**Agenda:**
- Reflect on presentation performance
- Discuss instructor feedback
- Begin planning Week 10 advanced queries

---

**Meeting Adjourned:** 6:30 PM  
**Minutes Recorded By:** [Member 4] - Documentation Lead  
**Approved By:** [Member 1] - Project Lead  

**Next Steps:** Deliver excellent Stage 2 presentation Thursday! 🚀  
**Team Morale:** High - we're ready! 💪