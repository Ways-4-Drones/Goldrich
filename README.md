# Scheduling Under Uncertainty
### A Case Study in Health Operations Management

**Strome College of Business, Old Dominion University**

**Lawrence J. Goldrich Institute for NeuroHealth**

---

## Overview

This repository hosts the public-facing materials for an experiential MBA case study developed in partnership with the [Lawrence J. Goldrich Institute for NeuroHealth](https://www.odu.edu/medicine/centers/lawrence-j-goldrich-institute-for-integrated-neuro-health) at Old Dominion University. Students take on the role of operations consultants advising the clinic's leadership on how to improve provider scheduling efficiency at a real dementia specialty clinic serving the Hampton Roads region of Virginia.

The case was developed with significant AI assistance (Claude, Anthropic). All clinical content was reviewed and verified by faculty against primary sources.

**Live case study:** [ways-4-drones.github.io/Goldrich/Goldrich_Case_Study.html](https://ways-4-drones.github.io/Goldrich/Goldrich_Case_Study.html)

---

## The Problem

The Goldrich Institute's Comprehensive Memory Clinic (CMC) currently operates at a provider utilization rate of approximately 60% — meaning four out of every ten available appointment slots go unfilled each week, despite a growing waiting list. The problem is not a shortage of patients. It is a scheduling process that does not reliably match available capacity to patient demand.

Students are asked to diagnose the root causes of this gap, design and test new scheduling policies using a simulation tool, and deliver an evidence-based recommendation to clinic leadership. The best submissions are shared — with student permission — directly with the Institute's Executive Director.

---

## Simulation Tool

The centerpiece of the case is a purpose-built discrete-event simulation model built in Python and delivered as a Google Colab notebook. The tool simulates one full year of clinic operations, incorporating:

- **Four providers** on a fixed weekly schedule (10 provider-shifts per day, ~22 per week)
- **3,120 synthetic patients** drawn from US Census data for the clinic's 30-ZIP-code catchment area, with severity scores, drive times, and visit duration distributions calibrated to the clinic's population
- **Real NOAA weather data** from the Norfolk Airport station, used to model patient tardiness and no-show probabilities
- **Stochastic patient behavior** including tardiness, no-shows, and visit duration variation driven by severity

Students adjust scheduling policy settings, run the simulation, and immediately see a comparison against the pre-computed baseline in Block 3.

**Open the simulation tool:** [Google Colab](https://colab.research.google.com/drive/1c9R25UcCMlAUwUSgjqVm2dAcCQi4H8uV?usp=sharing)

### Policy Levers

| Section | Lever | Default |
|---|---|---|
| Capacity | Patients per shift | 4 |
| Capacity | Slot duration (min) | 75 |
| Severity Rules | Max high-severity patients per shift | 4 (no cap) |
| Resilience | Buffer time between appointments (min) | 0 |
| Advanced | Severity-tiered slot lengths | Off |
| Advanced | Cluster high-severity patients on one day | Off |
| Advanced | Overbook by 1 patient per shift | Off |
| Advanced | Geographic scheduling hedge | Off |
| Additional Challenge | Rotate undesirable shifts equitably | Off |
| Additional Challenge | Severity-based provider routing | On |

### Key Performance Indicators

The simulation compares policies against the baseline on eight KPIs: provider utilization, total patients seen, average idle time per shift, percentage of shifts running over, total no-shows, average patient wait time, provider equity index, and empty shifts.

---

## Course Integration

The case study is designed for an MBA-level operations management course. It maps to four course learning objectives:

- **CLO1** — Identifying the strategic role of operations in organizational performance
- **CLO2** — Designing innovative operations practices that offer competitive advantage
- **CLO3** — Evaluating systems using analytical tools and methodologies
- **CLO4** — Deploying strategies that accommodate changing conditions

### Module Learning Objectives

1. Evaluate clinic scheduling operations using simulation-based analysis to identify root causes of capacity underutilization *(CLO3)*
2. Design and test scheduling policies that balance competing operational objectives and articulate the trade-offs of each choice *(CLO2, CLO4)*
3. Communicate evidence-based recommendations to a non-technical stakeholder audience, connecting findings to organizational strategy *(CLO1)*

### Assignment

Students submit a 12-minute recorded presentation with 6–18 slides, accompanied by two CSV files exported from the simulation tool (`policy_results.csv` and `policy_summary.csv`). Submissions are graded on problem diagnosis, policy design and trade-off analysis, evidence quality, and executive delivery. An extra credit question asks students to evaluate two structural policies currently in place at the clinic: annual schedule-setting and severity-based provider routing.

---

## Repository Contents

```
/
├── Goldrich_Case_Study.html         # Self-contained case study (6 tabbed pages)
├── fig4_catchment_map.html          # Interactive patient catchment map (Folium)
├── figures/
│   ├── fig_schedule.png             # Provider weekly schedule grid
│   ├── fig_weather.png              # 2025 weather conditions by month
│   ├── fig_severity.png             # Patient severity distribution
│   ├── fig_a1_kpi_scorecard.png     # A1 — KPI scorecard
│   ├── fig_a2_heatmap.png           # A2 — Utilization heatmap
│   ├── fig_a3_utilization_week.png  # A3 — Clinic utilization by week
│   ├── fig_a4_provider_heatmaps.png # A4 — Provider shift heatmaps
│   ├── fig_a5_idle_time.png         # A5 — Idle time by provider
│   ├── fig_a6_severity_band.png     # A6 — Severity band comparison
│   ├── fig_a7_day_of_week.png       # A7 — Utilization by day of week
│   └── fig_a8_weather_condition.png # A8 — Utilization by weather condition
└── README.md
```

The simulation notebook and instructor tools (validation notebook, KPI comparator) are maintained separately and distributed through Canvas.

---

## Technical Notes

### Simulation Design

The simulation is a discrete-event model implemented in Python (~1,200 lines) and delivered as a Google Colab notebook requiring no software installation. The baseline run is pre-computed and embedded in the notebook as a gzip-compressed JSON payload (~150 KB base64-encoded), ensuring identical results across all students regardless of network conditions.

Weather data is fetched from a publicly shared Google Drive CSV at runtime and falls back to a synthetic record (seed 42) if unavailable. The synthetic record is calibrated to Norfolk's historical climate: approximately 90 rainy days and 8 snowy days distributed realistically across 2025.

Patient tardiness and no-show probabilities are modeled as functions of severity, drive time, and weather condition. Visit durations are drawn from severity-specific distributions calibrated to neurology specialty clinic benchmarks.

### Instructor Tools

Two additional Colab notebooks are available for instructors:

- **Submission Validator** — uploads a student's `policy_results.csv`, checks structural integrity, verifies weather flag consistency against the canonical 2025 record, and derives KPIs directly from the submitted data for comparison against the student's stated results
- **KPI Comparator** — loads all submissions from a Google Drive folder, validates each, and produces comparison charts suitable for class presentation and clinic briefing

---

## Community Engagement

This case study is an example of community-engaged pedagogy and a direct feedback loop between student work and organizational decision-making. The Goldrich Institute's leadership is aware of the course, and the strongest student submissions are shared with the Executive Director at the end of each semester.

The case was first offered in Spring 2026. It is designed to be updated annually as the clinic's Epic EHR system (adopted July 2025) generates richer operational data, and as the simulation model is refined based on student feedback and faculty review.

