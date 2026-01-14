## Selected Action

| Byte   | Action          | Notes                                     |
| ------ | --------------- | ----------------------------------------- |
| `0x01` | Physical attack |                                           |
| `0x02` | Guard           |                                           |
| `0x03` | Escape?         | Shows the escape message but does nothing |
| `0x04` | Spell           | The byte after is the ID of the spell     |
| `0x05` | Use item        | The byte after is the ID of the item      |
Anything above `0x05` does not work.
## Player's Party
The memory location that stores the action that the current party member chooses is located at `+0x139` from the party member's base address.

## Targeting 
See also [[Targeting]] for spells.
There can be up to 10 combatants in a battle. 

| Index       | Target                          |
| ----------- | ------------------------------- |
| `0x00-0x05` | Individual player party members |
| `0x06-0x09` | Individual enemy party members  |
| `0x10`      | All of player's front row       |
| `0x20`      | All of player's back row        |
| `0x30`      | All of player's party members   |
| `0x40`      | All of enemy's party members    |
| `0xff`      | All combatants                  |
### Player's Party
The memory location that stores the target that the current party member chooses is located at `+0x138` from the party member's base address.
## Enemy's Party
First, the game generates three options for the enemy to pick and stores them in `0x801ff4f0` in the RAM.