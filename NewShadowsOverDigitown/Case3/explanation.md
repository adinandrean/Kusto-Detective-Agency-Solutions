# 🏦 Case 3: Bank Robbery

### 📖 Scenario
A professional gang of three robbed a bank at **157th Ave / 148th Street**. They escaped in three separate vehicles just minutes before the police sealed off the city. 

The timeline is critical:
* **08:17 - 08:31:** The robbery takes place.
* **08:31 - 08:40:** The gang escapes.
* **08:40:** The city is sealed; no vehicle can leave.

Our task is to analyze the city-wide camera recordings (`Traffic` table) and locate the gang's hiding place where all three vehicles met.

### 💡 The Investigation Logic
Finding three specific cars among thousands requires a process of elimination:

1.  **Eliminating "Noise":** I first identified all vehicles that were already moving during the robbery. Since the robbers were inside the bank, their getaway cars were likely parked.
2.  **Identifying the Getaway Vehicles:** I filtered for cars that:
    * Were NOT moving during the heist.
    * Appeared for the first time in the camera logs between **08:31 and 08:41** (immediately after the robbery).
    * Started their journey specifically from the bank's coordinates (**157th Ave / 148th Street**).
3.  **Tracking to the Hideout:** Once I had the list of potential VINs (Vehicle Identification Numbers), I tracked their movements until the end of the recording period (11:00 AM).
4.  **Finding the Convergence Point:** The "smoking gun" was the location where three of these specific VINs ended their journey at the same coordinates.

### 🛠️ Key KQL Techniques Used
- **Variable sets (`let` with `distinct`):** To create a list of "moving" cars to be excluded.
- **`arg_min()` / `arg_max()`:** To capture the exact start and end points of each vehicle's journey.
- **`where VIN !in (moving)`:** A powerful exclusion filter to narrow down suspects.
- **`make_list()` + `array_length()`:** To group vehicles by their final destination and identify where exactly 3 of our suspects met.

---

### 🚨 Spoiler Alert:
If you want to know how to pinpoint the hideout:

<details>
<summary>Click to reveal the investigation hint</summary>

The robbers split up to confuse the police, but they all headed to the same secret location. 

By grouping the final `Ave` and `Street` of the suspect cars:
`| summarize list_VIN = make_list(VIN) by Ave, Street`
`| where array_length(list_VIN) == 3`

You will find a single coordinate pair where the three getaway cars are currently parked. 

</details>

---