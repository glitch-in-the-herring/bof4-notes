Resistance determines how much damage a combatant takes from attacks. In the case of Holy resistance, it also determines how much healing a combatant receives from a healing spell.
Internally, they are ordered as such:
- Melee
- Ranged
- Magical
- Breath
- Fire
- Wind
- Water
- Earth
- Holy
- Mind
- Status
- Death
 In some cases, the resistances start with Melee (Melee = 0, Ranged = 1, etc). In others, such as the primary element of the [[General Success Rate Formula]], the resistances start with Fire (Fire = 0, Wind =1, etc).
## Elemental Resistances
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d09c` in the files
* `0x801e509c` in the RAM
A negative percentage means that the damage is absorbed and heals the target's HP.

| Value | Damage taken |
| ----- | ------------ |
| 0     | 200%         |
| 1     | 150%         |
| 2     | 100%         |
| 3     | 75%          |
| 4     | 50%          |
| 5     | 25%          |
| 6     | 0%           |
| 7     | -100%        |
### Multi-element spells
When a spell has more than one element, the damage taken by the target is the average of damage taken from those elements. For example, if a target's wind resistance is 2 and fire resistance is 1, then the damage taken is $\frac{150\%+100\%}{2}=125\%$.
## Melee, Ranged, Magic, and Breath Resistances:
Unlike elemental resistances, level 7 does not let the target absorb the damage.
### Melee and Ranged
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d120` in the files
* `0x801e5120` in the RAM

| Value | Damage taken |
| ----- | ------------ |
| 0     | 200%         |
| 1     | 150%         |
| 2     | 100%         |
| 3     | 75%          |
| 4     | 50%          |
| 5     | 25%          |
| 6     | 0%           |
| 7     | 0%           |
### Magic and Breath
#### Offensive
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d130` in the files
* `0x801e5130` in the RAM

| Value | Damage taken |
| ----- | ------------ |
| 0     | 200%         |
| 1     | 150%         |
| 2     | 100%         |
| 3     | 75%          |
| 4     | 50%          |
| 5     | 25%          |
| 6     | 0%           |
| 7     | 0%           |

#### Healing
Magic resistance is used in the [[Healing Spells|healing spells formula]]. It applies a multiplier to the amount of healed HP
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d140` in the files
* `0x801e5140` in the RAM

| Value       | Healing amount |
| ----------- | -------------- |
| 0           | 0%             |
| 1           | 50%            |
| 2 and above | 100%           |
## Holy Resistance
Holy resistance serves two purpose: to calculate how much damage a combatant takes when it is hit with a holy-elemental attack, and to calculate how much healing a combatant takes when a healing spell is used on them. This resistance is ignored when healing spells are used outside of battle. 
### Offensive
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d148` in the files
* `0x801e50ac` in the RAM

| Value | Damage taken |
| ----- | ------------ |
| 0     | 200%         |
| 1     | 200%         |
| 2     | 150%         |
| 3     | 150%         |
| 4     | 125%         |
| 5     | 100%         |
| 6     | 50%          |
| 7     | 0%           |

### Healing
The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001d148` in the files
* `0x801e5148` in the RAM
A negative percentage means that the healing spell damages the target.

| Value | Healing amount |
| ----- | -------------- |
| 0     | -200%          |
| 1     | -150%          |
| 2     | 0%             |
| 3     | 25%            |
| 4     | 50%            |
| 5     | 100%           |
| 6     | 200%           |
| 7     | 300%           |
## Mind, Status, Death, and RNG Multiplier
Mind, Status, and Death primarily affect the success rate of some spells. Other resistances can also be used used to modify the success rate. The values can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001cfb8` in the files
* `0x801e4fb8` in the RAM

| Value | Multiplier |
| ----- | ---------- |
| 0     | N/A        |
| 1     | 150        |
| 2     | 100        |
| 3     | 75         |
| 4     | 50         |
| 5     | 25         |
| 6     | N/A        |
| 7     | N/A        |
### Holy RNG
Holy has its own RNG table which can be found at
* `BIN/BATTLE/BTLMOVE.EMI: 0001cfc8` in the files
* `0x801e4fc8` in the RAM

| Value | Multiplier |
| ----- | ---------- |
| 0     | N/A        |
| 1     | 200        |
| 2     | 100        |
| 3     | 50         |
| 4     | 25         |
| 5     | N/A        |
| 6     | N/A        |
| 7     | N/A        |