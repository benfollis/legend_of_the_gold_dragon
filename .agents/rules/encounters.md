# Random Encounters & Enemy Scaling

This document defines the rules for rolling random enemy encounters and determining their combat levels.

## 📊 Encounter Level Variance Algorithm

When a random enemy encounter is triggered (whether on forest paths or off-path deep forest exploration), the game first calculates the **Baseline Encounter Level ($L_{\text{base}}$)** for the current location or depth:
* **Paths & Roads:** Set by the region's difficulty cap (e.g., Oakhaven: 1–3, Riverbend: 4–8, Stonehold: 9–15, Shadowfen: 16–20).
* **Off-Path Deep Forest:** Determined by exploration depth:
  `L_base = clamp(1, 20, Math.floor(Depth / 1.5) + 1)`

Once $L_{\text{base}}$ is calculated, a percentile roll is made to determine the final **Enemy Level**:

| Roll Probability | Level Adjustment | Final Enemy Level |
| :--- | :--- | :--- |
| **50%** | Same level | $L_{\text{enemy}} = L_{\text{base}}$ |
| **10%** | 1 level below | $L_{\text{enemy}} = \max(1, \; L_{\text{base}} - 1)$ |
| **10%** | 1 level above | $L_{\text{enemy}} = \min(20, \; L_{\text{base}} + 1)$ |
| **1%** | 3 levels above | $L_{\text{enemy}} = \min(20, \; L_{\text{base}} + 3)$ |
| **29%** (Remainder) | Random levels below | $L_{\text{enemy}} = \max(1, \; L_{\text{base}} - \text{random}(2, \; L_{\text{base}} - 1))$ |

* *Note:* The final calculated enemy level is always clamped between a minimum of **level 1** and a maximum of **level 20**.

---

## 🏷️ Procedural Enemy Name Pool

Enemies are procedurally named by combining a **Prefix**, **Base Name**, and optional **Suffix** randomly pulled from the thematic tables below:

| Prefix (1-20 Lvl) | Base Name (Type) | Suffix (Rare / Deep Forest) |
| :--- | :--- | :--- |
| *Feral* | *Wolf* | *of the Abyss* |
| *Savage* | *Boar* | *Stalker* |
| *Gloom* | *Spider* | *Devourer* |
| *Corrupted* | *Goblin* | *of the Shadow* |
| *Rabid* | *Orc* | *Bane* |
| *Spectral* | *Troll* | *Reaver* |
| *Blighted* | *Specter* | *Slayer* |
| *Vicious* | *Drake* | *of the Dark* |
| *Plague* | *Golem* | *Terror* |

*Example Names:* "Savage Goblin Stalker", "Spectral Drake of the Dark", "Feral Boar".

---

## 📈 Enemy Stat Baselines & Variance

An enemy's core stats (Attack, Defense, HP) are determined by their level, modified by random variance and **geographical weighting** (deep forest enemies are stronger than path/road enemies).

### 1. Stat Baselines
* **Base Attack ($A_{\text{base}}$):** $L_{\text{enemy}} \times 80$
* **Base Defense ($D_{\text{base}}$):** $L_{\text{enemy}} \times 70$
* **Base HP ($HP_{\text{base}}$):** $L_{\text{enemy}} \times 100$

### 2. Strength (Attack) Variance & Geographical Weighting
To create varying difficulty, an enemy's **Strength (Attack)** is modified by a rolled variance factor ($V_{\text{str}}$) with a maximum **50% variance** from the baseline. This factor is weighted depending on *where* the encounter takes place:

* **🛣️ Paths & Roads (Milder Enemies):**
  * $V_{\text{str}}$ is rolled between **`0.5` and `1.2`** (50% to 120% of baseline).
  * Formula: $\text{Attack}_{\text{path}} = \text{Math.floor}(A_{\text{base}} \times V_{\text{str}})$
* **🌳 Off-Path Deep Forest (Stronger Enemies):**
  * $V_{\text{str}}$ is rolled between **`0.8` and `1.5`** (80% to 150% of baseline).
  * Formula: $\text{Attack}_{\text{forest}} = \text{Math.floor}(A_{\text{base}} \times V_{\text{str}})$

### 3. Defense & HP Variance
Defense and HP undergo a standard variance roll of **$\pm 15\%$** (between `0.85` and `1.15`) regardless of location:
* $\text{Defense} = \text{Math.floor}(D_{\text{base}} \times \text{random}(0.85, \; 1.15))$
* $\text{HP} = \text{Math.floor}(HP_{\text{base}} \times \text{random}(0.85, \; 1.15))$

---

## 💰 Enemy Gold Drops Scaling

When an enemy is defeated, they drop a quantity of gold that scales exponentially with their level ($L_{\text{enemy}}$). This is to support the extremely high costs of high-level equipment:

$$\text{Gold Dropped} = \text{Math.floor}\left(100 \times (L_{\text{enemy}})^{1.75} \times \text{random}(0.8, \; 1.2)\right)$$

* **Roll Variance:** Gold dropped ranges between `80%` and `120%` of the baseline gold scaling.
* **Luck Scaling:** The player's Luck stat (`Luck / 1000`) rolls a chance to double this final gold reward.


