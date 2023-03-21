# Nesus
---
## Installation Guide
1. Goto https://www.tenable.com/products/nessus/nessus-essentials and register an account.
2. Download the `Nessus-#.##.#-debian6_amd64.deb` file and save it to your `/Downloads/` folder
3. In the terminal navigate to that folder and run the following command:
    - `sudo dpkg -i package_file.deb` (Remember to replace package_file.deb with the file name you downloaded)
4. Start the Nessus Service `sudo /bin/systemctl start nessusd.service`
5. Open Firefox and goto https://localhost:8834/ 
    - You may be prompted with a security risk alert
    - Click Advanced... -> Accept the Risk and Continue
6. Set up the scanner - Select the option 'Nessus Essentials'
7. Click the Skip button, input the code we got in the email from Nessus
8. Fill out Username and Password
9. Nessus will now install the plugins required for it to function.
10. Log in
---
## Navigation and Scan Types
- launch a scan with `new scan` button
- creare custom templates using `policies`
- change plugin properties `plugin rules`
- see what hosts are alive with a `host discovery` scan
- a scan suitable for any host is a `basic network` scan
- Authenticate to hosts and enumerate missing updates with a `credential patch audit` scan
- `web applications tests` are specifically used for scanning Web Applications
---
## Scanning
- Use `schedule` to set a time for a scan to run
- `port scan (all ports)` covers ports 1-65535
- change to `scan low bandwidth links` scan type for lower bandwidth connection
