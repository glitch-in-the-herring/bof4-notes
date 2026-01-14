There are two inventories: 
* Ryu's inventory
	* Items
		* Starts at `0x8011ad98` in the RAM
		* Starts at 
	* Weapons
		* Starts at `0x8011af98` in the RAM
		* Starts at 
	* Armor
		* Starts at `0x8011b198` in the RAM
		* Starts at
	* Accessories
		* Starts at `0x8011b398` in the ram
		* Starts at
* Fou-lu's inventory
	* Items
		* Starts at `0x8011ae98` in the RAM
		* Starts at
	* Weapons
		* Starts at `0x8011b098` in the RAM
		* Starts at
	* Armor
		* Starts at `0x8011b298` in the RAM
		* Starts at
	* Accessories
		* Starts at `0x8011b498` in the RAM
		* Starts at
All of the tables above are 256 bytes in length and follow the same format:

| Position | Description                     | Value(s)               | Note                                                                                |
| -------- | ------------------------------- | ---------------------- | ----------------------------------------------------------------------------------- |
| 0        | Item ID (based on the category) | 8-bit unsigned integer |                                                                                     |
| 1        | Quantity                        | 8-bit unsigned integer | While you can put numbers larger than `0x63` (99) here, the game doesn't like that. |
#RAM #SaveFile 