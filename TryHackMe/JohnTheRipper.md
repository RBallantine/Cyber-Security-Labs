# John The Ripper
---
- install in linux using `sudo apt install john`

For a collection of wordlists visit [SecLists](https://github.com/danielmiessler/SecLists)

## Basic Syntax
- `john [options] [path to file containing the hash]`
  - e.g. `john --wordlist=rockyou.txt rsa_id`
---
## Identifying Hashes
- John generally automatically detects the type of hash used
- When it can't use [hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master)
  - The file can be pulled using `wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py`
  - Launch it using `python3 hash-id.py`
- After identifying the hash type, provide the format to John
  - e.g. `john --format=raw-md5 --wordlist=rockyou.txt hash_to_crack.txt`
- Different hash format inputs include:
  - raw-md5
  - Raw-Sha1
  - Raw-sha256
  - whirlpool
  - nt (Windows Authentication Hash)
---
## /etc/shadow
- Location where password hashes are stored
- Only accessible by the root-user
- Needs to be combined with `/etc/passwd` file to crack (unshadowing)
  - `unshadow [path to passwd] [path to shadow]`
  - e.g. `unshadow local_passwd local_shadow > unshadowed.txt`
- The hash can now be cracked (may need to specify format)
  - `john --wordlist=rockyou.txt --format=sha512crypt unshadowed.txt`
---
## Single Crack Mode
- Only the information provided in the username is used to try and work out possible passwords heuristically, by slightly changing the letters and numbers contained within the username.

### Word Mangling
- Take the username: Markus
- Some possible passwords could be:
  - Markus1, Markus2, Markus3 (etc.)
  - MArkus, MARkus, MARKus (etc.)
  - Markus!, Markus$, Markus* (etc.)

### Usage
- `john --single --format=[format] [path to file]`
 - E.g. `john --single --format=raw-sha256 hashes.txt`
- File format must be changed when cracking hashes in single crack mode
- Done by prepending the hash with the username it belongs to
  - E.g. `1efee03cdcb96d90ad48ccc7b8666033` would change to `mike:1efee03cdcb96d90ad48ccc7b8666033`
---
## Custom Rules

