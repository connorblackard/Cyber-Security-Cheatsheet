## Hashcat
### Brute Force Attack
- `hashcat -a 3 -m 100 hashes.txt ?a?a?a?a?a?a?d`

### Wordlist/Dictionary Attack
- `hashcat -m 100 -a 0 hashes.txt wordlist.txt`

### Find hash types
- `hashcat --help | grep <hash_name>`

### Attack Modes
- **Dictionary:** 0 
- **Combination:** 1
- **Brute Force:**  3
- **Hybrid Wordlist:** 6
- **Hybrid Mask**: 7

### Character Sets 
- ?! - a-z
- ?u - A-Z
- ?d - 0-9
- ?s - Punctuation
- ?a - lower, upper, digit, punctuation

*** 
[Return to home page](../README.md)