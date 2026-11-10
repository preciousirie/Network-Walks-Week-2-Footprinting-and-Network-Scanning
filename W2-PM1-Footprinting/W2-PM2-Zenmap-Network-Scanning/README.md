# PM2 — Zenmap Network Scanning

## Overview
This module focused on network discovery and host identification using Zenmap, the graphical interface for Nmap.

The exercise involved identifying the local network range, scanning an authorized network, discovering active hosts, reviewing scan results, and generating a network topology diagram.

## Objectives
- Identify the local IP configuration and network subnet.
- Understand CIDR notation and network scan targets.
- Discover active hosts within an authorized network.
- Review host availability and detected services.
- Examine available host identification information.
- Export a network topology diagram in PDF format.

## Tools Used
- Zenmap
- Nmap
- Windows 11

## Methodology

### 1. Network Configuration
Identified the local host's IP configuration, subnet mask, and default gateway to determine the correct network range for the exercise.

### 2. Target Selection
Configured Zenmap to scan the authorized local subnet using CIDR notation.

An important learning point was understanding the difference between targeting a single host IP and targeting an entire subnet. For network-wide host discovery, the target should represent the network address and prefix, rather than only the local computer's IP address.

The subnet must be calculated from the actual IP address and subnet mask; the `/24` shortcut should only be used when the network actually has a `/24` prefix.

### 3. Host Discovery
Performed a network discovery scan and reviewed the results to identify active hosts within the selected network range.

### 4. Host Information Analysis
Examined the available host information, including detected services, open ports, and MAC address information where displayed.

Not all hosts returned MAC address information in the scan results. Findings were documented according to the available evidence.

### 5. Network Topology
Used Zenmap's Topology view to visualize the discovered network hosts and exported the resulting graphic as a PDF.

## Key Findings
- Successfully identified active hosts within the authorized network.
- Observed differences between the local host and gateway scan results.
- Identified services and open ports reported by the scanner.
- Learned that MAC address information may not be available for every discovered host.
- Successfully exported the network topology for documentation.

## Evidence
The evidence folder contains screenshots of the network configuration, scan target, host discovery results, host information, and exported topology.

## Learning Outcomes
- Improved understanding of IP addressing and subnet identification.
- Learned how CIDR notation is used to define scan targets.
- Gained practical experience with Zenmap and Nmap.
- Developed skills in interpreting network discovery results.
- Practised documenting technical findings while protecting sensitive network information.

## Conclusion
This module strengthened my practical understanding of network discovery, subnet identification, host analysis, and network topology visualization.

All scanning activities were conducted within an authorized lab/network environment.
