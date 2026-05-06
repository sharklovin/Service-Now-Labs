# Ticket Notes - Lab 08

> **Lab:** Lab 08 - Run a Report and Export Evidence for a Weekly SLA Review
>
> **Module:** ServiceNow Reports
>
> **Completed:** May 2026

---

## Report 1 - Weekly Incident Volume by Priority

### Report Source Configuration

| Field | Value | Notes |
|---|---|---|
| **Name** | Weekly Incident Summary (initial) - renamed to Weekly Incident Volume by Priority | Name changed after bar chart configuration to reflect the specific report content |
| **Table** | Incident [incident] | The primary incident table. Contains all incident records with their full field set. |
| **Description** | Summary of this week's incident performance | Human-readable description visible to other report consumers in the instance |
| **Application** | Global | Global scope means the report is available to all users with report access, not scoped to a specific application |

### Report Builder - Configure Step

| Setting | Value | Notes |
|---|---|---|
| **Columns** | Number, Short Description, Priority, State, Opened, Resolved, Assignment Group | Seven columns covering identity, classification, lifecycle, and routing fields |
| **Group by** | Priority (bar chart version) / None (list version) | Group by Priority generates one bar per priority level in the bar chart |
| **Report type (v1)** | List | Used for initial data verification - confirms the filter and columns are correct before switching to chart |
| **Report type (v2)** | Bars | Used for the final saved version - visualises priority distribution as a bar chart |

### Filter Condition

| Field | Operator | Value | Notes |
|---|---|---|---|
| **Opened** | at or after | This week | Dynamic date filter - recalculates automatically on each report run |

**Why "at or after" and not "after":**
"at or after" includes incidents opened on exactly the start of the current week (Monday 00:00:00). "after" would exclude that exact moment. For a weekly summary, including the full first day is correct.

**Why "This week" and not a hardcoded date:**
"This week" is a dynamic relative date value. Running this report next Friday will return next week's incidents with no changes to the filter. A hardcoded date requires manual updating each week and is a maintenance burden on whoever owns the report.

### Results Summary

| Metric | Value |
|---|---|
| **Total incidents returned** | 72 |
| **Records per page** | 20 (pagination: 1 to 20 of 72) |
| **Highest visible priority** | Priority 1 - Critical (multiple rows visible in the list) |
| **States observed** | Closed, On Hold, In Progress |
| **Bar chart - tallest bar** | Approximately 43 incidents (highest priority category) |
| **Bar chart - second bar** | Approximately 28 incidents (second priority category) |

---

## Report 2 - SLA Breached Incidents

### Report Source Configuration

| Field | Value | Notes |
|---|---|---|
| **Name** | SLA Breached Incident | Identifies this as a compliance/breach report, distinct from the volume report |
| **Table** | Task SLA [task_sla] | The SLA tracking table - separate from the Incident table. Contains one row per SLA agreement per task. |
| **Description** | (not completed) | Should contain: "All Task SLA records where Has breached is true - used for weekly SLA compliance review" |
| **Application** | Global | Available to all report consumers |

### Filter Condition

| Field | Operator | Value | Notes |
|---|---|---|---|
| **Has breached** | is | true | Boolean filter - returns only records where the SLA deadline passed without resolution |

### Task SLA Table - Key Fields

| Column | Description | Use in this report |
|---|---|---|
| **Task** | Linked incident or change number | Identifies which incident violated the SLA |
| **SLA definition** | The name of the SLA agreement | Identifies which specific SLA was breached (Priority 1 SLA, OLA, UC) |
| **SLA definition Type** | SLA, OLA, or Underpinning Contract | Determines which contractual tier was violated |
| **SLA definition Target** | Resolution, Response, or other target | Shows what the SLA was measuring |
| **Stage** | In Progress, Achieved, Breached, Completed, Cancelled | The current state of the SLA assessment |
| **Business time left** | Time remaining before/after breach | 0 Seconds = deadline passed |
| **Business elapsed time** | Total business time consumed | How long the task actually took |
| **Business elapsed percentage** | Elapsed time as % of target | 100% = met exactly, over 100% = breached, 704% = severely breached |
| **Start time** | When the SLA clock started | Usually when the incident was opened or priority was set |
| **Stop time** | When the SLA clock stopped | When the incident was resolved, cancelled, or the SLA was met |

