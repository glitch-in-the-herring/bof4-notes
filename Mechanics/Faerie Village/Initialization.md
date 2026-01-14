After ... battles. ...
The game chooses the base stats of the faerie from the base stats table. The table is located at:
* `0x800ff024` in the RAM
* In the following files:
```
BIN/WORLD/AREAE024.EMI: 000a8824
BIN/WORLD/AREAE025.EMI: 000a9024
BIN/WORLD/AREAE026.EMI: 000a9024
BIN/WORLD/AREAE027.EMI: 000aa824
BIN/WORLD/AREAE028.EMI: 000ae824
BIN/WORLD/AREAS041.EMI: 00093024
BIN/WORLD/AREAS042.EMI: 00092824
```
Each entry is four bytes long and has the following structure:

| Position | Description    |
| -------- | -------------- |
| 0        | Probability    |
| 1        | Base Endurance |
| 2        | Base Knowledge |
| 3        | Base Style     |
The table entries are:

| Probability | Base Endurance | Base Knowledge | Base Style |
| ----------- | -------------- | -------------- | ---------- |
| 15%         | 150            | 0              | 0          |
| 15%         | 10             | 150            | 0          |
| 15%         | 10             | 0              | 150        |
| 15%         | 10             | 80             | 80         |
| 15%         | 80             | 80             | 0          |
| 15%         | 80             | 0              | 80         |
| 5%          | 10             | 0              | 0          |
| 5%          | 150            | 150            | 150        |
