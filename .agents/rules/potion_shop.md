# Potion Shops

Potion shops are where players can buy consumable items to heal, restore stamina, or cure status effects. Potions can be used in town or during forest exploration to maintain player stamina and health.

## 🧪 1. Consumable Potions (Recovery)
Consumables are standard recovery options used to cure status ailments, restore health, or temporarily replenish current stamina.

| Consumable Name | Purchase Cost (Gold) | Effects & Mechanics |
| :--- | :--- | :--- |
| **Detox Potion** | **50 gold (Static)** | Instantly removes the `inebriated` (intoxicated) status effect, restoring Attack and Defense to normal. Cost does not scale. |
| **Health Potion** | **150 gold (Static)** | Instantly restores **+100 Hit Points** (up to the player's max HP). Cost does not scale. |
| **Stamina Elixir** | **$300 \times L_{\text{player}}$** | Instantly restores **+50 Stamina** (up to the player's max Stamina). Cost scales with player level ($L_{\text{player}}$). |

---

## 🔮 2. Permanent Stat Potions
The potion shop also offers a collection of highly rare, magical potions that **permanently** increase the player's base stats by **+1 point** per consumption. 

### 📐 Double-Scaling Cost Formula
To keep stats balanced at higher levels, the cost of a permanent stat potion scales **with both the player's level ($L_{\text{player}}$) and their current value in that specific stat ($\text{Stat}_{\text{current}}$)**:

$$\text{Potion Cost} = \text{Math.floor}\left(\text{Base\_Cost} \times L_{\text{player}} \times \left(1 + \frac{\text{Stat}_{\text{current}}}{\text{Scale\_Factor}}\right)\right)$$

| Stat Potion | Permanent Effect | Base Cost | Scale Factor | Exact Potion Cost Equation |
| :--- | :--- | :--- | :--- | :--- |
| **Luck Potion** | Base Luck **+1** | 100g | 100 | $\text{Cost} = \lfloor 100 \times L_{\text{player}} \times (1 + \frac{\text{Luck}_{\text{current}}}{100}) \rfloor$ |
| **Attack Potion** | Base Attack **+1** | 500g | 100 | $\text{Cost} = \lfloor 500 \times L_{\text{player}} \times (1 + \frac{\text{Attack}_{\text{current}}}{100}) \rfloor$ |
| **Defense Potion** | Base Defense **+1** | 500g | 100 | $\text{Cost} = \lfloor 500 \times L_{\text{player}} \times (1 + \frac{\text{Defense}_{\text{current}}}{100}) \rfloor$ |
| **Stamina Potion** | Max Stamina **+1** | 300g | 50 | $\text{Cost} = \lfloor 300 \times L_{\text{player}} \times (1 + \frac{\text{Stamina}_{\text{max}}}{50}) \rfloor$ |

Potions have different levels of regenerative effects, based on 3 levels - basic, standard, and strong. 
