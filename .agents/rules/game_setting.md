# Game Setting
Legend of the Golden Dragon (LOGD) is set in a society of medeival technolgy in the classic swords and sorcery style.
THe game takes place in land composed of civilized areas bordering "The Dark Forest", which is a large monster filled forest
full of things that want to kill you.

The player must enter that forest and hunt the creatures in order to gain experience and money, which they then bring back to "town".



All towns in the game are connected by defined roads and forest paths, but players can also choose to leave the path and explore the untamed forest.

### 🛣️ Roads (Safe Travel)
* Roads connect civilized areas and DO NOT enter the forest.
* Travel consumes **1 stamina per kilometer** (reduced to **0.1 stamina/km** if riding an owned horse).
* Low encounter rate, but a 10% chance per trip of being attacked by roving **Brigands**.

### 🌲 Forest Paths (High Encounter Shortcuts)
* Predefined paths cut directly through the forest to link towns.
* Travel consumes **1 stamina per kilometer** (reduced to **0.1 stamina/km** if riding an owned horse).
* High monster encounter rate (30% chance of standard monster encounter).

### 🌳 Off-Path Exploration (The Deep Forest)
* At any point on a forest path, a player can choose to **Step Off the Path** to explore the deep forest.
* **Depth Parameter:** A player's exploration depth starts at `1` and can scale up to `20`. Each step deeper or backward consumes **1 stamina**.
* **Difficulty Scaling:** Monster difficulty scales exponentially with depth:
  `L_base = clamp(1, 20, Math.floor(Depth / 1.5) + 1)`
  The final spawned enemy's level varies dynamically based on a probability distribution table (see [encounters.md](file:///Users/benfollis/Documents/repos/legend_of_the_gold_dragon/.agents/rules/encounters.md) for precise roll percentages).
* **Getting Lost:** Moving off-path immediately tags the player as `lost`.
* **Backtracking:** Attempting to retreat step-by-step to find the path has a **20% chance per step of going the wrong way** (increasing depth instead of decreasing it).
* **Search for the Path Action:** Consumes **1 stamina**. Success chance:
  `Success Chance = 30% + (Luck / 1000) * 20%`
  On success, the player returns safely to the nearest Forest Path. On failure, they remain lost and are immediately ambushed by a monster.
* **The Secret Town Forest (Aethelwood):**
  Aethelwood is a mystical hidden forest town. It cannot be reached by normal roads. To find it, a player must reach a Deep Forest depth of `15` or higher, which grants a **5% chance per explore action** of discovering the canopy entrance leading inside.

## 🏛️ Civilized Towns
All towns have the following things:

1. **An armor shop** (Master smith daily good/high, weekly magical gear + apprentice low-quality pieces).
2. **A weapon shop** (Identical to armor shop but for offensive weapons).
3. **A potion shop** (Selling Detox, Health, and Stamina potions).
4. **An arena** (Fight gladiators for gold, and place bets on running gladiator matches).
5. **A training center** (Undergo the level-up ritual once sufficient experience is earned).
6. **A bank branch** (Store gold safely away from death penalties; earns 1% daily interest up to a 1,000 gold cap).
7. **A tavern and inn** (Rent rooms for safe logout and stamina replenishment, buy drinks, bribe bartender for keys, or solicit prostitutes).
8. **A stable** (Purchase horses to reduce travel stamina costs to 1/10th on roads and paths).
9. **A healer's shop** (Replenish missing HP for a fee of 2 gold per HP).
10. **A quest board** (Fulfill bounty or material collection quests commissioned by local nobles for gold/item rewards).

This is a dangerous and untamed society. Roving brigands seek to prey on the weak, and the Dark Forest is filled with beasts. Ensure you are well-equipped before venturing forth!
