# Logistics & Fleet Operations — Performance Intelligence Dashboard

## Built with Microsoft Power BI | Multi-Table Logistics Dataset

---

## 🏢 Company Overview

This production-grade analytics project provides an executive-level operational review of a large-scale commercial transport and freight logistics enterprise. The operation manages an extensive asset pool and driver workforce across a highly active domestic distribution network, moving freight across **58 distinct geographic routes** to bridge decentralized supply chain metrics with high-level corporate profitability.

Over the recorded operating timeline, the enterprise processed **85,000 total dispatches**, logged **122 million operational miles**, and generated **$298.62M in Gross Total Revenue**. Despite strong headline performance, the business faces significant challenges from variable fleet maintenance costs, bottom-line fuel waste leaks, safety incidents, and lane-by-lane service delivery bottlenecks—all requiring a centralized business intelligence framework to protect revenue and isolate spend leaks.

---

## 📌 Business Problem Statement

> *"The logistics enterprise generates $298.62M in macroscopic revenue but has operated without structured, single-pane visibility into the underlying drivers of asset efficiency, route profitability, and operational risk mitigation. Top-line performance is healthy, yet variable fleet maintenance costs have reached $5.73M across 72.23K total downtime hours, and idle fuel waste alone leaks an alarming $2.33M from corporate profitability. Furthermore, baseline On-Time Delivery (OTD) rates are capped at 44.61%, meaning over half of all dispatches experience transit disruptions, threatening client retention and contract renewals.*
> 
> *Management requires an integrated analytical architecture that seamlessly consolidates linehaul revenue, system malfunctions, fuel burn efficiency, and compliance risk parameters. This interactive dashboard must enable data-driven executives to immediately target operational cost centers, uncover underperforming corridors, and deploy tactical interventions before variable liabilities compound."*

---

## 📊 Dashboard Architecture Preview

### Page 1 — Executive Financial Overview
*<img width="1271" height="639" alt="image" src="https://github.com/user-attachments/assets/d4581840-3bc2-4235-9c87-ea5d9772f52b" />
*

### Page 2 — Fleet Utilization & Maintenance Deep Dive
*<img width="1271" height="639" alt="image" src="https://github.com/user-attachments/assets/d10af6a3-05c3-498c-8bb0-587ffe3e407d" />
*

### Page 3 — Supply Chain Logistics & Route Profitability
*<img width="1271" height="639" alt="image" src="https://github.com/user-attachments/assets/5821a0f2-b21d-4c52-b09c-2288a2fedcb2" />
*

### Page 4 — Fleet Efficiency & Performance Matrix
*<img width="1271" height="639" alt="image" src="https://github.com/user-attachments/assets/6eab5b3a-6ab7-414e-a041-878f52d116c4" />
*

---

## 🗂️ Dataset Overview

This capstone portfolio architecture utilizes **14 interconnected data files** optimized to handle complex, high-density relational data points.

| Component / Focus | Description | Core Scope |
|---|---|---|
| **Core Dispatches** | Primary transactional tables tracking every trip, distance, and freight movement | 85,000 Trips |
| **Workforce & Drivers** | Driver tracking logs, performance metrics, and compliance scoring | 124 Drivers |
| **Fleet Assets** | Fleet tracking arrays, power unit profiles, and utilization data | 92 Trucks |
| **Network & Routes** | Lane matrices mapping origins, destinations, and corridor lengths | 58 Active Routes |
| **Client Portfolio** | Client profiles, account concentrations, and contract booking segments | Enterprise Accounts |
| **Supply Chain Events** | Service milestone entries capturing pickup, transit, and detention logs | High-Density Logs |
| **Variable Operational Expenses** | Granular fuel purchase logs, gallon consumption, and regional pricing grids | Fleet-Wide Transactions |
| **Equipment Maintenance** | Asset repair tickets, system failures, and mechanical downtime hours | 72.23K Downtime Hours |
| **Safety & Compliance** | Risk exposure tables tracking road infractions, damage costs, and fault flags | 170 Inc infractions |

**Total Operational Distance Modeled: 122,000,000 Miles**

---

## 🔗 Data Model — Table Relationships (Star Schema)

