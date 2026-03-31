# soc-log-analysis-sql-threat-detection
Security log investigation using SQL to detect suspicious login attempts, analyze access patterns, and identify systems requiring security updates.


# SOC Log Analysis Using SQL for Threat Detection

## Overview

This project demonstrates how SQL can be used by security analysts to investigate suspicious activity, analyze authentication logs, and identify systems that require security updates.

Using structured queries and filtering techniques, login attempts and employee system data were analyzed to detect potential security threats and support incident investigation.

The project simulates tasks commonly performed by Security Operations Center (SOC) analysts when investigating authentication logs and identifying abnormal system activity.

---

## Objectives

The primary goals of this project were to:

- Investigate suspicious login attempts
- Detect activity occurring outside normal business hours
- Identify login attempts from unexpected locations
- Retrieve employee systems requiring security updates
- Demonstrate how SQL queries can support security investigations

---

## Dataset Overview

Two tables were analyzed in this investigation:

### log_in_attempts

This dataset contains authentication records including:

- login time
- login date
- success or failure of login attempts
- geographic location of the login

### employees

This dataset contains employee information used to determine which systems require updates, including:

- department
- office location
- employee machine assignments

---

# Security Investigation Queries

## Detect After-Hours Failed Login Attempts

Potential security incidents often occur outside business hours. Failed login attempts occurring after **18:00** were investigated.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
AND success = FALSE;

This query identifies failed login attempts that occurred after normal working hours, which may indicate:

unauthorized access attempts
brute force login attempts
suspicious account activity
Investigate Login Attempts on Specific Dates


A suspicious event occurred on 2022-05-09, requiring investigation of login activity from that day and the day prior.
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
OR login_date = '2022-05-08';

Purpose
This query isolates authentication activity around the suspected incident timeframe.


Detect Logins Outside Expected Geographic Location
Login attempts from outside Mexico were identified as suspicious and required further investigation.

SQL Query
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';

Purpose
This query filters authentication attempts from countries other than Mexico, helping identify:
unauthorized remote access
compromised credentials
abnormal login behavior
Identify Employee Machines Requiring Security Updates

Security updates needed to be applied to employee systems in specific departments and locations.

Employees in Marketing Department (East Building)
SELECT *
FROM employees
WHERE department = 'Marketing'
AND office LIKE 'East%';

This query retrieves employees in the Marketing department located in the East building.
Security Insights

Using SQL filters allowed for efficient identification of:
suspicious login behavior
abnormal login times
unexpected geographic login locations
systems requiring targeted security updates

These types of queries are commonly used in:
Security Operations Centers (SOC)
Threat detection investigations
Identity and access monitoring
security log analysis
Skills Demonstrated
SQL Query Development
Security Log Analysis
Threat Detection
Authentication Monitoring
Data Filtering and Pattern Matching
Cybersecurity Investigation Support
