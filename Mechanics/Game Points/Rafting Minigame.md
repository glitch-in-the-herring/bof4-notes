The rafting minigame can be played at Mt. Ryft. After going through the mountain (you need to start facing south when entering the area from the world map), you will reach a river. At this point, you can choose to play the minigame. Use the left and right d-pad buttons to move the raft. Try to collect as many bags as you can and avoid hitting the edges. If you hit the edge too many times, your raft breaks and you need to start over.
## Points
For replays after the first attempt, divide the game points by 10.
Points are acquired when you collect the bags. There are two types of bags:
* Small bags: There are 9 of these, each are worth 200 points
* Large bag: There is only one of this, it appears near the waterfall at the end. It is worth five bags, or 1000 points.
The number of bags you have acquired is tracked at `0x801f4433` in the RAM.
Additional points are awarded if you manage to get the raft back in one piece. For every hit to the edge the raft suffers, a piece of it falls off, up to seven. The number of pieces lost is tracked at `0x801f4435` in the RAM.
The bonus scales as follows:

| Pieces Lost | Bonus |
| ----------- | ----- |
| 0           | 2000  |
| 1           | 1000  |
| 2           | 800   |
| 3           | 600   |
| 4           | 400   |
| 5           | 200   |
| 6           | 0     |

The following code can be found at `BIN/WORLD/AREAD109.EMI: 000c8930`.
```
801f0930 lbu     $v1, 0x4435(v0) ; load the number of pieces lost
801f0934 li      $v0, 0x0001
801f0938 sw      $ra, 0x001c(sp)
801f093c sw      $s2, 0x0018(sp)
801f0940 sw      $s1, 0x0014(sp)
801f0944 bne     $v1, $v0, 0x801f0954 
801f0948 sw      $s0, 0x0010(sp)

; If the number of pieces lost is 1
801f094c j       0x801f09a4
801f0950 li      $s0, 0x03e8 ; Set the bonus to 1000

; If the number of pieces lost is not 1
801f0954 li      $v0, 0x0002
801f0958 bne     $v1, $v0, 0x801f0968
801f095c li      $v0, 0x0003

; If the number of pieces lost is 2
801f0960 j       0x801f09a4
801f0964 li      $s0, 0x0320 ; Set the bonus to 800

; If the number of pieces lost is not 2
801f0968 bne     $v1, $v0, 0x801f0978
801f096c li      $v0, 0x0004

; If the number of pieces lost is 3
801f0970 j       0x801f09a4
801f0974 li      $s0, 0x0258 ; Set the bonus to 600

; If the number of pieces lost is not 3
801f0978 bne     $v1, $v0, 0x801f0988
801f097c li      $v0, 0x0005

; If the number of pieces lost is 4
801f0980 j       0x801f09a4
801f0984 li      $s0, 0x0190 ; Set the bonus to 400

; If the number of pieces lost is not 4
801f0988 bne     $v1, $v0, 0x801f0998
801f098c li      $v0, 0x0006

; If the number of pieces lost is 5
801f0990 j       0x801f09a4
801f0994 li      $s0, 0x0c8 ; Set the bonus to 100

; If the number of pieces lost is not 5
801f0998 bne     $v1, $v0, 0x801f09a4

; If the number of pieces lost is 0
801f099c li      $s0, 0x07d0

; If the number of pieces lost is 6
801f09a0 move    $s0, $r0 ; Set the bonus to 0
```
The bonus is then converted to the equivalent amount in bags
```
801f09a4 lui     $v0, 0x51eb
801f09a8 ori     $v0, 0x851f
801f09ac mult    $s0, $v0 
801f09b0 lui     $a0, 0x8012
801f09b4 addiu   $a0, -0x47fc
801f09b8 li      $a1, 0x000c
801f09bc lui     $s1, 0x801f
801f09c0 lbu     $v0, 0x4433(s1) ; load the current number of bags
801f09c4 mfhi    $a2, $hi
801f09c8 sra     $v1, $a2, 0x06 ; divide the bonus by 200
801f09cc addu    $v0, $v1 ; add the bonus bags
801f09d0 jal     0x80191828
801f09d4 sb      $v0, 0x4433(s1) ; store the new amount of bags
```