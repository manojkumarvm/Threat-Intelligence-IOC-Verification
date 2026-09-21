# Threat Intelligence Lookup & IOC Verification

## 📌 Project Overview

This project demonstrates a practical **Threat Intelligence and Indicator of Compromise (IOC) verification workflow**.

The project collects suspicious **IP addresses, domains, and file hashes**, verifies their reputation using public threat-intelligence platforms, maps relevant findings to **MITRE ATT&CK**, and documents the results in a structured IOC log.

The investigation workflow is:

**IOC Collection → Threat Intelligence Verification → MITRE ATT&CK Mapping → Classification → IOC Documentation**

---

## 🎯 Objectives

* Collect suspicious IP addresses, domains, and file hashes from public threat-intelligence sources.
* Verify IOC reputation using **VirusTotal** and **URLScan.io**.
* Identify malware or threat-family associations.
* Map relevant findings to **MITRE ATT&CK techniques**.
* Maintain a structured IOC log for investigation and reference.

---

## 🛠️ Tools & Technologies

| Tool                          | Purpose                                     |
| ----------------------------- | ------------------------------------------- |
| VirusTotal                    | IOC reputation and security-vendor analysis |
| URLScan.io                    | Website and URL analysis                    |
| ThreatFox                     | Threat intelligence and IOC collection      |
| MITRE ATT&CK                  | Adversary technique mapping                 |
| Microsoft Excel / Spreadsheet | IOC documentation                           |

---

## 🔎 Investigation Methodology

### 1. IOC Collection

Indicators were collected from public threat-intelligence sources.

The investigation covered three IOC types:

* IP address
* Domain
* SHA-256 file hash

### 2. VirusTotal Verification

Each IOC was searched in VirusTotal to review:

* Security-vendor detections
* Reputation
* Network information
* File information
* Historical submissions
* Threat classifications

### 3. URLScan.io Verification

Web-based IOCs were checked using URLScan.io to identify:

* Scan status
* HTTP response
* Final URL
* Page information
* Network-related information

A failed URLScan scan was recorded as **"Could not scan"** rather than being treated as evidence that the IOC was clean.

### 4. MITRE ATT&CK Mapping

Relevant threat behavior was mapped to MITRE ATT&CK techniques where documented evidence supported the mapping.

### 5. IOC Classification

The collected evidence was used to classify each IOC as:

* Malicious
* Security Test / Benign
* Other / Unknown where appropriate

---

# 📊 IOC Investigation Results

| IOC                                                                | Type    | Source             | Malware / Family | VirusTotal | URLScan            | Classification         |
| ------------------------------------------------------------------ | ------- | ------------------ | ---------------- | ---------- | ------------------ | ---------------------- |
| `124.223.177.82:22`                                                | IP:Port | ThreatFox          | Cobalt Strike    | 5/89       | ERR_EMPTY_RESPONSE | Malicious              |
| `h67as5d5x.m6p3wca1.cc`                                            | Domain  | ThreatFox          | Cobalt Strike    | 15/91      | Could not scan     | Malicious              |
| `275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f` | SHA-256 | VirusTotal / EICAR | EICAR Test File  | 66/68      | N/A                | Security Test / Benign |

---

# 🖥️ IOC #1 — IP Investigation

## Indicator

```text
124.223.177.82:22
```

### Threat Intelligence

* IOC Type: IP:Port
* Threat Type: Botnet C2
* Malware/Family: Cobalt Strike
* ThreatFox Confidence: 100%
* Compromised Status: True
* Port: 22

### VirusTotal

* Detection: **5/89**
* Network: `124.220.0.0/14`
* ASN: `45090`
* Country: China
* Network Name: TencentCloud

### URLScan.io

The HTTP scan returned:

```text
ERR_EMPTY_RESPONSE
```

The website could not be successfully scanned.

### MITRE ATT&CK

```text
T1021.004 — Remote Services: SSH
```

The Cobalt Strike software page documents SSH capability under this technique.

### Classification

**Malicious**

The classification was based on the combined threat-intelligence association, confidence information, and VirusTotal detections.

---

# 🌐 IOC #2 — Domain Investigation

