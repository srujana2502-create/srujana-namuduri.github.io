# Playbook: AI Insight Generation for Unit Groups — A Deterministic Protocol

## 1. Philosophy and Anti-Hallucination Principles

The objective of this insight is to function as a reliable, data-driven dashboard summary. It is **not** an interpretation or a creative narrative. To ensure accuracy and prevent hallucinations, the AI must adhere to the following core principles:

* **Absolute Grounding:** Every word and number in the generated phrase must be directly traceable to a specific key-value pair in the input JSON payload. The AI is forbidden from using outside knowledge or making assumptions about data that is not present.
* **Report, Don't Synthesize:** The AI's role is that of a reporter, not an analyst. It must report the trends and metrics of the group's members. It **must never** create a synthetic, group-level "why" (e.g., "The group is increasing rates because the market is hot"). It reports the *what*, and the *why* is explicitly left to the unit-type level insights.
* **Deterministic Logic:** The AI will follow a precise, programmatic set of steps. The choice of language for key parts of the insight is determined by simple calculations and conditional logic, not by creative choice.
* **Fixed Templates:** For consistency and accuracy, the AI will use pre-defined sentence structures ("templates") for presenting data. This minimizes variability and the risk of misstating facts.

---

## 2. Required Input Data Schema

The AI requires a structured JSON payload. The presence and accuracy of these fields are essential for the protocol to function correctly.

```json
{
  "group_name": "One Bedroom Floor Plans",
  "group_level_metrics": {
    "avg_advertised_rent": 1650,
    "avg_executed_rent": 1675,
    "avg_optimal_rent": 1685,
    "competitor_average_rent": 1700,
    "total_vacant_units": 8,
    "total_upcoming_renewals": 15,
    "current_occupancy_percent": 94.5
  },
  "unit_type_details": [
    {
      "unit_type_name": "A1a",
      "rate_change_direction": "Increase",
      "best_optimal_rent": 1595,
      "avg_advertised_rent": 1570,
      "avg_executed_rent": 1580
    }
  ]
}
```

---

## 3. The Step-by-Step Generation Protocol

### Step 1: Generate the Opening Statement

1. **Count Directions:** Iterate through the unit_type_details array and count the occurrences of each rate_change_direction.
2. **Select Template:**
   * **If count_increase is the clear majority:** "The **[group_name]** group is showing a strong upward trend, with most unit types seeing rate increases."
   * **If count_decrease is the clear majority:** "The **[group_name]** group is showing a clear downward trend, with most unit types seeing rate decreases."
   * **In all other cases (mixed signals, ties):** "The **[group_name]** group is showing mixed performance with varied rate strategies."

### Step 2: Generate the Individual Unit Breakdown (Loop)

For each unit type, execute the **Anchor Analysis Sub-routine:**

1. Check if avg_advertised_rent is 0 or null.
2. If not, check if the direction of (best_optimal_rent - avg_advertised_rent) conflicts with the rate_change_direction.
3. **Advertised Anchor Template** (no conflict): "**[unit_type_name]:** Recommended **[Direction]** to **$[optimal]** from an advertised rate of **$[advertised]**."
4. **Executed Anchor Template** (conflict or advertised is $0): "**[unit_type_name]:** Recommended **[Direction]** to **$[optimal]**, a move that aligns with the executed average of **$[executed]**."

### Step 3: Generate the Group Averages Block

"Across the group, the average optimal rate is **$[avg_optimal_rent]**, compared to an average advertised rate of **$[avg_advertised_rent]** and an executed average of **$[avg_executed_rent]**."

### Step 4: Generate the Competitor & Operations Block

"This compares to a competitor average of **$[competitor_average_rent]** in the market. Operationally, the group currently has **[total_vacant_units]** vacant units and **[total_upcoming_renewals]** upcoming renewals, maintaining a combined occupancy of **[current_occupancy_percent]%**."

### Step 5: Append the Mandatory Closing Statement

"For a detailed explanation of the factors driving each recommendation, please view the AI insights at the individual unit type level."
