# 🔍 Case 1: The rarest book is missing!

### 📖 Scenario
The rarest book in the museum, `De Revolutionibus Magnis Data`, is missing! However, the investigation reveals some interesting clues:
1. The book has a specific **weight** recorded in the catalog.
2. It was equipped with an **RFID sticker**, but that sticker was found detached on the museum floor.
3. Each **Shelf** in the museum has a weight sensor (total weight) and an RFID scanner.

### 💡 The Investigation Logic
To locate the physical book without its digital tag, I followed this strategy:
* **Identify the target:** Retrieve the precise weight of the missing book from the `Books` catalog.
* **Calculate expected weight:** Use `mv-expand` on the shelf data and `lookup` with the catalog to find the "digital" weight (sum of all scanned books).
* **Find the discrepancy:** Compare the **actual physical weight** (sensor) with the **digital weight** (scans).
* **Pinpoint the location:** The shelf where the weight difference matches the missing book's weight is where the book is physically located.

### 🛠️ Key KQL Techniques Used
- `toscalar()` - For storing the target weight.
- `mv-expand` - For handling the dynamic list of RFIDs.
- `lookup` - For joining shelf data with book metadata.

---

### 🚨 Spoiler Alert:
If you want to see more hints:

<details>
<summary>Click to reveal the hint for the solution</summary>

To find the missing shelf, I didn't use the book's exact weight, but rather a **10% margin of error**. 

This is crucial because physical weight sensors often have slight discrepancies compared to official database records. Using the `between` operator with a range (e.g., `weight * 0.9 .. weight * 1.1`) ensures you don't miss the target due to minor sensor noise.

</details>

---