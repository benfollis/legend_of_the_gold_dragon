# About the player

The player is a warrior who starts in a random town at level 1.


## Levels

There are 20 levels the character may proceed through, 1-20, which they do by gaining experience.
To advance a level you must aquire 1.75 times the experience of the previous level.
To advance from level 1 to 2 takes 1000 experience

A player may level up by reaching the required experience and undergoing a ritual at the training hall.

Leveling up does the following
1. increases hit points by 25%
2. increases unarmed (base) attack by 100
3. increases unarmored (base) defense by 100


## Hit points and Stamina

### Hit points
Hit points representt eh current "life" of an player. When hit points reach 0 the player dies, and must be resurected
Hit points are reduced by an opponents attack, and replenished by a healer or other game event

### Stamina
Stamina represents the number of actions a player can take without being fatigued.
When stamina reaches 0, then the user's attack and defense decrease by 50%, and decrease by 5% per action.
Stamina is replenished by sleeping with 12% of the players stamina returned by sleeping per wall clock hour

Stamina may also be replenished by in game special events.

### Sleeping
A player may chose to sleep in their current location by hiding, however if they do so they will experience a random chance of being attacked by a monster or a brigand.
If attacked in this manner the opponent gets a 50% chance to make a free first attack at double damange.

If sleeping in the inn, the player may not be attacked unless the door is unlocked (which occurs if another player bribes the bartender for a room key). If attacked in their inn room, the player will always wake up to the door opening and will not suffer a first attack penalty. The combat is resolved as a standard turn-based PvP fight (with the sleeping player's actions simulated based on their current stats and equipment).

## Actions
Actions that consume one stamina are as follows
1) Moving one kilometer along a road (reduced to 0.1 stamina if riding an owned horse).
2) Entering the forest.
3) Leaving the forest and entering a town.
4) Moving one kilometer along a forest path (reduced to 0.1 stamina if riding an owned horse).
5) Fighting one round with an opponent.



## Stats
### Combat Stats
There are two basic combat stats for the player, defense, and attack.
The damage an opponents attack does to the players hit points is calculated using the following formula:

`Damage = max(0, Math.floor((Attack - Defense) * Random_Variance))`

* **Random_Variance:** A randomly rolled decimal float between `0.85` and `1.15` inclusive.
* **Zero Damage:** If the defender's defense is high enough relative to the attacker's attack, the calculated damage will be `0` (it does not default to a minimum of 1).

Weapons add a weapon specific value to the players attack stat.
Armor adds an armor specific value to the players defense stat.


### Non Combat stats
There are other stats that effect non combat actions

1 Luck
1.1 ranges from 1 - 1000, starting at 1.
1.2 Effects the chance of acquiring double gold from killing a monster (probability is evaluated as `Luck / 1000`).
1.3 Effects the chance of landing a double damage strike on an opponent (probability is evaluated as `Luck / 1000`).

2 Stamina
2.1 ranges from 1 - 1000 starting at 100. Represents the maximum amount of stamina the player can have.
2.2 for every day that you consume at least 50% of your stamina you gain 1 stamina point
2.3 For every day that you don't consume at least of your stamina, you lose 1 stamina point

3 Charm
3.1 Ranges from 1-infinity, starting at 1
3.2 effects the chance of a favorible outcome when interacting with NPCs.


# Death
When a player is defeated in combat and dies, the following will happen
1. All on hand gold will be lost
2. 10% of experienc will be lost.
3. The player will lose all stamina
4. The player will be prevented from entering the game for 24 hrs.
On the next enterance to the game the player will start in the town center of the last town they were in.