To maximize query performance and eliminate data redundancy, the backend data architecture was engineered using a centralized **Star Schema** optimized for high-density aggregations. Descriptive dimensions filter transactional fact tables via `1:N` (One-to-Many) relationships, utilizing single-direction cross-filtering to keep the data model lean and responsive.


                     DATA MODEL: CENTRALIZED STAR SCHEMA ARCHITECTURE


                             ┌─────────────────────────┐
                             │        Dim_Date         │
                             │  (Central Date Anchor)  │
                             └────────────┬────────────┘
                                          │
                  ┌───────────────────────┼───────────────────────┐
                  │ 1:N (Single Filter)   │ 1:N (Single Filter)   │ 1:N (Single Filter)
                  ▼                       ▼                       ▼
      ┌───────────────────────┐ ┌───────────────────────┐ ┌───────────────────────┐
      │      Fact_Trips       │ │  Fact_Fuel_Purchases  │ │ Fact_Safety_Incidents │
      │  (85,000 Dispatches)  │ │  (Variable Fuel Logs) │ │ (170 Road Infractions)│
      └───────────▲───────────┘ └───────────────────────┘ └───────────────────────┘
                  │
                  ├──────────────────────────────┐ 1:N (Single Filter Direction)
                  │                              │
       ┌──────────┴──────────┐        ┌──────────┴──────────┐
       │     Dim_Drivers     │        │     Dim_Trucks      │
       │ (124 Active Workforce)       │  (92 Active Assets) │
       └─────────────────────┘        └─────────────────────┘
                  ▲
                  │ 1:N (Single Filter)
       ┌──────────┴──────────┐
       │    Dim_Customers    │
       │ (Enterprise Accounts)│
       └─────────────────────┘


                          RELATIONAL BLUEPRINT & FILTER LOGIC

1. Dim_Date: Centralizes temporal control across all fact records via 1:N relationships 
   linking to 'Trips[dispatch_date]', 'Fuel_Purchases[purchase_date]', and 
   'Safety_Incidents[incident_date]' to optimize time-intelligence calculations.
2. Dim_Drivers: Connects via 'driver_id' (1:N) to slice dispatch volumes, mileage metrics, 
   and safety compliance histories from a unified dimension.
3. Dim_Trucks: Connects via 'truck_id' / 'asset_id' (1:N) to track maintenance lifespans, 
   mechanical uptime metrics, and structural asset utilization anomalies.
4. Dim_Customers: Maps client account concentrations directly to fact performance matrices 
   to isolate service delivery (OTD) bottlenecks across key revenue categories.


     **Modeling Parameters:** All dimensional entities scale outward as Many-to-One single-direction relationships targeting the central transaction tables. A custom calendar engine was constructed to centralize all time intelligence calculations (MoM, YoY) on a uniform, performance-protected axis.

---

## 🔍 Core Structural Insight Areas

### Page 1: Executive Financial Overview
1. Which contract booking structures drive the highest macroscopic revenue capture between Dedicated, Spot, and Corporate contract segments?
2. How is client revenue concentration balanced across top enterprise accounts, and where are the primary high-value exposure lines?
3. What are the seasonal top-line growth trends and baseline operational spend trajectories over time?

### Page 2: Fleet Utilization & Maintenance Deep Dive
4. What is the financial distribution of variable maintenance liabilities when broken down by mechanical sub-systems (Inspection, Preventive, Tires, Brakes)?
5. Which specific outlier power units represent the highest upkeep costs and severe asset downtime bottlenecks?
6. How is active fleet asset capacity balanced across utilization statuses to maximize equipment longevity?

### Page 3: Supply Chain Logistics & Route Profitability
7. Which regional corridors and destination zones deliver the highest financial yields relative to route distance?
8. Where are network bottlenecks generating the most severe delivery detention hours?
9. What is the true volumetric split between on-time dispatches and delayed service execution across core client portfolios?

### Page 4: Fleet Efficiency & Performance Matrix
10. What is the total bottom-line financial leak resulting strictly from idle fuel waste across the asset network?
11. How do safety incident categories (DOT Violations, Moving Violations, Accidents) break down in composition, and what is their total claims exposure?
12. How does professional driver performance grade out chronologically when evaluated via a multi-metric scorecard?

---

---

## 📑 Executive Briefing: Key Insights
<table><tr><td bgcolor="#1F3A60"><b><font color="white" size="4">📊 CORE BUSINESS INTELLIGENCE DISCOVERIES</font></b></td></tr></table>

**💡 Key Analytical Findings**
**Finding 1 — Fuel Spend Concentration:** Variable fuel expense represents a massive operational draw on gross performance. Maximizing miles-per-gallon (MPG) metrics across the fleet remains the highest direct driver for expanding net margins.

**Finding 2 — Service Delivery Vulnerabilities:** The baseline On-Time Delivery rate sits below target benchmarks at 44.61%, creating an immediate commercial SLA risk. Network bottlenecks are highly concentrated around excessive terminal detention hours.

