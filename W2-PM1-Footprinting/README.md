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

## 🔍 4.3 WhatWeb Technology Identification

### Objective

To identify publicly detectable technologies, web server information, content management systems (CMS), and other technologies associated with `networkwalks.com`.

### 🛠️ Tool Used

- **WhatWeb**

### Command Executed

```bash
whatweb networkwalks.com
```

### 📋 Key Findings

| Category | Observation |
|---|---|
| HTTP Status | `301 Moved Permanently` |
| HTTPS Status | `200 OK` |
| Web Server | Apache |
| IP Address | `192.232.216.135` |
| CMS | WordPress 7.1.4 |
| WordPress Plugin Identified | WordPress Download Manager 3.3.76 |
| JavaScript Library | jQuery 3.7.1 |
| Front-end Framework | Bootstrap 7.1.4 (as reported by WhatWeb) |
| Web Technologies | HTML5, Open Graph Protocol |
| Analytics | Google Tag Manager |
| Page Title | Networkwalks Academy |
| Public Contact Email | info@networkwalks.com |
| Cookie Identified | `__wpdm_client` |
| Cookie Attribute | HttpOnly detected |

### 🔎 Analysis and Observations

The WhatWeb scan identified Apache as the web server and WordPress as the content management system used by the target website.

The initial HTTP request returned a `301 Moved Permanently` response, redirecting visitors to the HTTPS version of the website. The HTTPS endpoint returned `200 OK`, indicating that the page was successfully accessible during the scan.

WhatWeb also identified jQuery, Bootstrap, Google Tag Manager and WordPress Download Manager. These findings provide an overview of some of the technologies used by the website.

The scan detected the `__wpdm_client` cookie with the HttpOnly attribute. This attribute helps prevent client-side scripts from accessing that cookie.

### 🛡️ Security Relevance

Technology fingerprinting is useful during passive reconnaissance because it helps security professionals understand the technologies exposed by a website.

Identifying CMS platforms, plugins, frameworks and server technologies can help guide further security reviews. However, identifying a technology or version does not automatically establish that it contains a vulnerability.

Organizations should keep their web server, CMS, plugins and front-end dependencies updated and periodically review their security configurations.

### 📸 Evidence

The following screenshot captures the WhatWeb command execution and its output during the technology identification exercise.

- `PM1-03-WhatWeb-Scan.png`

### Conclusion

The WhatWeb scan successfully identified several publicly detectable technologies associated with `networkwalks.com`. The findings provide useful baseline information for the subsequent footprinting activities.

## 🔍 4.4 Nslookup – DNS Information Gathering

### Objective

To query the Domain Name System (DNS) and identify the IPv4 address associated with `networkwalks.com`.

### 🛠️ Tool Used

- **Nslookup**

### Command Executed

```bash
nslookup networkwalks.com
```

### 📋 Key Findings

| Category | Observation |
|---|---|
| Domain Queried | `networkwalks.com` |
| DNS Server | `10.171.146.84` |
| DNS Server Port | `53` |
| DNS Response Type | Non-authoritative answer |
| Resolved IPv4 Address | `192.232.216.135` |
| Additional Observation | DNS communication timeout reported after the answer |

### 🔎 Analysis and Observations

The Nslookup command successfully returned an IPv4 address for `networkwalks.com`.

The domain resolved to `192.232.216.135`, matching the IP address identified during the WhatWeb scan.

The DNS server used for the query was `10.171.146.84`, communicating over port 53.

The response was labelled non-authoritative, meaning the answer was supplied by a DNS resolver rather than directly by the domain's authoritative nameserver.

Although an answer was returned, the output also displayed a communication timeout involving the DNS server after the response. This indicates that an additional DNS communication attempt did not complete within the expected time.

### 🛡️ Security Relevance

DNS reconnaissance helps security professionals understand how domain names resolve to IP addresses and identify the DNS infrastructure involved in the resolution process.

The resolved IP address provides useful information for documenting the domain's publicly visible network presence. DNS timeout messages should also be recorded because they may indicate intermittent communication issues, although a single timeout does not establish a DNS vulnerability.

### 📸 Evidence

- `PM1-04-Nslookup-Results.png`

### Conclusion

The Nslookup query successfully resolved `networkwalks.com` to `192.232.216.135`. The result was consistent with the IP address identified during the WhatWeb scan, although a subsequent DNS communication timeout was also observed.
