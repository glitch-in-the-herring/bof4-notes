| Accessory ID | Equipped By | Weight | Defense        |
| ------------ | ----------- | ------ | -------------- |
| `0x55`<br>85 | All         | 0      | 0<br>See below |
The medallion is an accessory that initially gives +3 ATK and -3 DEF to the wearer, if the wearer is the only one using it. The effect is multiplied for every other character using it, and when everyone in the party is wearing it, the negative defense modifier becomes positive.
Note that the requirement is *everyone*, not *six people*. This means that Fou-lu wearing it alone is gives +3 ATK and +3 DEF. In a party of only Ryu, Nina, and Ershin, if everyone is wearing a medallion, then each party member gets +9 ATK and +9 DEF.

The number of characters that are currently wearing the medallion is tracked at `0x8011a910` in the RAM. If everyone is wearing it, then it becomes `0xff`. The byte next to it, `0x8011a911` is the number of currently active party members.

The code can be found at `BIN/SYSTEM/GAME.EMI: 000093d8`

```
801963d8 lbu    $v1, -0x56f0(a0) ; load the number of characters wearing the medallion
801963dc li     $v0, 0x00ff
801963e0 beq    $v1, $v0, 0x80196408
801963e4 move   $v0, $v1
	; If there are characters
	801963e8 sll    $a0, $v0, 0x01 ; multiply the number of characters wearing the medallion by 2
	801963ec addu   $a0, $v0 ; multiply the number of characters wearing the medallion by 3
	801963f0 lhu    $v0, 0x0042(s0) ; load the character's power
	801963f4 lhu    $v1, 0x0044(s0) ; load the character's defense
	801963f8 addu   $v0, $a0 ; add 3*characters wearing the medallion to the power
	801963fc subu   $v1, $a0 ; subtract  3*characters wearing the medallion from the power
	80196400 j      0x8019645c
	80196404 sh     $v0, 0x0042(s0) ; store the character's power
	8019645c sh     $v1, 0x0044(s0) ; store the character's defense. Note that this is shared with the other accessories

	; If everyone in the party is wearing the accessory
    80196408 lui     $v0, 0x8012
    8019640c lbu     $v0, -0x56ef(v0) ; load the maximum number of party members currently possible (i.e. party member count)
    80196410 lhu     $v1, 0x0044(s0) ; load the character's defense
    80196414 sll     $a0, $v0, 0x01 ; multiply the party member count by 2
    80196418 addu    $a0, $v0 ; multiply the party member count by 3
    8019641c lhu     $v0, 0x0042(s0) ; load the character's power
    80196420 addu    $v1, $a0 ; add 3*party member count to the defense
    80196424 sh      $v1, 0x0044(s0) ; store the character's defense.
    80196428 addu    $v0, $a0 ; add 3*party member count to the power
    8019642c j       0x80196460
    80196430 sh      $v0, 0x0042(s0) ; store the character's power.
```