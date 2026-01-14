There are a lot of resources that explain this more accurately than I can, but what you need to know is that a CD-ROM is divided into sectors, each containing up to 2,048 bytes of data. All of the game's data is padded up to the greatest multiple of 2,048 to make sure that they align with the sector's start and end.

## File table
To keep track of where each file is located on the CD, the game keeps track of the starting sector of files at:
* `SLUS_013.24: 0007AC10` in the game's files
* `0x80172c10` in the RAM

## Pointing to a file
In order to locate a file, the starting sector needs to be converted into HMS (hour, minute, second) format. The result of the conversion is stored at 