### Notable Records in the SLA Breach Report

**INC0000060 - Multiple SLA violations**

This single incident appears multiple times in the breach report, demonstrating that a single incident can violate multiple SLA agreements simultaneously.

| Row | SLA definition | Type | Stage | Elapsed % | Notes |
|---|---|---|---|---|---|
| 1 | Priority 3 resolution (1 day) | SLA | Achieved | 37.5% | Met - 15 hours elapsed of a 1-day target |
| 2 | SAN 001 contract resolution (3.5 hour) | Underpinning contract | Breached | 704.1% | 1 day 38 minutes elapsed against 3.5-hour target |
| 3 | Network group resolution | OLA | Breached | 482.07% | 19 hours 16 minutes elapsed |

**INC0008111 - Extreme elapsed time**

| SLA definition | Type | Stage | Elapsed time | Elapsed % | Notes |
|---|---|---|---|---|---|
| Priority 3 resolution (1 day) | SLA | Completed | 661 Days 14 Hours 54 Minutes | 66,162.13% | Extreme outlier - over 661 days to resolve a 1-day SLA |

The 66,162% elapsed time on INC0008111 is a data quality flag. A Priority 3 incident taking 661 days to resolve is either a data entry error (the incident was never properly closed in ServiceNow while the underlying issue was resolved elsewhere) or a genuine operations failure. Either way, this record should be reviewed and the incident closed with appropriate notes before the next service review.

### Results Summary

| Metric | Value |
|---|---|
| **Total Task SLA records returned** | 24 |
| **Export run date** | 2026-05-06 02:42:14 Pacific Daylight Time |
| **Export run by** | System Administrator |
| **Group by (in exported PDF)** | Active |
| **Sort order** | Active in ascending order |
| **Most severe breach** | INC0008111 at 66,162.13% elapsed |
| **Second most severe** | INC0000060 SAN 001 contract at 704.1% elapsed |

---

## PDF Export Metadata - Full Reference

The PDF export header block contains the following fields, all of which appear on every ServiceNow report export:

| Metadata field | Value in this export | Purpose |
|---|---|---|
| **Report Title** | SLA Breached Incidents | Identifies the report by name |
| **Run Date and Time** | 2026-05-06 02:42:14 Pacific Daylight Time | Timestamp of when the export was generated - critical for audit |
| **Run by** | System Administrator | Username of the person who generated the export |
| **Table name** | task_sla | The source table - confirms the data origin |
| **Group by** | Active | The grouping applied in the exported version |
| **Sort Order** | Active in ascending order | The sort applied - determines the row sequence |
| **Record count** | 24 Task SLAs | Total number of records in the export |

The Run Date and Time and Run by fields together constitute the chain of custody for the exported data. They prove who pulled the data and when, which is required for any report used as evidence in a service review, compliance audit, or contractual dispute.

---

## Analyst Summary - Full Text

> **Weekly Incident Performance - Week ending 9 May 2026**
>
> A total of 72 incidents were recorded in the ServiceNow instance for the current review period, with the majority falling into the Priority 1 - Critical category, indicating a higher-than-expected volume of high-urgency work reaching the service desk this week. The SLA breach report, run against the Task SLA table with the filter Has breached is true, returned 24 SLA records, confirming that multiple resolution and response targets were not met during the period, with individual elapsed percentages reaching as high as 704% over the contracted target. The Priority 1 volume and the SLA breach count together suggest that the service desk is operating above sustainable capacity for critical incidents, and that triage and escalation routing should be reviewed before the next working week begins. It is recommended that the team lead reviews the 24 breached SLA records individually to identify whether the breaches are concentrated in a specific assignment group, CI type, or category - this will determine whether the issue is a workload problem, a skills gap, or a routing misconfiguration. As an immediate action, any incidents currently in an On Hold or In Progress state with a Priority 1 classification should be reviewed for SLA proximity and re-prioritised before close of business today.

### Summary Breakdown - What Each Sentence Covers

