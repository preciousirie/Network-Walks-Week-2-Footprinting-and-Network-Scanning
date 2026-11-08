## 🖥️ 4.1 Environment Verification

Before beginning the footprinting activities, I verified my Kali Linux environment and checked the availability of the required tools to ensure that the working environment was properly prepared.

### 👤 Check 1: Verify the Current Username

**Command:**

```bash
whoami
```

**Purpose:** To identify the currently logged-in Kali Linux user and confirm the active user account.

### 🛠️ Check 2: Verify the Availability of Required Tools

I used the Linux `command -v` command followed by the names of the required tools to check whether they were available in the Kali Linux environment.

**Command:**

```bash
command -v whois whatweb nslookup curl wafw00f dnsrecon
```
Purpose: To verify the availability of the required tools and identify their executable paths before beginning the practical exercise.

### 📋 Observation: The preliminary checks helped establish the readiness of the Kali Linux environment and determine whether any required tools needed to be installed before proceeding with the footprinting activities.


🔍 4.2 **WHOIS Information Gathering**

Objective: To gather publicly available domain registration information about networkwalks.com using the WHOIS lookup tool.

Tool Used **WHOIS**

Command:

whois networkwalks.com

Key Findings

WHOIS Field

Observation

Domain Name - NETWORKWALKS.COM

Registrar - GoDaddy

Creation Date - 6 November 2019

Last Updated - 12 November 2025

Registrar WHOIS Server - whois.godaddy.com

**Analysis** : The WHOIS lookup provided publicly available registration information for the target domain.

The domain registration date indicates that the domain was initially registered in November 2019. GoDaddy was identified as the registrar, while the last update recorded in the supplied output was in November 2025.

**WHOIS** information is useful during passive reconnaissance because it helps establish basic domain registration details without directly interacting with the target's applications.

Security Relevance

Public registration information can help an organization understand what information about its domains is externally visible. Organizations should review their domain registration privacy settings and ensure that administrative contact information is appropriately protected.
