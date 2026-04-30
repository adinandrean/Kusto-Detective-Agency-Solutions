# 🕵️‍♂️ Kusto Detective Agency - My Journey
This repository contains my solutions for the **Kusto Detective Agency** challenges provided by Microsoft. It showcases my ability to analyze large-scale datasets, identify security threats, and master the **Kusto Query Language (KQL)**.

---

## 🎯 Project Overview
The Kusto Detective Agency is a gamified experience where you solve data-driven mysteries using Azure Data Explorer. Through these cases, I've developed expertise in:
* **Cybersecurity Analytics:** Tracking malicious activities and anomalies.
* **Geospatial Analysis:** Mapping coordinates and tracking movements (H3/S2 cells, street grid system).
* **Performance Optimization:** Writing efficient queries for billions of records.

---

## 🛠️ Key KQL Skills Demonstrated
In these solutions, I make extensive use of:
- **Aggregations:** `summarize`, `arg_max()`, `arg_min()`, `make_list()` etc.
- **Joins & Lookups:** Connecting disparate datasets using `lookup` and `join`.
- **Data Transformation:** `mv-expand`, `extend` and **Window Functions** (`prev`/`next`)
- **Time-Series & Geometry:** `bin()`, `geo_distance_2points()`, `geo_point_to_h3cell` etc.
- **Data Analysis:** Time-series anomaly detection, frequency analysis, pattern recognition.
- **Problem Solving:** Translating complex riddles and real-world scenarios into efficient queries.
- **Social Graph & Network Analysis**: Identifying isolated groups through exclusive interactions and cardinality
- **Digital Forensics & OSINT**: Correlating system logs with external metadata (EXIF data, emails) and Open-Source Intelligence (OSINT) to verify findings
- **Complex Decryption & UDFs**: Successfully analyzed and executed provided User-Defined Functions (UDFs) to decrypt hidden messages, demonstrating the ability to integrate custom logic into investigative workflows.
---

## 📂 Repository Structure
### New Shadows over Digitown
| Case | Title | Key Concept Used | Documentation | Solution Code |
| :--- | :--- | :--- | :--- | :--- |
| **0** | Onboarding | Basic KQL & Summation | [Explanation](./NewShadowsOverDigitown/Case0/explanation.md) | [View Code](./NewShadowsOverDigitown/Case0/solution.kql) |
| **1** | The rarest book is missing! | Data Joins & Weight Analysis | [Explanation](./NewShadowsOverDigitown/Case1/explanation.md) | [View Code](./NewShadowsOverDigitown/Case1/solution.kql) |
| **2** | Election fraud? | Anomaly Detection & Time-series | [Explanation](./NewShadowsOverDigitown/Case2/explanation.md) | [View Code](./NewShadowsOverDigitown/Case2/solution.kql) |
| **3** | Bank Robbery | Geospatial Tracking & Exclusion Logic | [Explanation](./NewShadowsOverDigitown/Case3/explanation.md) | [View Code](./NewShadowsOverDigitown/Case3/solution.kql) |
| **4** | Ready to play? | H3 Geospatial, Window Functions & Cryptography | [Explanation](./NewShadowsOverDigitown/Case4/explanation.md) | [View Code](./NewShadowsOverDigitown/Case4/solution.kql) |
| **5** | Big Heist | Forensics, Social Graph & Decryption | [Explanation](./NewShadowsOverDigitown/Case5/explanation.md) | [View Code](./NewShadowsOverDigitown/Case5/solution.kql) |

### Echoes of Deception
| Case | Title | Key Concept Used | Documentation | Solution Code |
| :--- | :--- | :--- | :--- | :--- |
| **0** | Onboarding | Basic KQL & Summation | [Explanation](./EchoesOfDeception/Case0/explanation.md) | [View Code](./EchoesOfDeception/Case0/solution.kql) |
| **1** | To bill or not to bill? | Data deduplication & Joins|  [Explanation](./EchoesOfDeception/Case1/explanation.md) | [View Code](./EchoesOfDeception/Case1/solution.kql) |
---

## 🚀 How to Run These Queries
1. Access the [Kusto Help Cluster](https://detective.kusto.io/) and create an account.
2. Navigate to the relevant Challenge (use `Switch Challenge`) and then select the case from the inbox(after completing a case, you can move on to the other one).
3. Clone the tables on your Azure dataexplorer using the provided script at the end of case description.
4. Copy the code from the `.kql` files in this repo and run it.

---

## 📱 Let's Connect!
If you have questions about these solutions or want to talk about **Security Operations (SecOps)** or **Big Data**, feel free to reach out:
- **LinkedIn:** [Adrian Nandrean](www.linkedin.com/in/adrian-nandrean-2b704171)
- **Email:** [adinandrean@gmail.com]
