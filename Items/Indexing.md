When referring to items, the game will sometimes use two bytes to index it. The category byte describes the item type:

| Byte | Type        |
| ---- | ----------- |
| 0    | Items       |
| 1    | Weapons     |
| 2    | Armor       |
| 3    | Accessories |
| 4    | Spells      |
Then the item's actual ID follows.