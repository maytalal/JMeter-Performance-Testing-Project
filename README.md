# 🚀 Flight Booking API Performance & Architecture Testing Suite

This repository contains a production-grade, end-to-end Performance Testing Framework built using **Apache JMeter** to evaluate the stability, responsiveness, and behavioral bounds of a distributed flight booking system workflow (BlazeDemo). 

The entire test execution, data extraction, and logging were structured via **Non-GUI (Command Line) Mode** to enforce maximum hardware resource conservation on the Load Generator and guarantee architectural baseline accuracy.

---

## 📊 Executive Summary & Key Benchmarks

Following rigorous execution of the JMX test harness, the transactional results dump (`results.csv`) was statically evaluated. The system profile indicates solid transactional resiliency alongside critical resource constraints under concurrent loads.

### 📈 Core Architecture Metrics
* **Total Executed Samples:** `2,177` Requests 
* **Global Error Rate:** `0.05%` *(Extremely High Success Rate of **99.95%**)* 🎉
* **Overall Average Response Time:** `~491 ms`
* **90th Percentile Line (Global SLA):** `484 ms` *(90% of all user interactions experienced response latencies below this strict threshold)*
* **Test Duration Profile:** `5 Minutes` continuous execution window.

---

## 🔍 Detailed Component Performance Breakdown

The transactional workflow is broken down across three sequential API endpoints under concurrent virtual user pools:

| API Endpoint / Transaction | Total Hits | Avg Response Time | Min / Max Response Time | Success Rate |
| :--- | :---: | :---: | :---: | :---: |
| 🛩️ **Reserve Request** | 735 | 868.2 ms | 368 ms / **42.5 sec** ⚠️ | 99.86% |
| 💳 **Purchase Request** | 733 | 310.9 ms | 244 ms / 2.2 sec | 100.00% |
| ✅ **Confirmation Request** | 709 | 287.4 ms | 241 ms / 491 ms | 100.00% |

### 💡 Critical QA Architecture Insight (Bottleneck Detection)
> [!WARNING]
> While the **Purchase** and **Confirmation** requests maintained rapid, sub-second execution profiles, the **Reserve Request** suffered an extreme response spike reaching **42.5 seconds** under maximum stress conditions. 
> 
> **Root Cause Hypothesis:** This indicates severe locking constraints during database lookups or compute-heavy filtering logic during peak concurrency. Remediation requires implementing **Database Indexing** on lookup keys or adding an application-level caching layer to prevent down-stream performance degradation.

---

## 📂 Repository Structure

The workspace is organized cleanly to provide instant visibility into script design and analytical artifacts:

```text
├── Booking Website.jmx    # Main JMeter XML Test Plan (Thread Groups, Samplers, Configuration Elements)
├── results.csv            # Raw transactional performance metrics dump (Timestamps, Latency, Codes)
└── Dashboard_Report/      # Automatically compiled Web UI Dashboard (Flot Charts, Apdex Index, TPS Charts)

🛠️ CLI Execution & Automation Engine
To eliminate the heavy graphical processing unit overhead of the JMeter GUI (which impacts script timing values), the test run is executed exclusively using the following native command:

Bash
jmeter -n -t "Booking Website.jmx" -l results.csv -e -o Dashboard_Report
Command Flags Architecture:
-n : Enforces Non-GUI Mode operation.

-t : Sets the explicit path to the target JMeter Test Plan (.jmx).

-l : Directs raw transaction tracking into the target log file (.csv / .jtl).

-e -o : Initiates post-test compilation to automatically generate the visual HTML dashboard inside the specified output folder.

🧠 Methodologies applied & Core Engineering Competencies
By architecting and completing this performance verification cycle, I have practically validated and mastered the following Software Engineering & QA principles:

Advanced Load Profiles Strategy: Configured deterministic Thread Groups utilizing proper Ramp-up and steady-state holding durations to safely establish system boundaries without provoking artificial system crashes.

Key Performance Indicators (KPIs) Analysis: Extracted and mapped crucial transactional metrics including Throughput (Transactions Per Second - TPS), Network Latency, and HTTP Status Code stability tracking.

Data-Driven Performance Profiling: Converted flat transactional logs (.csv) into structured charts to explicitly differentiate between application layer responsiveness and network-induced lag.

Shift-Left Methodology Alignment: Integrated functional test criteria (Assertions) directly into performance test flows, matching core software testing standards where structural failures are detected simultaneously with performance exhaustion.
