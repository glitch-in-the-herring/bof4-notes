Super Combo shows a sequence of buttons that the player must press successfully in order to increase the combo counter. Once the player hits the wrong button, then the sequence ends and the attack is dealt to the target. In Breath of Fire IV, a string is also displayed as a sort of name for the combo.
The current active button is stored at `0x801c892c` in the RAM. The button IDs are:

| ID  | Button   |
| --- | -------- |
| 0   | Circle   |
| 1   | Cross    |
| 2   | Triangle |
| 3   | Square   |
The game first stores the possible button IDs that can be displayed. At the start, it chooses from IDs 0 to 3:
```
801e91f0 jal    0x8016f384 ; call random number function
801e91f4 sw     $v0, 0x009c(v1)
8016f384 li     $t2, 0x00a0
8016f388 jr     $t2
8016f38c li     $t1, 0x002f
...
801e91f8 lbu    $v1, 0x0005(s0)
801e91fc andi   $v0, 0x0003 ; get a random number from 0 to 3
801e9200 sb     $v0, 0x0008(s0) ; store initial button ID
```
This code can be found at `BIN/BMAGIC/MAGIC088.EMI: 0000b9f0`

The game never shows the same button consecutively:
```
801e9338 lb     $v0, 0x0008(s1) ; load last active button ID
801e933c nop    
801e9340 beq    $v0, $v1, 0x801e9350
801e9344 addu   $v0, $a0, $s0

; if the current button ID is the same as the last button ID
801e9350 addiu  $v1, 0x0001 ; skip by 1 and go back to the start

; if the current button ID is not the same as the last button ID
801e9348 sb     $v1, 0x0000(v0) ; store current button ID
801e934c addiu  $s0, 0x0001
801e9350 addiu  $v1, 0x0001 ; increment button ID by 1
801e9354 slti   $v0, $v1, 0x0004
801e9358 bnez   $v0, 0x801e9338
801e935c nop
```
If the player presses the button correctly, the game rolls a random number from 0 to 2 to decide which button ID to pick, and then increments the combo counter. The combo counter is located at `0x801ea490`. At the same time, it also appends a `0x01` to an array of bytes starting at `0x801ea440`.
```
801e92c0 lbu    $v1, -0x5b70(a1) ; load current combo count
801e92c4 addiu  $a0, $v0, -0x5bc0
801e92c8 addu   $v1, $a0
801e92cc lbu    $v0, 0x0000(v1) ; load current array position
801e92d0 nop    
801e92d4 addiu  $v0, 0x0001 ; add 1
801e92d8 sb     $v0, 0x0000(v1) ; store new array item
...
801e9360 jal    0x8016f384 ; call random number function
801e9364 nop    
8016f384 li     $t2, 0x00a0
8016f388 jr     $t2
8016f38c li     $t1, 0x002f
...
801e9368 div    $v0, $s0
801e936c bnez   $s0, 0x801e9378
801e9370 nop    
801e9378 li     $at, -0x0001
801e937c bne    $s0, $at, 0x801e9390
801e9380 lui    $at, 0x8000
801e9390 mfhi   $v1, $hi ; get random number from 0 to 2
801e9394 nop    
801e9398 addu   $v0, $sp, $v1
801e939c lbu    $v0, 0x0020(v0) ; get button ID
801e93a0 lui    $v1, 0x801f
801e93a4 sb     $v0, 0x0008(s1) ; store button ID
801e93a8 lbu    $v0, -0x5b70(v1) ; load current combo counter
801e93ac nop    
801e93b0 addiu  $v0, 0x0001 ; increment combo counter
801e93b4 sb     $v0, -0x5b70(v1) ; store incremented combo counter
```
The timer is stored at `0x801c8972`. It starts at 112 and decrements every three frames:
```
801e9048 li     $v0, 0x0038 ; load 56
801e90a8 sb     $v0, 0x004e(s1) ; store 56
801e90ac move   $a0, $r0
801e90b0 lui    $v1, 0x801f
801e90b4 lbu    $v0, 0x004e(s1) 
801e90b8 addiu  $v1, -0x5bc0
801e90bc sll    $v0, 0x01 ; multiply 56 by 2
801e90c0 sb     $v0, 0x004e(s1) ; store initial timer value (112)
...
801e93e4 lbu    $v0, 0x004e(s1) ; load timer
801e93e8 nop    
801e93ec addiu  $v0, -0x0001 ; decrement
801e93f0 sb     $v0, 0x004e(s1) ; store new timer
```
Unlike in Breath of Fire III, the timer is never reset, and there is no acceleration between each button in the sequence, they are only changed as fast as the player can press the buttons.
Once the sequence is ended, the game gives a name to the combo using this algorithm:
