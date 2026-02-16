# QA Key Performance Indicator Definitions

## Primary KPIs

### First Pass Yield (FPY)
- **Definition:** Percentage of units passing inspection without rework or repair
- **Formula:** `(Units passing first inspection / Total units inspected) × 100`
- **Target:** ≥95%
- **Warning:** <90%
- **Critical:** <85%
- **Frequency:** Daily/weekly

### Defect Rate
- **Definition:** Proportion of defective units in total production
- **Formula:** `(Defective units / Total units produced) × 100`
- **Target:** ≤2%
- **Warning:** >5%
- **Critical:** >10%
- **Frequency:** Daily/weekly

### DPMO (Defects Per Million Opportunities)
- **Definition:** Number of defects per million opportunities for a defect to occur
- **Formula:** `(Number of defects / (Units × Opportunities per unit)) × 1,000,000`
- **Target:** ≤3,400 (equivalent to ~4.2 sigma)
- **Warning:** >6,210 (~4.0 sigma)
- **Critical:** >66,800 (~3.0 sigma)
- **Frequency:** Weekly/monthly

### Cost of Quality (CoQ) Ratio
- **Definition:** Total quality costs as a proportion of revenue
- **Formula:** `(Prevention + Appraisal + Internal failure + External failure costs) / Revenue`
- **Target:** ≤15%
- **Warning:** >25%
- **Critical:** >35%
- **Components:**
  - Prevention: training, process planning, supplier qualification
  - Appraisal: inspection, testing, audits
  - Internal failure: scrap, rework, re-inspection
  - External failure: returns, warranty, complaints
- **Frequency:** Monthly/quarterly

## Secondary KPIs

### Customer Return Rate
- **Definition:** Percentage of shipped units returned due to quality issues
- **Formula:** `(Units returned for quality reasons / Total units shipped) × 100`
- **Target:** ≤1%
- **Warning:** >3%
- **Critical:** >5%
- **Frequency:** Monthly

### Mean Time to Detect (MTTD)
- **Definition:** Average time between defect creation and detection
- **Formula:** `Sum of (detection time - creation time) / Number of defects`
- **Target:** ≤2 hours
- **Warning:** >8 hours
- **Critical:** >24 hours
- **Frequency:** Weekly

### Corrective Action Closure Rate
- **Definition:** Percentage of corrective actions closed within their target timeline
- **Formula:** `(CAs closed on time / Total CAs due) × 100`
- **Target:** ≥90%
- **Warning:** <75%
- **Critical:** <60%
- **Frequency:** Monthly

### Supplier Quality Score
- **Definition:** Composite score of incoming quality from each supplier
- **Formula:** Weighted average of incoming inspection pass rate, delivery conformance, and responsiveness
- **Target:** ≥85%
- **Warning:** <70%
- **Critical:** <50%
- **Frequency:** Quarterly

## Trend Indicators

When reporting KPIs, always include:
- **Current value** against target
- **Trend direction** (improving/stable/deteriorating) over last 3 periods
- **Traffic light status:** 🟢 at or above target, 🟡 in warning zone, 🔴 in critical zone
