There are two inventories: 
* Active party inventory
	* Items
		* Starts at `0x8011ad98` in the RAM
		* Starts at `+0x5cc` in the save files
	* Weapons
		* Starts at `0x8011af98` in the RAM
		* Starts at `+0x7cc` in the save files
	* Armor
		* Starts at `0x8011b198` in the RAM
		* Starts at `+0x9cc` in the save files
	* Accessories
		* Starts at `0x8011b398` in the RAM
		* Starts at `+0xbcc` in the save files
	* Zenny
		* Can be found at `0x8011ad80` in the RAM
		* Can be found at
* Inactive party inventory
	* Items
		* Starts at `0x8011ae98` in the RAM
		* Starts at `+0x6cc` in the save files
	* Weapons
		* Starts at `0x8011b098` in the RAM
		* Starts at `+0x8cc` in the save files
	* Armor
		* Starts at `0x8011b298` in the RAM
		* Starts at `+0xacc` in the save files
	* Accessories
		* Starts at `0x8011b498` in the RAM
		* Starts at `+0xccc` in the save files
All of the tables above are 256 bytes in length and follow the same format:

| Position | Description                     | Value(s)               | Note                                                                                |
| -------- | ------------------------------- | ---------------------- | ----------------------------------------------------------------------------------- |
| 0        | Item ID (based on the category) | 8-bit unsigned integer |                                                                                     |
| 1        | Quantity                        | 8-bit unsigned integer | While you can put numbers larger than `0x63` (99) here, the game doesn't like that. |
#RAM #SaveFile 