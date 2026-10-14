# Enumeration Tips and Tricks

## Initial Enumeration

* Start out performing light scans on your targets
  * Scan for 10 common ports
  * Manually interact with services found while waiting for thorough and longer scans

## Enumerate Carefully

* Avoid heavy (or aggressive) scans on multiple targets at once
* Revert machines after running unsafe scans
* Rerun scans to ensure all information is correct. _Scans can be inaccurate._
  * Use various tools to verify scan outputs.

## Enumeration is a Cyclical Approach

* After gaining initial access, enumerate again in the context of your new privileges.
  * If you gain login access to a webpage, enumerate the webapp as that user.
  * If you gain domain user access to a target machine, enumerate the domain as that user.
* This concept is often overlooked.
  * Individuals tent to stop enumerating after getting a shell or root access.

## Make Sure to Read Exploit Documentation Prior to Using Them

* Do you need to set up files or permissions prior to running the exploit?
* Do you need to modify the exploit to match your target?

## Check Multiple Exploits for the Same Vulnerability

* Exploits may use different methods to exploit vulnerabilities.
* Some exploits might be compatible or incompatible with your target.









