Some spells (notably breath attacks) can deal multiple, but distributed hits. This means that the spell calls the appropriate damage function a fixed number of times, no matter how many targets there are. For example, Primus' hit count is 8 normally. That means in a party that consists of...
* A single enemy, then that enemy receives eight hits
* Two enemies, then each enemy receives four
* Six enemies, then the first two enemies receive two hits, while the remaining four receive one.
If the spell can hit more than once, then the hit count is stored at `0x8011e0b9` in the RAM. If the spell cannot deal multiple hits, changing this value has no effect.