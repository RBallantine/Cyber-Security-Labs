# Burp Suite
- Web application penetration testing
- Can capture and manipulate all of the traffic between an attacker and a webserver
---
## Features
- Proxy: Allows us to intercept and modify requests/responses when interacting with web applications
- Repeater: Allows us to capture, modify, then resend the same request numerous times
  - Can be used to craft a payload through trial and error (e.g. in an SQLi -- Structured Query Language Injection) or when testing the functionality of an endpoint for flaws
- Intruder: Allows us to spray an endpoint with requests. This is often used for bruteforce attacks or to fuzz endpoints
  - Rate limited in community version
- Decoder: Provides a valuable service when transforming data
  - Use for decoding captured information, or encoding a payload prior to sending it to the target
- Comparer: Allows us to compare two pieces of data at either word or byte level
- Sequencer: Used in assessing the randomness of tokens such as session cookie values or other supposedly random generated data. 
  - If the algorithm is not generating secure random values, then this could open up some devastating avenues for attack.

---
## Using Burp Suite
![image](https://user-images.githubusercontent.com/84083756/226112875-c221b493-1f14-455f-b763-8c39aac2473e.png)


### 1. Task Menu (1)
- Allows us to define background tasks that Burp Suite will run whilst we use the application

### 2. Event Log
- Information about what Burp Suite is doing (e.g. starting the Proxy), as well as information about any connections that we are making through Burp.

### 3. Issue Activity
- Exclusive to Burp Pro
- Would list all of the vulnerabilities found by the automated scanner

### 4. Advisory
- More information about the vulnerabilities found, as well as references and suggested remediations
---
## Shortcuts
- ```Ctrl + Shift + D``` Switch to the Dashboard
- ```Ctrl + Shift + T``` Switch to the Target tab
- ```Ctrl + Shift + P``` Switch to the Proxy tab
- ```Ctrl + Shift + I``` Switch to the Intruder tab
- ```Ctrl + Shift + R``` Switch to the Repeater tab


