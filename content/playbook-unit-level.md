# AI Insight Generation Blueprint: A Step-by-Step Protocol

**Objective:** To define a deterministic, step-by-step process for the AI to analyze a property's performance data, build a transparent scorecard, and generate a concise, data-driven explanation for a given rental rate recommendation.

---

## Section 1: The Analytical Framework

The AI's reasoning is built on a hierarchical analysis of primary and secondary data factors, which are consolidated into three core "Signals" to determine a final verdict.

* **Primary Data Factors:** Occupancy, Exposure, Demand, Rate Anchors (advertised, executed)
* **Secondary Data Factors (Influencers & Constraints):** Fallback explanations used only when the primary data cannot explain the recommended rate action.

---

## Section 2: The Four-Step Analysis Protocol

### Step 1: Data Ingestion & Signal Calculation

| Signal | Calculation Logic |
|--------|-------------------|
| **Occupancy** | Nullification: If min_lease_to_goal and property_goal both 'Increase' → 'Increase'. Both 'Decrease' → 'Decrease'. Conflict → 'Neutral'. |
| **Exposure** | If total_exposure_units < 10% of total_units → 'Increase'. Else → 'Decrease'. |
| **Demand** | If at least one demand score is 'Increase' → 'Increase'. 'Decrease' only if both are 'Decrease'. |

### Step 2: Determine Final Verdict Signal using The Matrix

Combine the three signals (Occupancy, Exposure, Demand) to find majority consensus. Examples: I/I/I → Increase (High-Conf); D/D/D → Decrease (High-Conf); N/D/I → Maintain/Contextual.

### Step 3: Reconcile Verdict with Actual Outcome & Find the "Why"

**Primary Anchor Check (Advertised Rate):** Does direction of (optimal - advertised) match rate_change_direction?
- **If YES:** Use advertised as anchor.
- **If NO:** Move to Secondary Anchor (Executed Rate).

**Secondary Anchor Check (Executed Rate):** Does direction of (optimal - executed) match rate_change_direction?
- **If YES:** Use executed as anchor; acknowledge conflict.
- **If NO (Double Conflict):** Trigger Fallback Path (constraints, influencers).

**Happy Path:** Verdict aligns with outcome. Construct narrative with quantitative data.
**Fallback Path:** Verdict contradicts outcome. Investigate constraints and influencers.

### Step 4: Assemble the Final JSON Response

Generate JSON output ("title", "phrase", "keywords") based on Step 3 conclusion.

---

## Section 3: Scenario Examples

**I/I/I (High-Conf Increase):** All signals align. Focus on occupancy, low exposure, strong demand.
**D/D/D (High-Conf Decrease):** All signals align. Focus on high exposure, weak demand, below goals.
**N/D/I (Maintain):** Classic conflict of high supply vs. high demand. Frame as balanced, hold steady.
