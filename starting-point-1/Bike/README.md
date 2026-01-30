# Hack The Box – Bike (Starting Point)

## Overview

**Bike** is a Hack The Box *Starting Point* machine focused on web application enumeration and exploitation in a **Node.js** environment.  
The lab introduces concepts such as **service discovery**, **web fingerprinting**, **Server-Side Template Injection (SSTI)**, **encoding payloads**, and **command execution** in a modern JavaScript stack.

The objective is to identify exposed services, analyze the web application, detect an SSTI vulnerability, and leverage it to achieve **remote command execution as root**.

---

## Machine Information

- **Difficulty:** Starting Point  
- **Category:** Web / Linux  
- **Platform:** Hack The Box  
- **Key Skills:**  
  - Nmap enumeration  
  - Web fingerprinting (Wappalyzer)  
  - Node.js & Express analysis  
  - Server-Side Template Injection (SSTI)  
  - Payload encoding  
  - Command execution  

---

## Initial Enumeration

A TCP scan using **nmap** identifies two open ports on the target:

- **22** – SSH  
- **80** – HTTP  

The primary attack surface is the web service running on port **80**.

---

## Web Application Analysis

Visiting the web application reveals a Node.js-powered site.

Using **Wappalyzer**, the following technologies are identified:

- **Web Server Runtime:** Node.js  
- **Web Framework:** Express  
- **Template Engine:** Handlebars  

This combination suggests potential template-related attack vectors.

---

## Vulnerability Discovery – SSTI

User input is reflected in the web application without proper sanitization.

Submitting the payload: {{7*}}


results in evaluated output rather than literal text, confirming a **Server-Side Template Injection (SSTI)** vulnerability.

---

## Payload Crafting & Encoding

Because special characters are restricted in HTTP requests, payloads must be encoded.

Key tooling and concepts used:

- **Burp Suite → Decoder** (to encode payloads)
- **URL encoding** to safely transmit payloads

An attempt to execute system commands initially results in an error indicating: require is not defined 


This confirms execution within a restricted Node.js template context.

---

## Node.js Context Awareness

Further investigation relies on Node.js internals:

- **Top-level scope variable:** `global`
- The environment allows access to system-level execution through crafted payloads

With a correctly structured and encoded SSTI payload, command execution becomes possible.

---

## Exploitation Outcome

Successful exploitation of the SSTI vulnerability allows execution of arbitrary system commands.

The web server is running as: root 


This results in **full system compromise**.

---

## Key Takeaways

- Node.js template engines can be dangerous when user input is unsafely rendered
- SSTI vulnerabilities can directly lead to RCE
- Encoding payloads is critical when exploiting web filters
- Understanding runtime internals (like `global` in Node.js) is essential for exploitation

---

## Final Status

- **Root Access:** Achieved  
- **Machine:** Owned  

---

## Notes

This machine is an excellent introduction to modern web exploitation, especially for JavaScript-based stacks.  
It emphasizes methodology over brute force and reinforces careful observation of application behavior.

---






