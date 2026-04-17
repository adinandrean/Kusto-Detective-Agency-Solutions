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

## 🔍 Phase 2: Identifying the Gang
To find the 4 members, I applied several behavioral filters:

Group Size: Isolated channels where exactly 4 unique users joined.

Exclusivity: Filtered for users who only joined one channel during the entire log period, suggesting a dedicated "War Room."

Communication Hygiene: Used a leftanti join to remove users who sent Direct Messages (DMs) to anyone else, as the heist team was described as having "minimal interaction with the external world."

The "Sync" Pattern: In the final 3 candidate channels, I looked for rhythmic behavior. Channel cf053de3c7b showed 4 members posting exactly one message each in quick succession every two days—a classic "sync-up" behavior.