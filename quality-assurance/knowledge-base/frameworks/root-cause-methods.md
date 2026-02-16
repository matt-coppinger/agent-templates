# Root Cause Analysis Methodology Guide

## 1. Five Whys

A simple iterative technique for drilling down to the root cause of a problem.

### Process
1. **Define the problem** clearly and specifically
2. **Ask "Why?"** — why did this problem occur?
3. **Answer with facts**, not opinions or assumptions
4. **Repeat** — ask "Why?" for each answer (typically 3-5 levels)
5. **Stop** when you reach a cause that, if addressed, would prevent recurrence

### Tips
- Each "Why" answer must be supported by evidence or data
- If you get multiple answers at one level, follow each branch
- The root cause is usually a process or system failure, not a person
- Avoid stopping too early (symptom) or going too deep (impractical)

### Example
- **Problem:** Customer received incorrect part
- **Why 1:** Wrong part was packed → packing list had wrong part number
- **Why 2:** Packing list was wrong → order entry error
- **Why 3:** Order entry error → part numbers are similar (AB-1234 vs AB-1243)
- **Why 4:** Similar part numbers → no verification step in order entry
- **Root cause:** Order entry process lacks part number verification check

## 2. Ishikawa (Fishbone) Diagram

A structured brainstorming tool using the 6M categories.

### The 6M Categories

| Category | Also Known As | Typical Causes |
|----------|---------------|----------------|
| **Man** | People, Personnel | Training gaps, fatigue, experience, procedures not followed |
| **Machine** | Equipment | Calibration drift, maintenance overdue, wear, capability |
| **Material** | Inputs | Supplier variation, out-of-spec, storage degradation |
| **Method** | Process | Procedure gaps, sequence errors, work instruction clarity |
| **Measurement** | Inspection | Instrument accuracy, sampling plan, test method validity |
| **Mother Nature** | Environment | Temperature, humidity, contamination, vibration, lighting |

### Process
1. Write the problem (effect) at the head of the fish
2. Draw the six main category bones
3. Brainstorm potential causes under each category
4. For each cause, ask "Why?" to identify sub-causes
5. Identify the most likely causes based on evidence
6. Verify with data before concluding

## 3. Fault Tree Analysis (FTA)

A top-down, deductive approach for complex failures.

### When to Use
- Safety-critical failures
- Complex systems with multiple potential failure modes
- When you need to quantify failure probability

### Process
1. Define the top event (undesired outcome)
2. Identify immediate causes using AND/OR gates
3. Continue decomposing until you reach basic events
4. Evaluate probability of each basic event
5. Calculate probability of top event

## 4. Pareto Analysis

The 80/20 rule applied to quality: 80% of problems come from 20% of causes.

### Process
1. Collect defect data by type/category
2. Count frequency of each type
3. Sort in descending order
4. Calculate cumulative percentage
5. Identify the "vital few" (those contributing to ~80%)
6. Focus improvement efforts on the vital few

### Interpretation
- Steep curve = few dominant causes (good — clear targets)
- Flat curve = many equal causes (harder — systemic issue)
- Changes in Pareto over time indicate whether improvements are working

## 5. Is/Is-Not Analysis

A structured approach to narrowing down the cause.

| Dimension | IS (where/when it happens) | IS NOT (where/when it doesn't) | Distinction |
|-----------|---------------------------|-------------------------------|-------------|
| What | Which defect type? | Which types are not occurring? | What's unique? |
| Where | Which location/line/station? | Which are unaffected? | What's different? |
| When | What time/shift/date? | When does it not occur? | What changed? |
| Extent | How many? How severe? | What's the boundary? | What limits it? |

## Choosing the Right Method

| Situation | Recommended Method |
|-----------|-------------------|
| Simple, single-cause problem | 5 Whys |
| Multiple potential cause categories | Ishikawa |
| Complex system failure | Fault Tree Analysis |
| Prioritising where to focus | Pareto Analysis |
| Narrowing down from many variables | Is/Is-Not |
| General starting point | Ishikawa → 5 Whys on top causes |