| Sentence | ITIL topic covered | Data source |
|---|---|---|
| 1 - "A total of 72 incidents..." | Total volume and priority distribution | Weekly Incident Volume by Priority report (Incident table) |
| 2 - "The SLA breach report..." | SLA compliance and breach count | SLA Breached Incidents report (Task SLA table) |
| 3 - "The Priority 1 volume and breach count..." | Trend observation and capacity signal | Synthesis of both reports |
| 4 - "It is recommended..." | Recommended investigative action | Standard SLA breach investigation process |
| 5 - "As an immediate action..." | Immediate operational action | Prioritisation and SLA proximity review |

---

## Report Type Decision Guide

When building a report for a service review, the choice of report type determines how the audience receives the information. The wrong type obscures rather than communicates.

```
USE A LIST WHEN
  - The audience needs to see individual records
  - The purpose is to identify specific incidents for follow-up
  - Drill-down into detail is required
  - The report will be exported and reviewed record by record
  Examples: SLA breach list, open P1 incidents, unassigned queue

USE A BAR CHART WHEN
  - The audience needs to compare volumes across categories
  - The purpose is to show distribution (priority, state, assignment group)
  - The report will be shown on a screen in a meeting
  - A single visual should communicate the key message in seconds
  Examples: Incidents by priority, incidents by state, volume by team

USE A PIE CHART WHEN
  - The audience needs to see proportions of a whole
  - The total is less important than the share
  - There are 5 or fewer categories (more than 5 makes pie charts unreadable)
  Examples: Category distribution, source of incidents, resolution method

USE A LINE CHART WHEN
  - The audience needs to see how a metric changes over time
  - Trend identification is the goal (increasing, decreasing, stable)
  - Week-over-week or month-over-month comparison is needed
  Examples: Weekly incident volume trend, average resolution time over 12 months

USE A SINGLE SCORE WHEN
  - One number needs to be prominently displayed on a dashboard
  - The metric is a KPI with a clear threshold (target vs actual)
  Examples: Open P1 count, SLA compliance percentage, CSAT score
```

---

## Key Observations on ServiceNow Reporting Behaviour

**1. The "This week" filter value uses the ServiceNow instance time zone, not the user's time zone.**
If the instance is configured to US Pacific time and the user is in Nigeria (WAT), "This week" starts on Monday 00:00 Pacific, which is Monday 08:00 WAT. Incidents logged before 08:00 WAT on Monday would not appear in the report for users in West Africa. This is a known edge case in multi-timezone reporting that is resolved by using explicit date ranges when timezone precision matters.

**2. Group by fields must have discrete, finite values to produce readable charts.**
Group by Priority works because there are four priority levels (1, 2, 3, 4) - one bar each. Group by Opened (a datetime field) would produce one bar per unique timestamp, which is unreadable. Group by fields should always be categorical (Priority, State, Category, Assignment group) rather than continuous (dates, elapsed time, numbers).

**3. The report builder's AI question feature is supplementary, not a replacement for manual configuration.**
The "What do you want to see?" natural language input can produce fast starting points for common queries, but it does not guarantee the correct table, filter, or grouping. Manual verification of the data source and filter conditions is always required before a report is used in a formal context.

**4. Saved reports are visible to other users with report access.**
A report saved with Global application scope is visible in the All Reports list to anyone with the report_reader or itil role. Sensitive reports (headcount data, salary information, performance reviews) should be scoped to a restricted group or application. Standard service desk metrics (incident volume, SLA compliance) are generally appropriate to share at Global scope.

**5. Exporting to PDF captures the report at the moment of export.**
The PDF is a static snapshot. If five more incidents are logged after the export, they will not appear in the PDF. The Run Date and Time metadata field documents exactly when the snapshot was taken, which is why it matters for evidence purposes. For a service review, always export immediately before the meeting to ensure the data is as current as possible.

**6. The Task SLA table is populated automatically by ServiceNow SLA workflows.**
SLA records are created automatically when incidents are opened, updated, or prioritised, based on the SLA definitions configured in the instance. Analysts do not manually create Task SLA records - they are a product of the SLA engine running in the background. When a breach report returns unexpected results (records that should not be there, or missing records that should be there), the issue is usually in the SLA definition configuration, not in the report filter.
