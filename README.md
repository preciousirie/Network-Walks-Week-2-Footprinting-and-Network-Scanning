# Network Walks Cybersecurity Internship — Week 2

**Batch:** B084  
**Focus:** Footprinting and Network Scanning

## Overview

This repository documents my Week 2 practical activities as part of the Network Walks Cybersecurity Internship. The exercises focus on information gathering, reconnaissance, network discovery, and basic analysis using industry-relevant cybersecurity tools.

The work is organized into two practical modules, supported by screenshots and documented findings.

## Learning Objectives

- Understand the fundamentals of footprinting and reconnaissance.
- Identify domain information and investigate DNS records.
- Examine website technologies and HTTP response headers.
- Understand basic web application firewall detection.
- Discover active devices within an authorized local network.
- Interpret basic network scan results and host information.
- Generate and document a network topology diagram.

## Project Modules

### Module 1: Footprinting

**Folder:** `W2-PM1-Footprinting/`

This module covers information gathering and reconnaissance using multiple tools.

**Tools used:**
- WHOIS
- WhatWeb
- Nslookup
- cURL
- WAFW00F
- DNSRecon

[View Module 1 Documentation](W2-PM1-Footprinting/README.md)

### Module 2: Zenmap Network Scanning

**Folder:** `W2-PM2-Zenmap-Network-Scanning/`

This module focuses on local network discovery and scan-result analysis using Zenmap, the graphical interface for Nmap.

**Activities included:**
- Identifying the local IP address and subnet.
- Configuring the appropriate subnet target in CIDR notation.
- Discovering active hosts on the authorized local network.
- Reviewing host information and available MAC address details.
- Generating and exporting a network topology diagram.

[View Module 2 Documentation](W2-PM2-Zenmap-Network-Scanning/README.md)

## Final Report

The final report brings together the practical activities, methodology, observations, learning outcomes, and conclusions from both modules.

[View Week 2 Final Report](Final-Report/Week-2-Penetration-Testing-Report.md)

## Tools and Environment

| Category | Tools |
|---|---|
| Operating System | Kali Linux, Windows 11 |
| Footprinting | WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, DNSRecon |
| Network Scanning | Zenmap, Nmap |
| Documentation | GitHub, Markdown |
| Evidence | Screenshots, network topology PDF |

## Key Learning Outcome

One important lesson from the network scanning exercise was understanding the difference between a local host IP address and a network subnet.

When the objective is to discover active devices across a subnet, the target should be the correct network address in CIDR notation rather than only the local computer's IP address. The subnet must be determined from the actual IP address and subnet mask.

## Evidence and Documentation

Each module contains its own README and supporting evidence. Screenshots and exported files are organized within their respective module folders to make the practical work easy to review.

## Responsible Testing

All network scanning activities documented in this repository were conducted within an authorized local network environment for educational purposes.

## Conclusion

Week 2 provided practical exposure to footprinting, reconnaissance, DNS investigation, website technology identification, network discovery, and basic scan-result interpretation.

The exercises strengthened my understanding of how information gathering and network scanning contribute to the early stages of a penetration-testing workflow.

**Network Walks Cybersecurity Internship — Batch B084**
