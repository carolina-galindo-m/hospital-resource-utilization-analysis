# Hospital Resource Utilization & Efficiency Analysis

**Author:** Carolina Galindo Mendoza  
**Tools:** Python (pandas, matplotlib, seaborn, numpy)  
**Dataset:** Synthetic hospital operations dataset including staffing, patient admissions, and bed allocation across 4 services and 52 weeks [retrived from Kaggle](https://www.kaggle.com/datasets/jaderz/hospital-beds-management?resource=download&select=services_weekly.csv)

**Goal:** Identify where hospital resources are strained, where patients are being turned away, and what operational patterns drive patient satisfaction.

---

## Context

Hospital operations teams face a core challenge: **matching resource supply (beds, staff) to patient demand** without data, this is reactive and inefficient. This project applies exploratory data analysis to a simulated hospital environment to surface the patterns that operational leaders need to act on.

This type of analysis mirrors the work done by healthcare analytics platforms like LiveData, which track perioperative workflow and OR performance metrics to drive real-time operational decisions.

---

## Dataset

4 CSV files covering 1 year of simulated operations:

| File | Description |
|------|-------------|
| `hospital_staff.csv` | 110 staff members across 3 roles, 4 services |
| `hospital_staff_schedule.csv` | Weekly attendance records (52 weeks) |
| `hospital_patients.csv` | 1,000 patient records with arrival, discharge, service, satisfaction |
| `hospital_service_weekly.csv` | Weekly bed availability, demand, admissions, refusals, satisfaction, staff morale |

Services covered: **Emergency, Surgery, General Medicine, ICU**

---

## Key Findings

### 1. Emergency is in crisis - 77% of patients turned away
Emergency operates at **100% bed utilization** while facing demand **5.2x its capacity**. This is the single biggest operational failure in the dataset, 3 in 4 patients requesting emergency care are refused. No other service comes close to this level of strain.

### 2. General Medicine is the second pressure point
With 97% utilization and a 35% refusal rate, General Medicine is quietly overloaded, and likely absorbing spillover from Emergency.

### 3. ICU and Surgery are well-managed
ICU runs at 84% utilization with only a 12% refusal rate; close to the textbook "efficient without being overwhelmed" benchmark. Surgery is similar at 88% utilization and 17% refusals.

### 4. Staff attendance correlates with patient satisfaction, but differently by service
Across services, weeks with higher staff attendance tend to produce better patient satisfaction scores. The relationship is strongest in ICU and Surgery, where consistent staffing directly affects care quality. Emergency shows weaker correlation — likely because satisfaction there is driven more by sheer unmet demand than staffing levels.

### 5. Surgery patients stay longest — ICU has the widest variance
Median length of stay is ~7 days overall, but Surgery patients stay significantly longer. ICU shows the widest range, reflecting the unpredictable nature of critical care cases.

---

## Visualizations

| Figure | Description |
|--------|-------------|
| `fig1_bed_utilization.png` | Average bed utilization rate by service vs. 85% efficiency target |
| `fig2_demand_vs_refusal.png` | Demand pressure vs. refusal rate, 4-quadrant scatter with bubble size = utilization |
| `fig3_refusal_trends.png` | Weekly refusal rate trends across all 4 services over 52 weeks |
| `fig4_attendance_vs_satisfaction.png` | Staff attendance rate vs. patient satisfaction, by service |
| `fig5_length_of_stay.png` | Length of stay distribution (boxplot) by service |

---

## Recommendations

1. **Emergency capacity expansion is the top priority.** A 5.2x demand-to-supply ratio is unsustainable. Options include surge protocols, overflow routing to General Medicine, or bed reallocation during off-peak hours.

2. **Investigate General Medicine overflow.** The 35% refusal rate suggests it may be absorbing Emergency spillover. Tracking cross-service transfers would clarify this.

3. **Use ICU and Surgery as efficiency benchmarks.** Both services maintain strong utilization without excessive refusals, their staffing and scheduling practices are worth replicating.

4. **Build a staffing alert model.** The attendance-satisfaction correlation suggests that low-attendance weeks are a leading indicator of satisfaction drops. A simple threshold alert could trigger proactive scheduling adjustments.

---

## How to Run

```bash
# Install dependencies
pip install pandas matplotlib seaborn numpy

# Run the analysis
python or_utilization_analysis.py
```

Figures will be saved to the `figures/` folder.

---

## Skills Demonstrated

- Data cleaning and feature engineering (pandas)
- Exploratory data analysis across multiple joined datasets
- Data visualization (matplotlib, seaborn); bar charts, scatter plots, line charts, box plots
- Translating analytical findings into operational recommendations
- Healthcare operations domain familiarization
