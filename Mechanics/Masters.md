As you progress through the game you'll meet masters who grant you new abilities as you pass their increasingly difficult milestones.
## Ordering

| ID  | Name   |
| --- | ------ |
| 1   | Rwolf  |
| 2   | Momo   |
| 3   | Kryrik |
| 4   | Abbess |
| 5   | Njomo  |
| 6   | Gyosil |
| 7   | Stoll  |
| 8   | Una    |
| 9   | Bunyan |
| 10  | Lyta   |
| 11  | Kahn   |
| 12  | Marlok |
## Prerequisite
Masters need you to pass a prerequisite check before you can apprentice under them. 
### Lyta
Lyta checks if any member of your party is apprenticed under Gyosil. The code can be found at `BIN/WORLD/AREAS011.EMI: 000c6d28` in the game's files
```
801f0d28 li        $a1, 0x0006 ; load Gyosil's index
801f0d2c lui       $v0, 0x8012
801f0d30 addiu     $v1, $v0, -0x56b4
801f0d34 lbu       $v0, 0x0084(v1) ; load the character's current master
801f0d38 nop
801f0d3c bne       $v0, $a1, 0x801f0d4c ; check if they are the same
```

## Milestones
A master's milestones are stored in the AREA files where the master lives in
* `BIN/WORLD/AREAD086.EMI: 0009b9cc` contains Rwolf's milestones (5, 10, 15, 20)
* `BIN/WORLD/AREAS002.EMI: 00089160` contains Momo's milestones (25, 30, 40, 50)[^1]
* `BIN/WORLD/AREAM027.EMI: 000c097c` contains Kryrik's milestones (30, 40, 50, 70)
* `BIN/WORLD/AREAS036.EMI: 000c0ea4` contains the Abbess' milestones (70, 85, 100)
* `BIN/WORLD/AREAS055.EMI: 00097a9c` contains Njomo's milestones (8, 12, 16, 20)
* `BIN/WORLD/AREAM017.EMI: 000aa004` contains Gyosil's milestones (4000, 6000, 9500)
* `BIN/WORLD/AREAD114.EMI: 0009dc84` contains Stoll's milestones (80, 120)
* `BIN/WORLD/AREAS020.EMI: 0009e05c` contains Una's milestones (1500, 3000, 10000)
* `BIN/WORLD/AREAD116.EMI: 0009d804` contains Bunyan's milestones (3000, 5000, 8000, 12000)
* `BIN/WORLD/AREAS011.EMI: 000c7f8b` contains Lyta's milestones (20, 25, 30)
* `BIN/WORLD/AREAE075.EMI: 0009d158` contains Kahn's milestones (300, 400*, 500, 600)
	* Kahn doesn't have anything listed for the 400 encounters milestones, but it's there in the game data for some reason.
## Rewards
The rewards for all masters are stored in the AREA files where each master lives in. Yes, this game is redundant, if it's not clear at this point.
First, here is a list of the locations of the reward table:
* `BIN/WORLD/AREAD086.EMI: 0009cea8` is the location for the reward table in Rwolf's area
* `BIN/WORLD/AREAS002.EMI: 0008a6a8` is the location for the reward table in Momo's area
* `BIN/WORLD/AREAM027.EMI: 000c1ea8` is the location for the reward table in Kryrik's area
* `BIN/WORLD/AREAS036.EMI: 000c1ea8` is the location for the reward table in the Abbess's area
* `BIN/WORLD/AREAS055.EMI: 00098ea8` is the location for the reward table in Njomo's area
* `BIN/WORLD/AREAM017.EMI: 000abea8` is the location for the reward table in Gyosil's area
* `BIN/WORLD/AREAD114.EMI: 0009eea8` is the location for the reward table in Stoll's area
* `BIN/WORLD/AREAD116.EMI: 0009eea8` is the location for the reward table in Bunyan's area
* `BIN/WORLD/AREAS020.EMI: 0009f6a8` is the location for the reward table in Una's area
* `BIN/WORLD/AREAS011.EMI: 000c8ea8` is the location for the reward table in Marlok's and Lyta's area
* `BIN/WORLD/AREAE075.EMI: 0009e6a8` is the location for the reward table in Kahn's area
* `BIN/WORLD/AREAM019.EMI: 00085ea8` is the location for the reward table in [[AREAM019#Unused Textures|Noritake's Town]]
In the RAM this is always(?) found at `0x800f96a8`

Each master can have up to four rewards. Each reward is defined using two bytes. See [[Indexing]] for more information about how the entries work. After the entries for the four rewards follow a couple of addresses that I'm not sure the function of. In any case, the reward table for a single master is 24 bytes long.
## Text
Rather annoyingly, the game does not use dynamic text for master-related functions.
## Wills
See [[Wills]]

[^1]: Found by Tony H
