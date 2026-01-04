# ECON485 Project 3 - Meeting Notes: Week 5

**Meeting Date:** Tuesday, Week 5 (Fall 2025)  
**Meeting Type:** Normalization Review & SQL Schema Finalization  
**Duration:** 90 minutes  
**Location:** Library Study Room B

## 📋 Attendees

- ✅ [Member 1] - Project Lead
- ✅ [Member 2] - Data Analyst  
- ✅ [Member 3] - Economic Analyst
- ✅ [Member 4] - Documentation Lead

## 🎯 Meeting Objectives

1. Review Stage 1 submission feedback
2. Complete 3NF normalization analysis
3. Finalize SQL schema (schema.sql)
4. Address intentional denormalizations
5. Plan Week 6 CRUD operations

---

## 📝 Discussion Summary

### 1. Stage 1 Feedback Review

**Instructor Feedback Received:**
- ✅ "Good initial scope and entity selection"
- ✅ "ER diagram is clear and well-organized"
- ⚠️ "Consider whether TotalCost should be stored or calculated"
- 💡 "Think about seasonal pricing - might need additional table"

**Team Response:**
- TotalCost decision to be analyzed in normalization document
- HotelRoomPricing table added as optional enhancement

---

### 2. Normalization Analysis

**Led by:** [Member 2] (Data Analyst)

**3NF Compliance Check Results:**

**✅ Tables in Full 3NF:**
1. Regions - No transitive dependencies
2. Visitors - All attributes depend directly on VisitorID
3. RoomTypes - Simple lookup table
4. Seasons - No derived attributes
5. Expenditures - Clean dependency structure

**⚠️ Potential 3NF Violations Discussed:**

**Issue 1: Hotels Table - City and ZipCode**
- **Problem:** ZipCode → City (transitive dependency)
- **Discussion:**
  - [Member 2]: "Technically violates 3NF"
  - [Member 1]: "But creating separate Locations table seems excessive"
  - [Member 3]: "In Turkey, addresses rarely change for hotels"
- **Decision:** Accept denormalization, document in analysis
- **Rationale:** Practical convenience outweighs theoretical purity

**Issue 2: Bookings Table - TotalCost**
- **Problem:** TotalCost = PricePerNight × (CheckOutDate - CheckInDate)
- **Discussion:**
  - [Member 2]: "Clear transitive dependency"
  - [Member 3]: "But hotels never change historical booking prices"
  - [Member 1]: "Recalculating in every query adds latency"
  - [Member 4]: "Historical accuracy is important for analytics"
- **Decision:** Keep TotalCost, heavily justify in document
- **Rationale:** Performance + immutability + historical accuracy

**Voting Results:**
- Keep TotalCost: 4/4 unanimous
- Document as intentional denormalization: Approved

---

### 3. SQL Schema Finalization

**Presented by:** [Member 2] (Data Analyst)

**Schema Components Reviewed:**

**Tables (7 core + 1 optional):**
```sql
✅ Regions (8 fields)
✅ Hotels (11 fields) 
✅ Visitors (10 fields)
✅ RoomTypes (4 fields)
✅ Seasons (6 fields)
✅ Bookings (11 fields)
✅ Expenditures (8 fields)
⭐ HotelRoomPricing (6 fields - optional)
```

**Constraints Added:**
- CHECK constraints for data validation
- FOREIGN KEY with CASCADE/RESTRICT
- UNIQUE constraints where appropriate
- DEFAULT values for timestamps

**Indexes Planned:**
- Primary keys (automatic)
- Foreign keys (manual indexes)
- Frequently queried fields (Region, Date ranges)

**Data Types Confirmed:**
- INT for IDs (AUTO_INCREMENT)
- VARCHAR for text (appropriate lengths)
- DECIMAL(10,2) for money
- DATE for dates, TIMESTAMP for audit trails
- ENUM for constrained values

---

### 4. Denormalization Justification Document

**Discussion Points:**

**Why We're Keeping Denormalizations:**

1. **TotalCost in Bookings:**
   - **Performance:** Queried in 80% of revenue reports
   - **Immutability:** Booking costs never change after confirmation
   - **Historical Accuracy:** Preserves pricing at time of booking
   - **Alternative Rejected:** Calculated views too slow

2. **Address Components in Hotels:**
   - **Convenience:** Common practice in address storage
   - **Low Risk:** Hotel addresses stable (rarely change)
   - **Query Simplicity:** No JOINs needed for basic info

**Documentation Strategy:**
- Create detailed normalization_analysis.md
- Explain each violation with business justification
- Reference academic sources on denormalization trade-offs
- Include instructor feedback consideration

