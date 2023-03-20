# Metasploit
---
## Main Components
Modules can be found in ```/opt/metasploit-framework/embedded/framework/modules```

### Auxilary
- Scanners, crawlers and fuzzers

### Encoders
- Allows you to encode the payload or exploit
- Can aid in avoiding AV signature-based detections
- limited success

### Evasion
- Unlike encoders, these modules actually try to evade AV detection

### Exploits
- Common exploits for vulnerabilities

### NOPs (No Operation)
- CPU will do nothing for one cycle
- Can be used as a buffer to acheive consistent payload sizes

### Payloads
- Code to run on the target system
- Example include:
  - getting a shell 
  - loading a malware or backdoor to the target system 
  - running a command 
  - launching calc.exe as a proof of concept to add to the penetration test report

- Contains 4 different directories  
  - Adapters: 
    - Wraps single payloads to convert them into different formats. 
    - e.g. a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.
  - Singles: Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
  - Stagers: Responsible for setting up a connection channel between Metasploit and the target system. 
    - Useful when working with staged payloads. 
    - “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). 
    - This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
  - Stages: Downloaded by the stager. This will allow you to use larger sized payloads.

- Identify Single or Stages payloads in naming convention:
  - generic/shell_reverse_tcp (inline (or single) payload, indicated by the “_” between “shell” and “reverse”) 
  - windows/x64/shell/reverse_tcp (staged payload, indicated by the “/” between “shell” and “reverse”)

### Post
- Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation.

---
## Msfconsole
- To run metasploit in the command line use ```msfconsole```
- External Blue Example
  - ```set rhosts [IP Address]```
  - ```use exploit/windows/smb/ms17_010_eternalblue```
  - use ```show options``` to view required parameters
  - the ```show``` command can be used with any of the module types, e.g. ```show payloads```
  - ```info exploit/windows/smb/ms17_010_eternalblue``` can also be used to view more information
  - use the ```search``` command to search for CVEs for example
