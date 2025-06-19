# CST8919 Lab 2: Web App Threat Detection with Azure Monitor & KQL
## Name :- Vaibhav Mishra
## Student ID :- 041165850
## 👨‍💻 Project Title
**Flask Login Monitor** — Detecting Brute-Force Login Attempts using Azure Monitor, Kusto Query Language (KQL), and Automated Alerting

---

## 🎯 Objective

In this lab, we:
- Developed a Python Flask app with login tracking
- Deployed it to **Azure App Service**
- Enabled **diagnostic logging** and sent logs to **Log Analytics Workspace**
- Queried failed login attempts using **Kusto Query Language (KQL)**
- Created an **email alert rule** to detect brute-force login behavior

---

## 🔧 Scenario

As a cloud security engineer, your goal is to secure a web app by detecting failed login attempts. You must:
- Capture both successful and failed logins
- Forward logs to Azure Monitor
- Detect brute-force behavior
- Trigger an automated alert when 5+ failed logins occur in 5 minutes

---

## ✅ Tasks Completed

### Part 1: Deploy the Flask App to Azure
- Created a Flask app with a `/login` route
- Configured logging using `app.logger.warning()` and `info()`
- Deployed the app to **Azure Web App (Linux, Python 3.11)**

### Part 2: Enable Monitoring
- Created a **Log Analytics Workspace**
- Enabled:
  - `AppServiceConsoleLogs`
  - `AppServiceHTTPLogs` (optional)
- Connected Web App diagnostic logs to the workspace

### Part 3: Generate and Query Logs
- Used a `.http` file with REST Client in VS Code to send:
  - Valid login attempts
  - Invalid (failed) login attempts
- Queried logs in Log Analytics using KQL

### Part 4: Create Alert Rule
- Used KQL query as condition
- Set threshold: > 5 failed logins in 5 minutes
- Configured evaluation frequency: every 1 minute
- Created **Action Group** with email alert
- Tested and confirmed that alerts are triggered and email received

---

### Video Link
https://drive.google.com/file/d/1Z4Rkckkx2b--KR44CrN6XghGrTs7rsD4/view?usp=sharing

## 🔎 KQL Query with Explanation

```kusto
AppTraces
| where TimeGenerated > ago(5m)
| where Message has "Login failed"


