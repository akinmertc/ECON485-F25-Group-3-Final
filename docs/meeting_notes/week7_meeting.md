# ECON485 Project 3 - Meeting Notes: Week 7

**Meeting Date:** Thursday, Week 7 (Fall 2025)  
**Meeting Type:** Business Query Development & Economic Analysis  
**Duration:** 2 hours  
**Location:** Team Video Call (Zoom)

## 📋 Attendees

- ✅ Mert Akin - Project Lead
- ✅ Kaan Erdemir - Data Analyst  
- ✅ Yaren Yamak - Economic Analyst
- ✅ Oraz - Documentation Lead

## 🎯 Meeting Objectives

1. Review Week 6 CRUD operations completion
2. Develop 3 business analysis queries
3. Define economic interpretation for each query
4. Validate query results against sample data
5. Prepare for Week 8 exam (no deliverables)

---

## 📝 Discussion Summary

### 1. Week 6 CRUD Completion Review

**Status Report by Kaan Erdemir:**

✅ **Completed:**
- schema.sql executed successfully (all 7 tables created)
- 85+ sample records inserted across all tables
- CRUD operations demonstrated (INSERT, SELECT, UPDATE, DELETE)
- Foreign key constraints tested and working
- Transaction examples included

✅ **Data Distribution:**
- 10 Regions (Turkey geographic coverage)
- 15 Hotels (3.5-5.0 star range)
- 16 Visitors (50% domestic, 50% international)
- 16 Bookings (2024-2025, seasonal distribution)
- 17 Expenditures (diverse spending categories)

✅ **Sample Data Quality:**
- No orphaned records
- Realistic pricing (seasonal variation)
- Proper date ranges (CheckOut > CheckIn)
- Balanced geographic distribution

**Team Validation:** All members tested queries locally - all passed ✅

---

### 2. Business Query Selection

**Led by:** Yaren Yamak (Economic Analyst)

**Query Selection Criteria:**
1. Must demonstrate economic insight
2. Must use multi-table JOINs
3. Must include aggregations
4. Must support tourism board decision-making

**Queries Selected (3 required):**

**Query 1: Average Spending Per Visitor by Region**
- **Business Question:** Which regions generate highest visitor spending?
- **Use Case:** Resource allocation, marketing budget decisions
- **Economic Relevance:** Regional economic impact assessment

**Query 2: Hotel Occupancy Rate and Revenue by Season**
- **Business Question:** How does seasonality affect hotel performance?
- **Use Case:** Dynamic pricing strategy, staff planning
- **Economic Relevance:** Seasonal employment patterns, revenue volatility

**Query 3: Visitor Demographics and Spending Patterns**
- **Business Question:** Which visitor segments are most valuable?
- **Use Case:** Targeted marketing campaigns
- **Economic Relevance:** International vs domestic tourist economic contribution

**Team Vote:** Approved 4/0 ✅

---

### 3. Query Development Process

**Query 1 Development:**

**Initial Attempt by Kaan Erdemir:**
```sql
SELECT RegionName, SUM(Amount) 
FROM Regions r
JOIN Expenditures e ON r.RegionID = e.RegionID
GROUP BY RegionName;
```

**Issue Identified:** Missing accommodation spending (only shows expenditures)

**Refined Version (with team input):**
- Added Bookings table JOIN for accommodation revenue
- Added visitor count with COUNT(DISTINCT)
- Added spending breakdown by category (CASE statements)
- Calculated per-visitor averages

**AI Tool Used:** ChatGPT
- Prompt: "How to combine Bookings and Expenditures for total visitor spending?"
- Response: Suggested LEFT JOINs and COALESCE
- **Correction:** Team refined HAVING clause logic

---

**Query 2 Development:**

**Challenge:** How to classify bookings by season?

**Discussion:**
- Kaan Erdemir: "Seasons table doesn't directly link to Bookings"
- Yaren Yamak: "We need derived relationship based on CheckInDate"
- Mert Akin: "Use CASE statement with MONTH() function"

**Solution:** CASE WHEN for seasonal classification
```sql
CASE 
    WHEN MONTH(CheckInDate) IN (6,7,8,12,1) THEN 'Peak'
    WHEN MONTH(CheckInDate) IN (4,5,9,10) THEN 'Shoulder'
    ELSE 'Off-Season'
END AS Season
```

