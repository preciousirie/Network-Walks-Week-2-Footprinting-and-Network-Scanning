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


🔍 4.5 cURL – HTTP Header Analysis

Objective

To inspect the HTTP response headers returned by networkwalks.com and identify information about the web server, response status, cookies and other HTTP configurations.

🛠️ Tool Used

cURL

Command Executed

curl -I https://networkwalks.com

📋 Key Findings

Category

Observation

HTTP Protocol

HTTP/2

Response Status

200 OK

Web Server

Apache

Content Type

text/html; charset=UTF-8

WordPress REST API

/wp-json/ detected

Cookie

__wpdm_client

Cookie Security Attributes

Secure, HttpOnly

Referrer Policy

no-referrer-when-downgrade

Cache Information

x-nginx-cache: WordPress

Permissions Policy

Present

Response Date

8 November 2026

🔎 Analysis and Observations

The cURL command successfully retrieved the HTTP response headers from the HTTPS endpoint of networkwalks.com.

The server returned an HTTP/2 200 response, indicating that the request was successfully processed.

The response identified Apache as the web server and revealed WordPress REST API references through the /wp-json/ endpoint.

The __wpdm_client cookie was also observed with both Secure and HttpOnly attributes. These attributes help protect the cookie by restricting transmission to secure connections and preventing direct access through client-side scripts.

Additional response headers included a permissions policy, referrer policy and WordPress-related cache information.

🛡️ Security Relevance

HTTP header analysis helps security professionals understand how a web server communicates with clients and identify security-related configuration information.

Reviewing headers and cookie attributes can help assess whether appropriate security controls are being applied. However, the presence of a particular header does not independently prove that the website is secure.

📸 Evidence

PM1-05-cURL-Header-Analysis.png

Conclusion

The cURL request successfully returned the website's HTTP response headers, revealing useful information about its web server, WordPress configuration, cookie attributes and HTTP security policies.


🔍 4.6 Wafw00f – Web Application Firewall Detection

Objective

To identify whether a Web Application Firewall (WAF) was detected in front of networkwalks.com.

🛠️ Tool Used

Wafw00f v2.4.2

Command Executed

wafw00f networkwalks.com

📋 Key Findings

Category

Observation

Target

networkwalks.com

WAF Detection Result

WAF detected

Identified WAF

ModSecurity

WAF Provider/Signature

SpiderLabs

Requests Made

2

HTTPS Endpoint

https://networkwalks.com

🔎 Analysis and Observations

The Wafw00f scan identified ModSecurity (SpiderLabs) as the Web Application Firewall protecting the target website.

The tool completed its detection process using two HTTP requests.

This finding indicates that the website has a detected web application firewall layer that may help monitor and filter certain HTTP requests.

🛡️ Security Relevance

A Web Application Firewall provides an additional layer of protection by inspecting web traffic and helping detect or filter suspicious requests.

Identifying the WAF technology is useful during reconnaissance because it provides insight into the website's defensive security infrastructure.

WAF detection alone does not establish how effectively the firewall is configured or whether all potential threats are blocked.

📸 Evidence

PM1-06-Wafw00f-WAF-Detection.png

Conclusion

The Wafw00f scan successfully identified ModSecurity (SpiderLabs) as the detected WAF protecting networkwalks.com.


🔍 4.7 DNSRecon – DNS Enumeration

Objective

To collect publicly available DNS information associated with networkwalks.com, including address records, text records and other DNS-related information.

🛠️ Tool Used

DNSRecon

Command Executed

dnsrecon -d networkwalks.com

📋 Key Findings

DNS Category

Observation

Domain

networkwalks.com

A Record

192.232.216.135

TXT Record 1

Google site verification record detected

TXT Record 2

SPF record detected

SPF Mechanisms

+a, +mx, +ip4:50.87.144.87, +include:websitewelcome.com, ~all

DNSSEC Query

No answer received

SOA Lookup

DNS operation timed out

Nameserver Used

10.171.146.84

SRV Records

No SRV records found

🔎 Analysis and Observations

DNSRecon successfully identified the A record for networkwalks.com, resolving the domain to 192.232.216.135.

The enumeration also discovered two TXT records. One contained a Google site verification value, while the other contained an SPF policy.

The SPF record included mechanisms for authorizing the domain's A and MX records, a specific IPv4 address (50.87.144.87) and an external SPF include (websitewelcome.com). The ~all mechanism indicates a softfail policy for senders that do not match the listed mechanisms.

The tool also reported that no answer was received for its DNSSEC query and that the SOA lookup timed out while using 10.171.146.84 as the DNS server.

No SRV records were found during the enumeration.

🛡️ Security Relevance

DNS enumeration helps security professionals understand a domain's publicly available DNS configuration.

A records reveal address resolution, TXT records can expose domain verification and email security policies, while SPF information helps explain which sources are authorized to send email for a domain.

DNSSEC and SOA lookup errors should be recorded as observations. However, the DNSSEC query failure and SOA timeout alone do not establish a DNS security vulnerability.

Organizations should periodically review their DNS records, email authentication policies and DNS infrastructure to ensure that configurations remain accurate and properly maintained.

📸 Evidence

PM1-07-DNSRecon-Enumeration.png

Conclusion

DNSRecon successfully identified the target domain's A and TXT records, including its Google verification and SPF information. The scan also reported DNSSEC and SOA lookup errors, alongside the absence of SRV records.
