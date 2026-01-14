The equipability byte determines who can use a piece of equipment. It is a bit switch:

| Bit    | User   |
| ------ | ------ |
| `0x01` | Ryu    |
| `0x02` | Nina   |
| `0x04` | Cray   |
| `0x08` | Scias  |
| `0x10` | Ursula |
| `0x20` | Ershin |
| `0x40` | Fou-Lu |
For example, a weapon that only Nina and Ursula can use is indicated by `0x12`.