**Occupancy Calculation Challenge:**
- True occupancy requires daily room-night tracking
- We simplified: bookings / total rooms (approximation)
- Documented limitation in query comments

---

**Query 3 Development:**

**Initial Complexity:** Too many JOINs (5 tables)

**Simplification Process:**
1. Started with Visitors as base
2. LEFT JOIN Bookings (some visitors might not have bookings yet)
3. LEFT JOIN Expenditures
4. Added RoomTypes for preference analysis
5. Used GROUP_CONCAT for room type list

**AI Tool Used:** GitHub Copilot
- Autocompleted JOIN syntax
- Suggested GROUP_CONCAT for room types
- **Correction:** Fixed aggregation logic (SUM before divide, not after)

---

### 4. Economic Interpretation Session

**Led by:** Yaren Yamak (Economic Analyst)

**Query 1 Economic Insights:**

**Finding:** Istanbul shows 505 TL average spending per visitor
- **Interpretation:** Urban tourism commands premium due to cultural attractions
- **Policy Implication:** Invest in Istanbul tourism infrastructure
- **Comparison:** 2x higher than rural regions (Pamukkale: 255 TL)

**Economic Concept:** Agglomeration economies in tourism
- Concentration of attractions increases willingness-to-pay
- Network effects: restaurants, shopping, activities cluster

**Finding:** Cappadocia high activity spending (hot air balloons)
- **Interpretation:** Experience-based tourism = high margins
- **Business Implication:** Promote unique experiences over commodity tourism

---

**Query 2 Economic Insights:**

**Finding:** Peak season 50% of bookings, 60% of revenue
- **Interpretation:** Severe seasonality creates economic volatility
- **Labor Market Impact:** Seasonal unemployment in off-season
- **Policy Challenge:** How to smooth demand across year?

**Economic Concept:** Price discrimination by season
- Peak: +30-50% pricing (inelastic demand)
- Off-season: -40% discounts (elastic demand)
- Optimal dynamic pricing maximizes revenue

**Finding:** 5-star hotels maintain better off-season occupancy
- **Interpretation:** Luxury market less price-sensitive
- **Business Implication:** Quality investment = demand stability

---

**Query 3 Economic Insights:**

**Finding:** International visitors spend 2,266 TL vs domestic 892 TL
- **Interpretation:** 2.5x multiplier effect from international tourism
- **Currency Effect:** Strong foreign currencies boost spending power
- **Policy Priority:** Marketing to high-income countries (UK, Germany, Gulf)

**Economic Concept:** Tourism export earnings
- International tourism = "invisible export"
- Improves balance of payments
- Foreign exchange generation

**Finding:** Longer stays correlate with higher total spending
- **Interpretation:** Length of stay (LOS) = key KPI
- **Business Strategy:** Incentivize extended stays (package deals)

---

### 5. Query Testing and Validation

**Testing Process:**

**Step 1: Syntax Validation**
- All queries executed without errors ✅
- No NULL aggregation issues ✅

**Step 2: Logic Validation**
- Manual spot-checks against raw data
- Example: Visitor 1 bookings + expenditures = calculated total ✅
- Seasonal classification matches calendar ✅

**Step 3: Edge Case Testing**
- Regions with no expenditures (handled with LEFT JOIN) ✅
- Visitors with no bookings (excluded with HAVING) ✅
- Division by zero (used NULLIF) ✅

**Step 4: Performance Check**
- All queries complete in <100ms on sample data ✅
- Indexes on foreign keys helping JOIN performance ✅

**Issues Found & Fixed:**

**Issue 1:** Query 1 initially showed NULL for regions without visitors
- **Fix:** Changed INNER JOIN to LEFT JOIN, added HAVING filter

**Issue 2:** Query 2 occupancy calculation showed >100%
- **Fix:** Realized multi-night bookings inflate count, added note about limitation

**Issue 3:** Query 3 double-counted visitors with multiple bookings
- **Fix:** Added COUNT(DISTINCT VisitorID)

---

### 6. Documentation Standards

**Query Documentation Requirements (agreed):**

**Each query must include:**
1. **Business Question** - Plain English problem statement
2. **Use Case** - Who uses this query and why?
3. **Economic Insight** - What economic principle is revealed?
4. **Expected Output** - Sample results in comments
5. **Query Explanation** - Step-by-step logic breakdown

