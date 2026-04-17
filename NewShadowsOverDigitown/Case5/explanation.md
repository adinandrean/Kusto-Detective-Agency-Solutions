# 🕵️‍♂️ Case 5: Big Heist

## 📝 Scenario Overview
A major heist is being planned by a 4-member team. The only traces left are metadata logs from a public chat server. The goal was to identify the suspects' IP addresses, infiltrate their machines via a provided utility, and decode hidden messages to find the **exact time and location** of the crime.

---

## 🛠️ Phase 1: Data Structuring & Pattern Discovery
The `ChatLogs` table contained unstructured text messages. I implemented an iterative parsing strategy to map all possible system messages and identify patterns:

* **Message Types Categorized:**
    * `LI` / `LO`: Login/Logout events (essential for extracting User-IP mappings).
    * `JC` / `LC`: Joining and Leaving channels.
    * `DM` / `CM`: Direct Messages vs. Channel Messages.

```kusto
// Example of the logic used to unify the data
| extend 
    User = coalesce(SenderID, UserID, UserID2, UserID3, UserID4),
    MsgType = case(
        isnotempty(destType) and destType has "user", "DM",
        isnotempty(destType) and destType has "channel", "CM",
        ...
    )
```
## 🔍 Phase 2: Identifying the Gang
The heist team was characterized by minimal interaction and high secrecy. I isolated them using a strict process of elimination:

1. **Group Size**: Filtered for channels containing exactly 4 unique users.

2. **Exclusivity**: Focused on users who joined only one channel (the heist "War Room").

3. **Behavioral Cleaning**: Used leftanti join to eliminate users engaging in DMs with outsiders, ensuring the group was a closed loop.

4. **Temporal Analysis**: Identified channel cf053de3c7b by observing a "sync" pattern—members posted sequentially every second day at specific times.

## 💻 Phase 3: Forensic Infiltration (SneakInto)
After extracting the **Login IPs** for the 4 suspects, I used the *SneakInto* utility to analyze their local files. The evidence gathered was:


* **Image Metadata (EXIF)**: Extracted *Date1* and *GPS* coordinates from image3.jpg.

* **Advanced Cryptography**: I applied the custom *ReadMessage* function to the "PS:" section of the challenge description using the key from the previous case. This revealed a hidden Bing search query pointing to a specific historical year (YYYY).

* **Cryptographic Riddle**: Decoded a formula from an email: Date1 + (YYYY % 1000) days.

## 🛠️ Technical Skills Demonstrated
* **Data Engineering**: Multi-stage *parse* and *coalesce* to structure "dirty" logs.

* **Advanced Filtering**: Using *make_set*, *mv-expand*, and *leftanti* joins for social graph analysis.

* **Security Mindset**: Correlating Chat Metadata with Login IPs (SIEM-like investigation).

* **Functional Programming**: Executing complex user-defined functions for decryption.