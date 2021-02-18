# Nessus

Learn how to set up and use Nessus, a popular vulnerability scanner.

## Navigation and Scans

    1. What is the name of the button which is used to launch a scan?
        a. New Scan
    2. What sude menu option allows us to create custom templates?
        a. Policies
    3. What menu allows us to change plugin properties such as hiding them or changing their severity?
        a. Plugin Rules
    4. In the ;Scan Templates' section after clicking 'New Scan', what scan allows us to see simply what hosts are alive?
        a. Host Discovery
    5. One of the most useful scan types, which is considered to be 'suitable for any host'?
        a. Basic Network Scan
    6. What scan allows you to 'Authenticate to hosts and enumerate missing updates'?
        a. Credentialed Patch Audit
    7. What scan is specifically used for scanning Web Applications?
        a. Web Application Tests

## Scanning

    1. Create a new 'Basic Network Scan' targeting the deployed VM. What option can we set under 'BASIC' (on the left) to set a time for this scan to run? This can be very useful when network congestion is an issue.
        a. Schedule
    2. Under 'DISCOVERY' (on the left) set the 'Scan Type' to cover ports 1-65535. What is this type called?
        a. Port scan (all ports)
    3. What 'Scan Type' can we change to under 'ADVANCED' for lower bandwidth connection?
        a. Scan low bandwidth links
    4. After the scan completes, which 'Vulnerability' in the 'Port scanners' family can we view the details of to see the open ports on this host?
        a. Nessus SYN Scanner
    5. What Apache HTTP Server Version is reported by Nessus?
        a. 2.4.99

## Scanning a Web Application!

    1. What is the plugin id of the plugin that determines the HTTP server type and version?
        a. 10107
    2. What authentication page is discovered by the scanner that transmits credentials in cleartext?
        a. login.php
    3. What is the file extension of the config backup?
        a. .bak
    4.  Which directory contains example documents? (This will be in a php directory)
        a. /external/phpids/0.6/docs/examples/
    5. What vulnerability is this application susceptible to that is associated with X-Frame-Options?
        a. clickjacking