---

### 5. Database Creation Plan

**Week 6 Activities Outlined:**

**Day 1-2: Schema Implementation**
- Execute schema.sql in MariaDB
- Verify all constraints work
- Test foreign key cascades

**Day 3-4: Sample Data Generation**
- [Member 2] creates Python data generator
- Generate 10 regions, 15 hotels, 15+ visitors
- Ensure realistic seasonal distribution

**Day 5: CRUD Testing**
- INSERT all sample data
- UPDATE examples (status changes, corrections)
- DELETE examples (with foreign key testing)
- SELECT queries with JOINs

**Deliverable:** Working database with 80+ records

---

### 6. AI Tool Usage This Week

**Tools Used:**

**ChatGPT:**
- Prompt: "Review this schema for 3NF violations"
- Response: Identified TotalCost and address issues
- **Correction:** Team provided business context ChatGPT lacked
- **Learning:** AI good at theory, humans needed for practice

**Perplexity AI:**
- Research: "Best practices for denormalization in databases"
- Found academic papers supporting our TotalCost decision
- **Validation:** Industry commonly denormalizes for performance

**dbdiagram.io:**
- Updated ER diagram with final schema
- Added notes about intentional denormalizations
- Exported clean PNG for documentation

**AI Interaction Logged:** All prompts and responses documented in ai_logs.md

---

### 7. Risk Assessment

**Potential Issues Identified:**

**Risk 1: Data Generation Complexity**
- **Issue:** Realistic seasonal patterns difficult to code
- **Mitigation:** [Member 2] will use weighted random for seasons
- **Backup:** Manual data entry if script fails

**Risk 2: Foreign Key Constraint Testing**
- **Issue:** Deleting records with dependencies might be tricky
- **Mitigation:** Test CASCADE vs RESTRICT carefully
- **Plan:** Document expected behaviors

**Risk 3: Time Constraint**
- **Issue:** Week 6 has CRUD + Week 7 has queries
- **Mitigation:** Start data generation this week (Week 5)
- **Plan:** [Member 2] begins Python script immediately

---

## ✅ Action Items

| # | Action | Owner | Due Date | Status |
|---|--------|-------|----------|--------|
| 1 | Complete normalization_analysis.md | Member 2 | Thu Week 5 | ✅ Done |
| 2 | Finalize schema.sql with all constraints | Member 2 | Thu Week 5 | ✅ Done |
| 3 | Update ER diagram with final design | Member 1 | Fri Week 5 | ✅ Done |
| 4 | Begin Python data generator script | Member 2 | Fri Week 5 | 🔄 In Progress |
| 5 | Test schema.sql on local MySQL/MariaDB | All | Weekend | ⏳ Pending |
| 6 | Update AI logs with Week 5 interactions | Member 4 | Fri Week 5 | ✅ Done |
| 7 | Review normalization document | All | Mon Week 6 | ⏳ Pending |

---

## 🤔 Questions / Concerns

**Q: Should we implement triggers for TotalCost validation?**
- **A:** No, keep it simple. Application-level validation sufficient for this project.

**Q: Do we need stored procedures?**
- **A:** Not required by assignment. Focus on queries in Week 7+.

**Q: What if instructor disagrees with denormalization?**
- **A:** We have solid justification document. Willing to discuss trade-offs.

---

## 📅 Next Meeting

**Date:** Friday, Week 5  
**Time:** 3:00 PM  
**Agenda:**
- Review completed normalization document
- Test schema.sql execution
- Finalize data generation approach
- Prepare for Week 6 CRUD operations

---

## 💡 Key Insights

1. **3NF is a guideline, not absolute law** - Business needs justify exceptions
2. **Performance vs purity trade-off** - TotalCost decision demonstrates mature thinking
3. **Documentation is critical** - Justifying design choices shows understanding
4. **AI limitations** - ChatGPT knows theory but lacks business context
5. **Team consensus** - Unanimous vote on major design decisions builds confidence

---

## 📚 Resources Referenced

- Silberschatz: Database System Concepts (Chapter 7 - Normalization)
- Academic paper: "When to Denormalize" (Referenced in decision)
- Course Homework 1: Normalization requirements
- Instructor Stage 1 feedback

---

**Meeting Adjourned:** 4:30 PM  
**Minutes Recorded By:** [Member 4] - Documentation Lead  
**Approved By:** [Member 1] - Project Lead  

**Next Steps:** Complete normalization document, begin Week 6 CRUD implementation
