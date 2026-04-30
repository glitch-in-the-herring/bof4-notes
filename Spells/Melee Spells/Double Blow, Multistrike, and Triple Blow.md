Double Blow:

| Spell ID      | Targeting                                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ----------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x7c`<br>124 | Weapon-dependent<br>Player or enemy party | Yes<br>3  | 0     | 3   | Normal  | Melee     |
Multistrike:

| Spell ID      | Targeting                                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ----------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x7d`<br>125 | Weapon-dependent<br>Player or enemy party | Yes<br>6  | 0     | 5   | Normal  | Melee     |
Triple Blow:

| Spell ID      | Targeting                                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ----------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x7e`<br>126 | Weapon-dependent<br>Player or enemy party | Yes<br>3  | 0     | 8   | Normal  | Melee     |
Double Blow, MultiStrike, and Triple Blow inflict extra physical hits when used. They share the same code:
```
801e9178 lhu    $v1, -0x1f3e(v0) ; load current spell's ID
801e917c li     $v0, 0x007d
801e9180 beq    $v1, $v0, 0x801e91d0
801e9184 slti   $v0, $v1, 0x007e
    ; if the current spell is Multistrike
    801e91d0 lui    $v0, 0x801c
    801e91d4 li     $v1, 0x000c
    801e91d8 addiu  $s0, $v0, 0x6830
    801e91dc jal    0x8016f384 ; call random()
    801e91e0 sb     $v1, 0x6830(v0) ; set a flag?
    ...
    801e91e4 andi   $v0, 0x0003 ; get a random number from 0 to 3
    801e91e8 bnez   $v0, 0x801e9210
        ; if the random number is greater than zero
        801e91ec sb     $v0, 0x0001(s0) ; store hit count

        ; if the random number is zero
        801e91f0 li     $v0, 0x0002 ; load 2
        801e91f4 j      0x801e9210
        801e91f8 sb     $v0, 0x0001(s0) ; store 2 as the hit count

801e9188 beqz   $v0, 0x801e91a0
801e918c li     $v0, 0x007c
801e91a0 li     $v0, 0x007e
801e91a4 beq    $v1, $v0, 0x801e91fc
801e91a8 lui    $v0, 0x801c
    ; if the current spell is Triple Blow
    801e91fc li     $v1, 0x0008
    801e9200 sb     $v1, 0x6830(v0) ; set a flag?
    801e9204 addiu  $v0, 0x6830
    801e9208 li     $v1, 0x0003
    801e920c sb     $v1, 0x0001(v0) ; set the number of hits to 3

801e9188 beqz   $v0, 0x801e91a0
801e918c li     $v0, 0x007c
801e9190 beq    $v1, $v0, 0x801e91bc
801e9194 lui    $v0, 0x801c
    ; if the current spell is double Blow
    801e91bc li     $v1, 0x0008
    801e91c0 sb     $v1, 0x6830(v0) ; set a flag?
    801e91c4 addiu  $v0, 0x6830
    801e91c8 j      0x801e920c
    801e91cc li     $v1, 0x0002
    801e920c sb     $v1, 0x0001(v0) ; set the number of hits to 2
...
801e693c lbu    $a0, 0x011c(s0) ; load current weapon's ID
801e6940 addiu  $v1, -0x5eac
801e6944 sll    $v0, $a0, 0x03
801e6948 subu   $v0, $a0
801e694c sll    $v0, 0x01
801e6950 addu   $v0, $v1
801e6954 lbu    $v1, 0x0001(a1) ; load current hit count
801e6958 lbu    $v0, 0x0007(v0) ; load current weapon's hits and shield damage
801e695c addiu  $v1, 0x00ff ; subtract current hit by 1
801e6960 srl    $v0, 0x04 ; get just the weapon's hits
801e6964 addu   $v1, $v0 ; add the weapon's hits to the current hit count - 1
801e6968 sb     $v1, 0x0001(a1) ; store new hit count
```
Which can be found at `BIN/BMAGIC/MAGIC084.EMI: 00003178`
Each hit has less damage than a regular physical attack. The multipliers are:
* Double Blow:
```
801db288 lui    $a1, 0x51eb
801db28c lui    $v1, 0x8012
801db290 addiu  $v1, -0x1f40
801db294 lhu    $a0, 0x001e(v1) ; load current effective PWR
801db298 ori    $a1, 0x851f
801db29c sll    $v0, $a0, 0x02 ; multiply current effective PWR by 4
801db2a0 addu   $v0, $a0 ; multiply current effective PWR by 5
801db2a4 sll    $v0, 0x04 ; multiply current effective PWR by 80
801db2a8 mult   $v0, $a1
801db2ac mfhi   $t1, $hi
801db2b0 sra    $v0, $t1, 0x05 ; multiply current effective PWR by 80%
801db2b4 j      0x801db41c
801db2b8 sh     $v0, 0x001e(v1) ; store as new effective PWR
```
Can be found at `BIN/BATTLE/BTLMOVE.EMI: 00013288`
* Multistrike:
```
801db2bc lui    $a1, 0x51eb
801db2c0 lui    $a0, 0x8012
801db2c4 addiu  $a0, -0x1f40
801db2c8 lhu    $v1, 0x001e(a0) ; load current effective PWR
801db2cc ori    $a1, 0x851f
801db2d0 sll    $v0, $v1, 0x03 ; multiply current effective PWR by 8
801db2d4 addu   $v0, $v1 ; multiply current effective PWR by 9
801db2d8 sll    $v0, 0x02 ; multiply current effective PWR by 36
801db2dc subu   $v0, $v1 ; multiply current effective PWR by 35
801db2e0 j      0x801db34c
801db2e4 sll    $v0, 0x01 ; multiply current effective PWR by 70
801db34c mult   $v0, $a1
801db350 sra    $v0, 0x1f
801db354 mfhi   $t1, $hi
801db358 sra    $v1, $t1, 0x05 ; multiply current effective PWR by 70%
801db35c subu   $v1, $v0
801db360 j      0x801db41c
801db364 sh     $v1, 0x001e(a0) ; store as new effective PWR
```
Can be found at `BIN/BATTLE/BTLMOVE.EMI: 000132bc`
* Triple Blow:
```
801db1a4 nop    
801db2e8 lui    $a1, 0x51eb
801db2ec lui    $a0, 0x8012
801db2f0 addiu  $a0, -0x1f40
801db2f4 lhu    $v1, 0x001e(a0) ; load current effective PWR
801db2f8 ori    $a1, 0x851f
801db2fc sll    $v0, $v1, 0x04 ; multiply current effective PWR by 16
801db300 subu   $v0, $v1 ; multiply current effective PWR by 15
801db304 j      0x801db34c
801db308 sll    $v0, 0x02 ; multiply current effective PWR by 60
801db34c mult   $v0, $a1
801db350 sra    $v0, 0x1f
801db354 mfhi   $t1, $hi
801db358 sra    $v1, $t1, 0x05 ; multiply current effective PWR by 60%
801db35c subu   $v1, $v0
801db360 j      0x801db41c
801db364 sh     $v1, 0x001e(a0) ; store new effective PWR
```
Can be found at `BIN/BATTLE/BTLMOVE.EMI: 000131a4`