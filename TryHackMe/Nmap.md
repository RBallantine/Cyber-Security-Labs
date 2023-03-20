# NMAP 
Used to obtain a "map" of the network structure, 
to see which IP addresses contain active hosts, and which do not.

### Open NMAP in the terminal using the command > nmap
![open_nmap](https://user-images.githubusercontent.com/84083756/225712433-49bbd2d1-62c2-4de8-984e-e29949242685.png)
---
## TCP Connect Scans ```-sT```
 - TCP Connect scan works by performing the three-way handshake with each target port in turn
 - If Nmap sends a TCP request with the SYN flag set to a closed port, the target server will respond with a TCP packet with the RST (Reset) flag set. 
 - By this response, Nmap can establish that the port is closed.
 - If the port is open, the target will respond with a TCP packet with the SYN/ACK flags set
---
## SYN Scans ```-sS```
- "Half-open" scans, or "Stealth" scans
- Often not logged by applications listening on open ports
- SYN scans are significantly faster than a standard TCP Connect scan
- If the port is closed then the server responds with a RST TCP packet
- If filtered by a firewall then the TCP SYN packet is either dropped, or spoofed with a TCP reset.
- Disadvantages
  - They require sudo permissions
  - Unstable services are sometimes brought down by SYN scans
---
## UDP Scans ```-sU```
- UDP connections are stateless
  - No handshake
  - UDP connections rely on sending packets to a target port and essentially hoping that they make it
- No server response indicates open|filtered port
- closed ports are indicated by an ICMP (ping) packet containing a message that the port is unreachable
- Slow scan
---
## NULL, FIN and Xmas Scans 
These three types of scans are similar and can only identify ports being open|filtered, closed, or filtered.
They are identified as filtered if the target resppnds with an ICMP unreachable packet.

### Null Scan ```-sN```
- TCP request sent with no flags set
- Target should respond with RST flag if the port is closed

### FIN Scan ```-sF```
- TCP request sent with only the FIN flag set (usually used to close an active connection)
- Target should respond with RST flag if the port is closed

### Xmas Scan ```-sX```
- Sends a malformed TCP packet
- Expects RST response for closed ports
- (PSH, URG and FIN flags look like blinking lights when viewed in Wireshark)

### <b>NOTE</b>: 
Microsoft Windows (and a lot of Cisco network devices) are known to respond with a RST to any malformed TCP packet -- regardless of whether the port is actually open or not. This results in all ports showing up as being closed.
---
## ICMP Network Scanning (Ping Sweep) ```-sn```
![ping_sweep](https://user-images.githubusercontent.com/84083756/225763558-2ff27605-5c2d-48d8-a5c1-a3f773576447.png)
- Sends an ICMP packet to every possible IP address for the specified network
- Responding IP addresses are marked as being alive
- Not always accurate but can provide a baseline
- Wont scan any ports
- Relies primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets. 
- Sends a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.
---
## NMAP Scripting Engine (```--script=vuln```, ```--script=safe```)
- LUA programming language
- Mulitple uses
  - Scan for Vuln
  - Automate exploits
Contains many categories including:
- <b>safe:</b> Won't affect the target
- <b>intrusive:</b> (Not safe) likely to affect the target
- <b>vuln:</b> Scan for vulnerabilities
- <b>exploit:</b> Attempt to exploit a vulnerability
- <b>auth:</b> Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
- <b>brute:</b> Attempt to bruteforce credentials for running services
- <b>discovery:</b> Attempt to query running services for further information about the network (e.g. query an SNMP server).

### Running Scripts
- To run a specific script: ```--script=<script-name>```
- To run multiple scripts separate using a comma: ```--script=smb-enum-users,smb-enum-shares```
- Script arguments are given using the ```--script-args``` switch:
  - ```nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'``` 
- A help function for each script can be found using the command: ```nmap --script-help <script-name>```

### Searching for Scripts
- A full list of scripts can be found [here](https://nmap.org/nsedoc/scripts/)
- Nmap stores its scripts on Linux at ```/usr/share/nmap/scripts```
- A text style data base is also stored at ```/usr/share/nmap/scripts/script.db```
  - Search using:
    -  ```grep``` e.g. ```grep "ftp" /usr/share/nmap/scripts/script.db```
    -  ```ls -l /usr/share/nmap/scripts/*ftp*```

### Updating Scripts
- Update Nmap: ```sudo apt update && sudo apt install nmap```
- Add specific scripts: ```sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse```
  - Followed by: ```nmap --script-updatedb```
  - Also use updatedb when creating your own scripts
---
## Firewall Evasion
- Typically Windows default firewall will block all ICMP packets
- Presents a problem when using PING to establish activity
- Use ```-Pn``` to prevent Nmap from pinging the host before scanning it. 
  - This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block
- Can potentially take a very long time to complete the scan (if the host really is dead then Nmap will still be checking and double checking every specified port

### Switches of note
- ```-f``` Used to fragment the packets, making it less likely that the packets will be detected by a firewall or IDS.
- ```--mtu <number>``` An alternative to ```-f```
  - More control over the size of the packets ```--mtu <number>``` 
  - Accepts a maximum transmission unit size to use for the packets sent. (Must be a multiple of 8)
- ```--scan-delay <time>ms``` Used to add a delay between packets sent. 
  - Useful if the network is unstable and also for evading any time-based firewall/IDS triggers which may be in place.
- ```--badsum``` Used to generate in invalid checksum for packets. 
  - Can be used to determine the presence of a firewall/IDS
- Other switches usefull for firewall evasion can be found [here](https://nmap.org/book/man-bypass-firewalls-ids.html)
