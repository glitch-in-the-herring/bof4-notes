This section is based on ioev's work on hacking the game's button configuration. His hack can be found [here](https://www.romhacking.net/hacks/7843/). This section is also partly contributed by Naro.
## Main Configuration
The table that controls which face button does what function can be found at these locations:
```
BIN/SYSTEM/CAMP.EMI: 00037463
BIN/SYSTEM/COMMU01.EMI: 00021c63
BIN/SYSTEM/COMMU02.EMI: 00018c63
BIN/SYSTEM/COMMU03.EMI: 00033463
BIN/SYSTEM/COMMU04.EMI: 00019463
BIN/SYSTEM/COMMU05.EMI: 00019463
BIN/SYSTEM/COMMU06.EMI: 00039c63
BIN/SYSTEM/COMMU07.EMI: 00035463
BIN/SYSTEM/COMMU08.EMI: 0002a463
BIN/SYSTEM/COMMU09A.EMI: 00039463
BIN/SYSTEM/COMMU09B.EMI: 00037463
BIN/SYSTEM/COMMU09C.EMI: 0003d463
BIN/SYSTEM/GAME.EMI: 00022497
BIN/SYSTEM/LOT_SHOP.EMI: 0001d463
BIN/SYSTEM/MASTER.EMI: 00035463
BIN/SYSTEM/MSHOP.EMI: 00031463
BIN/SYSTEM/SAVE.EMI: 00033c63
BIN/SYSTEM/SGAMEN.EMI: 00041463
BIN/SYSTEM/SHOP.EMI: 00034c63
BIN/WORLD/AREAD075.EMI: 000fc463
BIN/WORLD/AREAE000.EMI: 000f9463
BIN/WORLD/AREAE003.EMI: 000f9463
BIN/WORLD/AREAE004.EMI: 000f9463
BIN/WORLD/AREAE006.EMI: 000fa463
BIN/WORLD/AREAE013.EMI: 000fa463
BIN/WORLD/AREAE014.EMI: 000fa463
BIN/WORLD/AREAE019.EMI: 000fec63
BIN/WORLD/AREAE021.EMI: 000fec63
BIN/WORLD/AREAE022.EMI: 00100463
BIN/WORLD/AREAE041.EMI: 000fbc63
BIN/WORLD/AREAE049.EMI: 000f9c63
```
The table contains four entries. Each entry represents one layout scheme and is 18 bytes long. Each entry contains the button mapping. Each button is two bytes long:

| Bytes  | Button   |
| ------ | -------- |
| 0x0080 | Square   |
| 0x0040 | X        |
| 0x0020 | O        |
| 0x0010 | Triangle |
## Button Settings Layout
The layout for the button settings can be found at:
* `0x801b5310` in the RAM
* In the game files at:
```
BIN/SYSTEM/GAME.EMI: 00020310
BIN/SYSTEM/SGAMEN.EMI: 0003ef9c
BIN/WORLD/AREAD075.EMI: 000f9e20
BIN/WORLD/AREAE000.EMI: 000f6e20
BIN/WORLD/AREAE003.EMI: 000f6e20
BIN/WORLD/AREAE004.EMI: 000f6e20
BIN/WORLD/AREAE006.EMI: 000f7e20
BIN/WORLD/AREAE013.EMI: 000f7e20
BIN/WORLD/AREAE014.EMI: 000f7e20
BIN/WORLD/AREAE019.EMI: 000fc620
BIN/WORLD/AREAE021.EMI: 000fc620
BIN/WORLD/AREAE022.EMI: 000fde20
BIN/WORLD/AREAE041.EMI: 000f9620
BIN/WORLD/AREAE049.EMI: 000f7620
```
There are 14 text entries and 5 underline entries. The text entries are two bytes long, the first byte being the x value of the text's position and the second being the y value of the text's position:

| No. | Entry              |
| --- | ------------------ |
| 1   | Camera             |
| 2   | Change Rank        |
| 3   | /Cancel            |
| 4   | Subscrn            |
| 5   | Action             |
| 6   | Talk/Confirm       |
| 7   | Dash               |
| 8   | START button Pause |
| 9   | Select Button Help |
| 10  | (Circle)           |
| 11  | (Square)           |
| 12  | (Triangle)         |
| 13  | (Cross)            |
| 14  |                    |
The underline entries are three bytes long, the first two bytes being the xy-coordinates of the underline's start and the third byte being the underline's length:

| No. | Entry                              |
| --- | ---------------------------------- |
| 15  | Underline under Change Rank        |
| 16  | Underline under Action/Cancel      |
| 17  | Underline under Subscrn            |
| 18  | Underline under Dash               |
| 19  | Underline under START button Pause |
## Button Functions
* The button that is used to toggle between the characters' stats in the item/equipment menu can be found at
	* `0x801b31dc` in the RAM
	* `BIN/SYSTEM/SGAMEN.EMI: 000389DC` in the game's files
* The button that is used to toggle between the character's stats in the stats menu can be found at
	* `0x801aa4e8` in the RAM
	* `BIN/SYSTEM/SGAMEN.EMI: 0002FCE8` in the game's files
* The button that is used to move forward the cursor in the name entry screen can be found at:
	* `0x801b4684` in the RAM
	* `BIN/SYSTEM/GAME.EMI: 0001F684` in the game's files