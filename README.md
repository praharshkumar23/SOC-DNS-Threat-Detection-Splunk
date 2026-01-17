
<h1 align="center">📊 DNS Log Analysis Using Splunk (Zeek Logs)</h1>

<p align="center">
  Hands-on SOC lab for ingesting, analyzing, and detecting DNS-based threats using Splunk Enterprise
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SIEM-Splunk-success" />
  <img src="https://img.shields.io/badge/Logs-Zeek-blue" />
  <img src="https://img.shields.io/badge/Language-SPL-orange" />
</p>

---

## 📌 Project Overview

This project demonstrates how to **ingest, parse, and analyze DNS logs** using **Splunk Enterprise** in a SOC-style lab environment.  
Using **Zeek-style JSON DNS logs**, the project focuses on **DNS traffic visibility, behavioral analysis, and threat detection** using **Splunk Search Processing Language (SPL)**.

The lab helps simulate how SOC analysts investigate DNS telemetry to identify:

- Frequently queried domains
- High-volume DNS-generating hosts
- DNS query type distribution
- Abnormal or suspicious DNS behavior

---

## 🎯 Learning Objectives

By completing this project, you will gain hands-on experience with:

- Ingesting JSON-based DNS logs into Splunk
- Extracting and analyzing DNS metadata (domains, IPs, record types)
- Writing SPL queries for DNS traffic investigation
- Identifying suspicious DNS patterns and anomalies
- Building a strong foundation for DNS-based threat detection in SOC environments

---

## 🛠️ Tools & Technologies

- **Splunk Enterprise**
- **Zeek DNS Logs (JSON format)**
- **Splunk Search Processing Language (SPL)**

---

## 📂 Dataset Details

The dataset consists of **Zeek-style DNS logs** in JSON format with the following fields:

```

ts          → Event timestamp
id.orig_h  → Source (client) IP address
id.resp_h  → DNS server IP address
qtype      → DNS query type (A, AAAA, PTR, CNAME)
query      → Queried domain name
answers    → DNS response values
rcode      → DNS response code
rtt        → Round Trip Time

```

---

## ⚙️ Lab Setup & Data Ingestion

### Step 1: Upload DNS Logs

1. Open **Splunk Web**
2. Navigate to:
```

Settings → Add Data → Upload

```
3. Select the file:
```

dns_logs.json

````
4. Configure ingestion:
- **Source Type:** `json` (or custom `zeek:dns`)
- **Index:** Create a new index such as `dns_lab` (recommended)

---

### Step 2: Verify Data Ingestion

Confirm that logs are indexed successfully:

```spl
index=dns_lab | head 5
````

---

## 🔍 Analysis Tasks & SPL Queries

### 🔹 Task 1: Most Frequently Queried Domain Names

Identify domains queried most often in the environment.

```spl
index=dns_lab
| stats count by query
| sort -count
```

**SOC Use Case:**
Detect suspicious domains, malware beaconing, or potential C2 communication.

---

### 🔹 Task 2: Most Active Client IP Addresses

Identify hosts generating unusually high DNS traffic.

```spl
index=dns_lab
| stats count by id.orig_h
| sort -count
```

**SOC Use Case:**
Identify compromised endpoints or misconfigured systems.

---

### 🔹 Task 3: DNS Query Type Distribution

Analyze DNS record types to understand traffic patterns.

```spl
index=dns_lab
| stats count by qtype
```

**Common DNS Types:**

* `A` → IPv4 resolution
* `AAAA` → IPv6 resolution
* `CNAME` → Domain alias mapping
* `PTR` → Reverse DNS lookup

---

## 📈 Key Findings

* Identified **top queried domains** (e.g., Google, Microsoft, Yahoo)
* Detected **high-volume DNS-generating client IPs**
* Observed distribution of **A, AAAA, CNAME, and PTR records**
* Analyzed **DNS response times (RTT)** and failed lookups
* Established a **baseline for normal DNS behavior**

---

## 🚨 Security Insights

This DNS analysis can assist SOC teams in detecting:

* DNS tunneling activity
* Malware beaconing through repeated DNS queries
* Excessive reverse DNS lookups
* High-latency or failed DNS responses
* Rare or newly observed domain activity

---

## 📊 Dashboards & Alerts (Future Enhancements)

Planned improvements include:

* Interactive Splunk dashboards for DNS visibility
* Automated alerts for:

  * High DNS query volume
  * NXDOMAIN spikes
  * Rare or suspicious domains

---

## ✅ Conclusion

Through this project, I:

* Successfully ingested and analyzed DNS logs using Splunk
* Built SPL queries for DNS-focused investigations
* Identified security-relevant DNS patterns
* Gained practical SOC experience in SIEM-based log analysis

This project is well-suited for **SOC Analyst, SIEM Engineer, and Blue Team roles**.

---

## 🚀 Future Enhancements

* GeoIP enrichment for DNS responses
* DNS tunneling detection using entropy analysis
* Correlation with HTTP or proxy logs
* Automated alerting and reporting

---

⭐ *If you found this project useful, consider starring the repository!*

```

---

### ✅ Why this version is better
- SOC + interview language
- Clean structure (easy for recruiters)
- Clear use cases (not just queries)
- No unnecessary fluff
- Looks **senior for a fresher**

If you want next:
- 📌 LinkedIn post for this project  
- 📌 Resume project bullet points  
- 📌 SOC interview explanation (DNS-focused)  

Tell me 👍
```
