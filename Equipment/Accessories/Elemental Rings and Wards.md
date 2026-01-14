For convenience, all elemental rings and wards are grouped here
## Rings
All rings set their respective elemental resistances to 7. The code for rings can be found starting at `BIN/SYSTEM/GAME.EMI: 00006d7c`
### Ring of Fire
The ring of fire sets the user's fire resistance to 7.
```
80193d7c li      $v0, 0x0007 ; load 7 to $v0
80193d80 j       0x80193f0c
80193d84 sb      $v0, 0x004e(s0) ; store 7 as the fire resistance
```
### Ring of Wind
The ring of fire sets the user's wind resistance to 7
```
80193d88 li      $v0, 0x0007 ; load 7 to $v0
80193d8c j       0x80193f0c
80193d90 sb      $v0, 0x004f(s0) ; store 7 as the wind resistance
```
### Ring of Ice
The ring of fire sets the user's water resistance to 7
```
80193d94 li      $v0, 0x0007 ; load 7 to $v0
80193d98 j       0x80193f0c
80193d9c sb      $v0, 0x0050(s0) ; store 7 as the water resistance
```
### Ring of Clay
The ring of fire sets the user's earth resistance to 7
```
80193da0 li      $v0, 0x0007 ; load 7 to $v0
80193da4 j       0x80193f0c
80193da8 sb      $v0, 0x0051(s0) ; store 7 as the earth resistance
```
## Wards
All wards increase the user's elemental resistance by +2, up to a maximum of 6. The following code is used to check for the user's elemental resistance:
```
801946e8 lbu     $v1, 0x0000(a1) ; load the user's elemental resistance to $v1
801946ec li      $v0, 0x0007 ; load 7 to v0
801946f0 beq     $v1, $v0, 0x8019472c ; do nothing if the user's elemental resistance is already 7
801946f4 move    $a2, $v1 ; load the user's resistance to $a2
801946f8 sll     $v0, $a0, 0x18
801946fc sra     $v0, 0x18
80194700 addu    $v1, $a2, $v0 ; add 2 (stored in $v0) to the user's elemental resistance
80194704 slti    $v0, $v1, 0x0007 
80194708 bne     $v0, $r0, 0x80194718 ; make sure that it is less than 7

; If the elemental resistance is not less than 7
	8019470c li      $v0, 0x0006  ; cap the elemental resistance to 6

; If the elemental resistance is less than 7
	80194718 bgez    $v1, 0x80194728
	8019471c addu    $v0, $a2, $a0 ; add 2 to the user's elemental resistance
	80194728 sb      $v0, 0x0000(a1)
```
Found at `BIN/SYSTEM/GAME.EMI: 000076e8`
### Fire Ward
```
80193e40 li      $a0, 0x0002 ; load 2 to $a0
80193e44 jal     0x801946e8 ; jumps to check
80193e48 addiu   $a1, $s0, 0x004e ; loads the address of the user's fire resistance to $a1
...
80193e4c j       0x80193f0c
80193e50 nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006e40`
### Wind Ward
```
80193e54 li      $a0, 0x0002 ; load 2 to $a0
80193e58 jal     0x801946e8 ; jumps to check
80193e5c addiu   $a1, $s0, 0x004f ; loads the address of the user's wind resistance to $a1
...
80193e60 j       0x80193f0c
80193e64 nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006e54`
### Water Ward
```
80193e68 li      $a0, 0x0002 ; load 2 to $a0
80193e6c jal     0x801946e8 ; jumps to check
80193e70 addiu   $a1, $s0, 0x0050 ; loads the address of the user's water resistance to $a1
...
80193e74 j       0x80193f0c
80193e78 nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006e68`
### Earth Ward
```
80193e7c li      $a0, 0x0002 ; load 2 to $a0
80193e80 jal     0x801946e8 ; jumps to check
80193e84 addiu   $a1, $s0, 0x0051 ; loads the address of the user's earth resistance to $a1
...
80193e88 j       0x80193f0c
80193e8c nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006e7c`
### Astral Ward
```
80193e90 li      $a0, 0x0002 ; load 2 to $a0
80193e94 jal     0x801946e8 ; jumps to check
80193e98 addiu   $a1, $s0, 0x004c ; loads the address of the user's magic resistance to $a1
...
80193e9c li      $a0, -0x0001 ; load -1 to $a0
80193ea0 jal     0x801946e8 ; jumps to check
80193ea4 addiu   $a1, $s0, 0x004a ; loads the address of the user's melee resistance to $a1
...
80193ea8 li      $a0, -0x0001 ; load -1 to $a0
80193eac jal     0x801946e8 ; jumps to check
80193eb0 addiu   $a1, $s0, 0x004b ; loads the address of the user's ranged resistance to $a1
...
80193eb4 j       0x80193f0c
80193eb8 nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006e90`
### Body Ward
```
80193ebc li      $a0, 0x0002 ; load 2 to $a0
80193ec0 jal     0x801946e8 ; jumps to check
80193ec4 addiu   $a1, $s0, 0x004a ; loads the address of the user's melee resistance to $a1
...
80193ec8 li      $a0, 0x0002 ; load 2 to $a0
80193ecc jal     0x801946e8 ; jumps to check
80193ed0 addiu   $a1, $s0, 0x004b ; loads the address of the user's ranged resistance to $a1
...
80193ed4 li      $a0, -0x0001 ; load -1 to $a0
80193ed8 jal     0x801946e8 ; jumps to check
80193edc addiu   $a1, $s0, 0x004c ; loads the address of the user's magic resistance to $a1
...
80193ee0 j       0x80193f0c
80193ee4 nop
```
Found at `BIN/SYSTEM/GAME.EMI: 00006ebc`