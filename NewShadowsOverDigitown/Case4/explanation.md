# 🌉 Case 4: Ready to play?

### 📖 Scenario
The mysterious message from "El Puente" challenged me to prove my worth through a multi-layered riddle. The trail started with a massive dataset of prime numbers and ended on the streets of Brooklyn, requiring the decryption of a hidden message.

The investigation was split into three major phases: **Mathematical Decoding**, **Geospatial Identification**, and **Visual OSINT**.

### 💡 The Investigation Logic

#### Phase 1: The Prime Gateway
The first clue pointed towards "Special Prime Numbers" (primes that are the sum of two consecutive primes + 1). 
* **The Task:** Find the largest special prime under 100,000,000.
* **The Logic:** Using the `prev()` function in KQL, I compared each prime with its predecessor to calculate potential "Special Primes" and joined the results back to the original list to validate them.
* **The Result:** The resulting number unlocked a hidden ingestion script for the `nyc_trees` dataset.

#### Phase 2: The Tree Whisperer (Geospatial Analysis)
The second hint described a specific urban micro-environment: a small area containing exactly **1 Turkish Hazelnut** and **4 'Schubert' Chokecherries**.
* **The Tool:** I used **H3 Cells** (resolution 10), which hexagonalize the map into cells of ~66m radius.
* **The Search:** By joining the locations of different tree species on their H3 Cell ID, I isolated the unique cell that matched the signature.
* **The Target:** Inside that specific cell, I was instructed to find the smallest **American Linden** tree, which provided the final coordinates.

#### Phase 3: Street View OSINT
The coordinates led me to a specific street corner in Brooklyn.
* **Virtual Tour:** Using a custom `VirtualTourLink` function, I inspected the location in Street View.
* **The Discovery:** I found a vibrant mural titled **"Muralistas de El Puente"**.
* **The Key:** The message "ASHES TO ASHES" provided the decryption key needed to unlock the final message from El Puente.

### 🛠️ Key KQL Techniques Used
- **`prev()` & `next()`:** For window functions over ordered numerical data.
- **`geo_point_to_h3cell()`:** To perform high-precision geospatial grouping without complex polygon math.
- **`make_set()` & `array_length()`:** To filter clusters based on specific counts of distinct entities.
- **`arg_min()`:** To find the specific attributes (longitude/latitude) of the smallest tree in a subset.
- **`Decrypt()`:** To reveal the final hidden message using the discovered key.

---

### 🚨 Challenge Insight:
The hardest part was realizing that "El Puente" wasn't just a name, but a physical location that bridged the gap between raw data and the real world.

> **Final Key Found:** `ASHES TO ASHES`