# Case 0: The Most Epic Detective of the Year

## 🕵️ Mission Overview
The objective is to analyze the Kusto Detective Agency's 2022 archives to identify the "Most Epic Detective of the Year." The title is awarded to the detective who claimed the most bounty money. 

**Rules of the Game:**
1. Only the **first** detective to solve a case (claim the bounty) receives the reward.
2. We need to correlate case opening data (where the bounty is defined) with case completion data (where the detective is identified).

---

## 🛠️ Data Exploration
Upon initial inspection of the `DetectiveCases` table, I identified two key event types:
- `CaseOpened`: Contains a JSON string in the `Properties` column with the `Bounty` value.
- `CaseSolved`: Identifies the `DetectiveId` and the `Timestamp` of the solution.

---

## 🚀 The Solution: Step-by-Step

### Step 1: Pre-processing Bounties
Since the bounty amount is stored within a dynamic/JSON column, I first isolated the "CaseOpened" events and extracted the `Bounty` value as an integer for calculations.

```kusto
let bountyPrice = DetectiveCases
| where EventType == "CaseOpened"
| extend Bounty = toint(Properties.Bounty);
```

### Step 2: Correlating Solutions with Rewards
I performed an `inner join` between the solve events and my pre-processed bounty list using the unique `CaseId`. This maps each solution to its respective monetary value.

### Step 3: Handling Concurrency (The "First Come, First Served" Rule)
In a real-world scenario, multiple detectives might solve the same case. To strictly follow the agency rules, I used `arg_min(Timestamp, ...)` grouped by `CaseId`. This ensures that only the earliest timestamp (the actual winner) is credited.

### Step 4: Final Aggregation
The last step involved summing up the total bounties per `DetectiveId` and sorting to find the top earner.

---
## 💻 Final KQL Query

```kusto
// Define the bounty per case
let bountyPrice = DetectiveCases
| where EventType == "CaseOpened"
| extend Bounty = toint(Properties.Bounty);

// Identify the winners and aggregate the total moolah
DetectiveCases
| where EventType == "CaseSolved"
| join kind=inner (bountyPrice) on CaseId
// Ensure only the first detective to solve each CaseId gets credit
| summarize arg_min(Timestamp, Bounty, DetectiveId) by CaseId
// Calculate the leaderboard
| summarize TotalBounty = sum(Bounty) by DetectiveId
| top 1 by TotalBounty desc
```

## 💡 Key Learnings & Skills Demonstrated
- **JSON Parsing**: Efficiently extracting values from dynamic columns using `toint(Properties.Bounty)`.

- **Data Correlation**: Using join to link disparate events (Open vs. Solved) via a shared key (`CaseId`).

- **Precision Aggregation**: Utilizing `arg_min` to handle competitive race conditions (multiple solvers for one case).

- **Business Logic Translation**: Converting the "first solver wins the bounty" rule into a functional, optimized query.
