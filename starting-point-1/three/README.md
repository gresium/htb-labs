# HTB Starting Point – Three

## Overview

**Three** is a Hack The Box Starting Point machine focused on web enumeration, DNS fundamentals, cloud storage exposure, and basic interaction with Amazon S3 services.  
The lab introduces how misconfigured subdomains and publicly accessible cloud buckets can expose sensitive data.

This machine reinforces enumeration discipline and teaches how cloud services integrate into web infrastructures.

---

## Machine Information

- **Platform:** Hack The Box
- **Tier:** Starting Point
- **Difficulty:** Easy
- **Category:** Web / Cloud / Enumeration
- **Target OS:** Linux
- **Cloud Service:** Amazon S3

---

## Initial Enumeration

### Port Scanning

A TCP scan reveals only two open ports on the target system:

- **Port 80** – HTTP
- **Port 22** – SSH

This indicates a minimal attack surface, with the primary focus on web enumeration.

---

## Website Reconnaissance

### Contact Information Discovery

Browsing the website and inspecting the **Contact** section reveals an email address using a custom domain:


thetoppers.htb

This strongly suggests the presence of **virtual hosts or subdomains**, which are not resolvable via public DNS.

---

## Hostname Resolution

Since no DNS server is provided, hostname resolution must be handled locally.

The Linux hosts file is used to manually map domains to the target IP address:


etc/hosts

Adding the discovered domain allows proper access to the web service.

Amazon S3 

This indicates that the application is using an S3 bucket for file storage, potentially exposed due to misconfiguration.

---

## Cloud Interaction Setup

### AWS CLI Usage

To interact with the S3 service, the AWS Command Line Interface is required.

The AWS CLI is configured using: aws comfigure 

For this machine, authentication is either not required or improperly enforced, allowing anonymous interaction.

---

## Bucket Enumeration

Once configured, all accessible S3 buckets are listed using: aws s3 ls 


This command reveals exposed buckets associated with the application.

---

## Data Discovery

Exploring the contents of the accessible bucket reveals web application files.

Among the discovered files is PHP-based content, confirming that the server processes: php 


This completes the exploitation chain by demonstrating how exposed cloud storage can leak application logic or sensitive files.

---

## Key Takeaways

- Always enumerate **email domains** found on websites
- Manual hostname resolution via `/etc/hosts` is critical without DNS
- Subdomains often reveal backend services
- Cloud storage (S3) is frequently misconfigured
- Anonymous access to S3 buckets is a real-world risk
- AWS CLI is an essential tool for cloud enumeration

---

## Tools Used

- Nmap
- Web Browser
- `/etc/hosts`
- AWS CLI

---

## Final Status

✅ Enumeration complete  
✅ Cloud service identified  
✅ S3 bucket accessed  
✅ Machine completed successfully  

---

## Notes

This machine emphasizes **methodical enumeration over exploitation** and mirrors common real-world cloud misconfiguration issues found in production environments.

---







