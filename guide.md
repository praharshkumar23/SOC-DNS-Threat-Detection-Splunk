<h1 align="center">📊 DNS Log Analysis Using Splunk (Zeek Logs)</h1>

<p align="center">
  Ingesting, analyzing, and visualizing DNS logs using Splunk & Zeek
</p>



## 📌 Project Overview
This project demonstrates how to **ingest, parse, and analyze DNS logs** using **Splunk Enterprise**.  
Using **Zeek-style JSON DNS logs**, we perform security-focused DNS traffic analysis with **Splunk Search Processing Language (SPL)**.


---

## 🛠️ Tools & Technologies
- **Splunk Enterprise**
- **Zeek DNS Logs (JSON format)**
- **Search Processing Language (SPL)**

---

## 📂 Dataset Information
The dataset consists of **Zeek-style DNS logs** in JSON format containing the following fields:

```

ts          → Timestamp
id.orig_h  → Source IP address
id.resp_h  → DNS server IP
qtype      → DNS query type (A, AAAA, PTR, CNAME)
query      → Queried domain name
answers    → DNS response
rcode      → DNS response code
rtt        → Round Trip Time

```

---

## ⚙️ Lab Setup & Data Ingestion

### Step 1: Upload DNS Logs
1. Open **Splunk Web**
<img width="1919" height="960" alt="1" src="https://github.com/user-attachments/assets/50979df3-c854-4efa-ab16-a7ad6ebc7ba5" />

2. Navigate to:
```

Settings → Add Data → Upload

```
<img width="1919" height="961" alt="2" src="https://github.com/user-attachments/assets/8ccd82ff-a637-4ac2-847f-5434b25f0727" />
<img width="1919" height="962" alt="3" src="https://github.com/user-attachments/assets/09002c91-38e6-476c-9a44-706d704a7257" />
<img width="1919" height="963" alt="4" src="https://github.com/user-attachments/assets/fead3b3e-72b8-4505-99f2-6f35f70f2eca" />

3. Select the file:
```

dns_logs.json

````
<img width="1919" height="1079" alt="5" src="https://github.com/user-attachments/assets/8a95c35b-a154-48a6-b7df-27aacf63ead4" />
<img width="1919" height="962" alt="6" src="https://github.com/user-attachments/assets/a574fc37-66a5-461a-879c-192bd7507784" />

4. Configure:
- **Source Type:** `json` (or custom `zeek:dns`)
- **Index:** create a new index like `dns_lab` (recommended)
<img width="1919" height="964" alt="7" src="https://github.com/user-attachments/assets/fba778f8-375d-444e-8fda-24ac3e3e1efc" />
<img width="1919" height="963" alt="8" src="https://github.com/user-attachments/assets/32ba2774-2c6d-45a1-ae16-3046ae2f1a29" />
<img width="1919" height="964" alt="9" src="https://github.com/user-attachments/assets/a252a32f-eb50-4f8e-83e3-e6599d0ecc8c" />
<img width="1919" height="963" alt="10" src="https://github.com/user-attachments/assets/2c144ca4-76f8-4170-954a-56169217c6a6" />
<img width="1919" height="960" alt="11" src="https://github.com/user-attachments/assets/fc95559c-cbb6-460f-806f-203c3a6bc985" />
<img width="1919" height="962" alt="12" src="https://github.com/user-attachments/assets/e6b1a3b8-e017-4f69-ab5c-916a838c5351" />
<img width="1919" height="960" alt="13" src="https://github.com/user-attachments/assets/08a47656-2af0-4ae2-991e-d9c1ca74f8d1" />
<img width="1919" height="961" alt="14" src="https://github.com/user-attachments/assets/e18bc077-1507-40e0-99f1-cb3ecb89191a" />

---

### Step 2: Verify Data Ingestion
Run the following SPL query:

```spl
index=dns_lab | head 5
````
<img width="1919" height="963" alt="15" src="https://github.com/user-attachments/assets/73f70cab-a061-41d2-af7b-e853f869c796" />

---

## 🔍 Lab Tasks & SPL Queries

### 🔹 Task 1: Most Frequently Queried Domain Names

Identify the domains queried most often.

```spl
index=dns_lab 
| stats count by query
| sort -count
```

**Use Case:** Detect suspicious domains, beaconing behavior, or malware C2 traffic.
<img width="1919" height="961" alt="16" src="https://github.com/user-attachments/assets/aecf91a9-6306-4f76-8388-dcf4ab6c0f80" />

---

### 🔹 Task 2: Most Active Client IPs

Find hosts generating the highest DNS traffic.

```spl
index=dns_lab 
| stats count by "id.orig_h"
| sort -count
```

**Use Case:** Identify compromised systems or misconfigured devices.
<img width="1919" height="962" alt="17" src="https://github.com/user-attachments/assets/0bf5abb4-8861-4739-ad38-0d2e4a494e7e" />

---

### 🔹 Task 3: DNS Query Type Breakdown

Analyze DNS record types in the environment.

```spl
index=dns_lab 
| stats count by qtype
```

**Common Types:**

* `A` → IPv4 address lookup
* `AAAA` → IPv6 address lookup
* `CNAME` → Canonical name mapping
* `PTR` → Reverse DNS lookup
<img width="1919" height="962" alt="18" src="https://github.com/user-attachments/assets/e7bc8072-3d64-42c2-bcca-abecf9d9c98c" />

---

## 📈 Key Findings

* Identified **top queried domains** (e.g., Google, Microsoft, Yahoo)
* Discovered **high-volume DNS-generating client IPs**
* Observed distribution of **A, AAAA, CNAME, and PTR records**
* Analyzed **response time (RTT)** and failed DNS resolutions
* Established a baseline for DNS behavior

---

## 🚨 Security Insights

This analysis can help detect:

* DNS tunneling
* Malware beaconing via repeated DNS queries
* Excessive reverse DNS lookups
* High-latency or failed DNS responses
* Rare or suspicious domain queries

---

## 📊 Dashboards & Alerts (Enhancements)

Future improvements may include:

* Splunk dashboards for DNS activity visualization
* Alerts for:

  * High DNS query volume
  * NXDOMAIN spikes
  * Rare or newly observed domains

---

## ✅ Conclusion

By completing this project, you have:

* Successfully ingested and parsed DNS logs in Splunk
* Built SPL queries for DNS traffic analysis
* Identified key DNS usage patterns
* Gained hands-on experience in SIEM-based security analysis

This project is well-suited for **SOC Analyst, Cybersecurity, and SIEM roles**.

---

## 🚀 Future Enhancements

* GeoIP enrichment for DNS responses
* DNS tunneling detection using entropy analysis
* Correlation with HTTP or proxy logs
* Automated alerting and reporting

---

⭐ **If you found this project helpful, consider starring the repository!**

```