**Example Format:**
```sql
-- ========================================
-- QUERY 1: Average Spending Per Visitor
-- ========================================
-- Business Question: Which regions generate highest spending?
-- Use Case: Tourism board resource allocation
-- Economic Insight: Regional economic impact varies 2x-3x
-- [Query here]
-- Expected Output: [Sample results]
```

**Assigned:** Oraz to ensure all queries follow this format

---

### 7. Preparation for Week 9 Presentation

**Early Planning Discussion:**

**Stage 2 Presentation Topics:**
1. Schema design (normalization decisions)
2. Live demo of CRUD operations
3. Business query results (Query 1-3)
4. Economic insights discovered
5. AI tool usage reflections
6. Challenges overcome

**Slide Responsibilities:**
- Mert Akin: Schema & design overview
- Kaan Erdemir: Technical implementation & demo
- Yaren Yamak: Economic analysis & insights
- Oraz: AI learning & team process

**Demo Plan:**
- Run queries live (backup: screenshots if internet fails)
- Show query → result → interpretation flow
- 15-20 minute presentation target

---

## ✅ Action Items

| # | Action | Owner | Due Date | Status |
|---|--------|-------|----------|--------|
| 1 | Finalize all 3 business queries | Kaan Erdemir | Fri Week 7 | ✅ Done |
| 2 | Write economic interpretation for each query | Yaren Yamak | Fri Week 7 | ✅ Done |
| 3 | Add comprehensive comments to SQL file | Oraz | Sat Week 7 | ✅ Done |
| 4 | Test queries on clean database reload | All | Weekend | ✅ Done |
| 5 | Update ai_logs.md with query development | Oraz | Sun Week 7 | ✅ Done |
| 6 | Begin Stage 2 presentation outline | Mert Akin | Week 8 | ⏳ Pending |
| 7 | Prepare for Week 8 exam (no project work) | All | Week 8 | — |

---

## 🤔 Questions / Concerns

**Q: Should we add more than 3 queries?**
- **A:** Assignment requires 3. We can add more in Week 10 for advanced queries.

**Q: Occupancy calculation is simplified - is that acceptable?**
- **A:** Yes, we documented the limitation. True occupancy requires daily tracking beyond project scope.

**Q: Should economic insights be in SQL comments or separate doc?**
- **A:** Both. Brief notes in SQL, detailed analysis in presentation.

---

## 📅 Next Meeting

**Week 8:** No meeting (exam week)

**Week 9 Meeting:**  
**Date:** Monday, Week 9  
**Time:** 4:00 PM  
**Agenda:**
- Stage 2 presentation rehearsal
- Query demo practice
- Finalize slides
- Assign speaking roles

---

## 💡 Key Insights

1. **Economic context makes queries meaningful** - Raw numbers alone aren't insights
2. **Seasonality dominates Turkish tourism** - 50% revenue in 3 months creates challenges
3. **International tourism disproportionately valuable** - 2.5x spending multiplier
4. **Query complexity vs clarity trade-off** - Simplified occupancy calc for understandability
5. **AI helps with syntax, humans with logic** - Copilot autocomplete useful but needs validation

---

## 📊 Query Results Summary

### Query 1: Regional Spending
| Region | Avg Spending/Visitor |
|--------|---------------------|
| Istanbul | 505 TL |
| Antalya | 377 TL |
| Cappadocia | 255 TL |

### Query 2: Seasonal Performance
| Season | Bookings | Avg Price |
|--------|----------|-----------|
| Peak | 8 (50%) | 320 TL |
| Shoulder | 5 (31%) | 170 TL |
| Off-Season | 3 (19%) | 130 TL |

### Query 3: Visitor Segments
| Type | Spending/Visitor |
|------|-----------------|
| International | 2,266 TL |
| Domestic | 892 TL |

---

## 📚 Resources Referenced

- Turkish Tourism Statistics (validation of seasonality patterns)
- Hotel revenue management literature (dynamic pricing)
- Tourism economics textbooks (multiplier effects)
- SQL aggregate function documentation

---

**Meeting Adjourned:** 6:00 PM  
**Minutes Recorded By:** Oraz - Documentation Lead  
**Approved By:** Mert Akin - Project Lead  

**Next Steps:** Week 8 exam preparation, Week 9 presentation development