## Indicator

```text
h67as5d5x.m6p3wca1.cc
```

### Threat Intelligence

* IOC Type: Domain
* Malware/Family: Cobalt Strike
* ThreatFox Confidence: 75%

### VirusTotal

* Detection: **15/91**
* Categories included:

  * Suspicious
  * Phishing
  * Fraud

The observed HTTP response was:

```text
Status Code: 200
```

The page title was:

```text
Not Found
```

### URLScan.io

The submitted website could not be scanned.

The result indicated that the website could not be contacted or that network, TLS, or authentication conditions may have prevented scanning.

### MITRE ATT&CK

```text
T1021.004 — Remote Services: SSH
```

This mapping uses the documented Cobalt Strike capability associated with the threat-intelligence finding.

### Classification

**Malicious**

The classification was based on the ThreatFox Cobalt Strike association and multiple VirusTotal detections.

---

# 🔐 IOC #3 — SHA-256 Investigation

## Indicator

```text
275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f
```

### File Information

* File Type: PowerShell
* File Size: 68 bytes
* Magic: EICAR virus test files
* TrID: EICAR antivirus test file

### VirusTotal

```text
66/68 detections
```

### Important Interpretation

This hash belongs to an **EICAR antivirus test file**.

EICAR is intentionally harmless and is designed to test whether antivirus software detects a test signature.

Therefore, the IOC was **not classified as real malware**.

### Classification

**Security Test / Benign**

---

# 🧩 MITRE ATT&CK Mapping

| Context                  | MITRE ID  | Technique                 |
| ------------------------ | --------- | ------------------------- |
| Cobalt Strike IP IOC     | T1021.004 | Remote Services: SSH      |
| Cobalt Strike Domain IOC | T1021.004 | Remote Services: SSH      |
| EICAR Test File          | N/A       | No MITRE mapping assigned |

---

# 📁 Project Structure

```text
Threat-Intelligence-IOC-Verification/
│
├── README.md
│
├── ioc-log/
│   └── Threat_Intelligence_IOC_Log.xlsx
│
├── report/
│   └── Threat_Intelligence_IOC_Investigation_Report.pdf
│
└── screenshots/
    ├── 01-threatfox-ip.png
    ├── 02-virustotal-ip.png
    ├── 03-urlscan-ip.png
    ├── 04-threatfox-domain.png
    ├── 05-virustotal-domain.png
    ├── 06-urlscan-domain.png
    ├── 07-virustotal-hash.png
    └── 08-mitre-mapping.png
```

---

# 📋 IOC Log

The project maintains a structured IOC log containing:

* IOC
* IOC Type
* Source
* Malware/Family
* VirusTotal Result
* URLScan Result
* MITRE ATT&CK ID
* MITRE Technique
* Classification

The spreadsheet provides a quick reference for the investigated indicators.

---

# 🔒 Safety Practices

This project follows a safe IOC-analysis workflow.

* Malicious URLs were not intentionally opened.
* Malware samples were not downloaded or executed.
* Hashes were searched using their identifiers.
* Existing threat-intelligence scan results were used for analysis.
* The EICAR sample was treated as a harmless security test file.

---

# 📌 Key Findings

* The IP IOC was associated with Cobalt Strike in the observed threat-intelligence data.
* The domain IOC showed multiple VirusTotal detections and a Cobalt Strike association.
* URLScan.io could not successfully scan the two web-based IOCs, so the failed scans were documented without treating them as clean results.
* The SHA-256 IOC was identified as the EICAR antivirus test file.
* MITRE ATT&CK was used to document relevant Cobalt Strike behavior.
* All findings were consolidated into a structured IOC log.

---

# 🚀 Conclusion

This project demonstrates a practical threat-intelligence workflow for collecting, verifying, classifying, and documenting Indicators of Compromise.

The investigation combines multiple public security platforms to improve IOC validation and provides a structured approach that can be reused during security investigations and threat-intelligence analysis.

---

## 👨‍💻 Project Focus

**Cybersecurity | Threat Intelligence | IOC Analysis | MITRE ATT&CK | Security Investigation**