**Finding 3 — High-Yield Corridors:** Long-haul lanes heading through core destination corridors like Oregon, California, and Washington drive premium revenue volumes, though they require strict maintenance planning due to high mileage accumulation.

**Finding 4 — Revenue Segmentation:** Top-line revenue capture relies heavily on Dedicated Freight structures, which command 49.60% ($148.12M) of the booking allocation, compared to a balanced split between Corporate and Spot markets.

**Finding 5 — Maintenance Liability Outliers:** A small cluster of asset anomalies account for a disproportionate share of upkeep cost, led by high-cost vehicle repair peaks on specific power units like TRK00003 ($90K).

**Finding 6 — Bottom-Line Leaks:** Non-productive asset behavior represents a significant cash leak, with $2.33M spent purely on fleet-wide idle fuel waste.

**Finding 7 — Compliance Risk Exposure:** Corporate safety risk is heavily driven by DOT Violations (22.94%) and preventable accidents, representing a significant liability footprint across 170 recorded infractions.

**Finding 8 — Asset Failure Distribution:** Mechanical repair costs are heavily concentrated across specialized sub-components, identifying clear engineering categories where preventive cycles can reduce system downtime.

✅** Tactical Recommendations**
Deploy Fuel Optimization Systems: Target the $2.33M idle fuel leak by implementing strict automated engine-idle boundaries and optimizing regional refueling behaviors.

Establish High-Yield Lane Allocations: Expand freight capacity across identified high-yield long-haul corridors (Oregon, California) to secure optimal revenue-per-mile returns.

Launch OTD Remediation Protocols: Address the 44.61% on-time delivery crisis by restructuring dispatch schedules on high-detention routes and establishing structured penalties for terminal loading delays.

Implement Predictive Maintenance Windows: Address systemic fleet downtime by transitioning asset maintenance from reactive troubleshooting to proactive intervals, targeting known failure points.

Enforce Targeted Risk Interventions: Conduct focused safety workshops for the driver cohorts identified within the high-risk composite index to reduce liability exposure from DOT infractions.

**🛠️ Tools & Technologies Used**
**Microsoft Power BI Desktop:** Centralized data modeling, DAX architecture, and interactive dashboard design.

**Power Query (M Engine):** Data cleaning, parameter validation, schema transformation, and type enforcement.

**Microsoft Excel:** Advanced data validation, preliminary analysis, and data dictionary mapping.

**GitHub Markdown:** Technical documentation compilation and repository presentation.

**👤 About the Analyst**
Data Analyst Specializing in turning complex, decentralized operational data into clear, strategic business insights. Proficient in database relationships, advanced data modeling, and dynamic visualization architectures.

---

## 📐 Enterprise DAX Measures (Selected Architecture)

### Operational Financial Syntax
```dax
Gross Total Revenue = SUM('loads'[revenue])

Total Operational Expenses = 
    SUM('loads'[revenue_variables]) 
    + SUM('loads'[fuel_surcharge]) 
    + SUM('loads'[accessorial_charges])

Net Fleet Profit = [Gross Total Revenue] - [Total Operational Expenses]

Revenue Per Operational Mile = DIVIDE([Gross Total Revenue], SUM('trips'[actual_distance_miles]))

Efficiency & Spend Metrics
Total Fuel Cost = SUM('fuel_purchases'[total_cost])

Fuel As Pct Revenue = DIVIDE([Total Fuel Cost], [Gross Total Revenue])

Idle Fuel Waste Cost = SUM('trips'[idle_fuel_waste_dollars])

Average MPG Performance = AVERAGE('trips'[average_mpg])

Logistics & SLA Compliance
On-Time Delivery (OTD) Rate = 
    DIVIDE(
        CALCULATE(COUNTROWS('delivery_events'), 'delivery_events'[on_time_flag] = TRUE()),
        COUNTROWS('delivery_events')
    )

Total Network Detention Hours = SUM('delivery_events'[detention_hours])

Risk & Upkeep Formulations
Total Maintenance Costs = SUM('maintenance_records'[total_cost])

Total Safety Incident Claims = SUM('safety_incidents'[claim_amount])

Driver Risk Score Matrix = 
    VAR IncidentWeight = 0.35 
    VAR PreventableWeight = 0.30 
    VAR OTDWeight = 0.20 
    VAR IdleWeight = 0.15 
    RETURN 
        ([Driver Incident Score] * IncidentWeight) + 
        ([Driver Preventable Score] * PreventableWeight) + 
        ([Driver OTD Risk Score] * OTDWeight) + 
        ([Driver Idle Score] * IdleWeight)

