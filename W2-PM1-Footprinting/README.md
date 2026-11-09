# 🔍 W2-PM1: Footprinting and Information Gathering

## 🖥️ 4.1 Environment Verification

### Objective

To verify the Kali Linux working environment and confirm the availability of the required tools before beginning the footprinting activities.

### 🛠️ Checks Performed

**Check 1: Verify the Current Username**

Command:

```bash
whoami
```

Purpose: To identify the currently logged-in Kali Linux user and confirm the active user account.

**Check 2: Verify the Availability of Required Tools**

Command:

```bash
command -v whois whatweb nslookup curl wafw00f dnsrecon
```

Purpose: To check whether the required command-line tools were available in the Kali Linux environment and identify their executable paths.

### 📋 Observations

The preliminary checks established the working environment and provided an initial assessment of the availability of the tools required for the footprinting exercise.

The `command -v` utility checks whether commands can be located through the system's executable search path.

### 📸 Evidence

- `PM1-01-Environment-Verification.png`

### Conclusion

The environment verification established the initial readiness of the Kali Linux system for the practical footprinting activities.

---

## 🔍 4.2 WHOIS – Domain Registration Information Gathering

### Objective

To collect publicly available domain registration information associated with `networkwalks.com` using the WHOIS lookup utility.

### 🛠️ Tool Used

- WHOIS

### Command Executed

```bash
whois networkwalks.com
```

### 📋 Key Findings

| WHOIS Field | Observation |
|---|---|
| Domain Name | `NETWORKWALKS.COM` |
| Registrar | GoDaddy |
| Creation Date | 6 November 2019 |
| Last Updated | 12 November 2025 |
| Registrar WHOIS Server | `whois.godaddy.com` |

### 🔎 Analysis and Observations

The WHOIS lookup returned publicly available registration information for `networkwalks.com`.

The domain was initially registered on 6 November 2019, with the latest update shown in the supplied output dated 12 November 2025.

GoDaddy was identified as the domain registrar, while `whois.godaddy.com` was listed as the registrar WHOIS server.

WHOIS information provides useful background during reconnaissance by helping security professionals understand domain registration details and identify publicly available registration information.

### 🛡️ Security Relevance

Domain registration information can help organizations understand what details about their domains are externally accessible.

Organizations should periodically review their domain registration information and ensure that administrative contact details are appropriately protected.

### 📸 Evidence

- `PM1-02-WHOIS-Lookup.png`

### Conclusion

The WHOIS lookup successfully provided registration information about `networkwalks.com`, including its registrar, creation date and last recorded update.

---

## 🔍 4.3 WhatWeb – Web Technology Identification

### Objective

To identify publicly detectable web technologies, server information, content management systems and other technologies associated with `networkwalks.com`.

### 🛠️ Tool Used

- WhatWeb

### Command Executed

```bash
whatweb networkwalks.com
```

### 📋 Key Findings

| Category | Observation |
|---|---|
| HTTP Response | `301 Moved Permanently` |
| HTTPS Response | `200 OK` |
| Web Server Fingerprint | Apache |
| IP Address | `192.232.216.135` |
| CMS | WordPress 7.1.4 (as reported) |
| Plugin Identified | WordPress Download Manager 3.3.76 |
| JavaScript Library | jQuery 3.7.1 |
| Front-end Technology | Bootstrap 7.1.4 (as reported) |
| Other Technologies | HTML5, Open Graph Protocol |
| Analytics Technology | Google Tag Manager |
| Page Title | Networkwalks Academy |
| Public Contact Email | `info@networkwalks.com` |
| Cookie Identified | `__wpdm_client` |
| Cookie Attribute | HttpOnly detected |

### 🔎 Analysis and Observations

The WhatWeb scan identified several technologies associated with the target website.

The initial HTTP request returned a `301 Moved Permanently` response, redirecting visitors to the HTTPS version of the website. The HTTPS endpoint subsequently returned `200 OK`, indicating that the requested page was accessible.

Apache was identified as the web server fingerprint, while WordPress was identified as the content management system.

Additional technologies detected included jQuery, Bootstrap, Google Tag Manager and WordPress Download Manager.

The scan also identified the `__wpdm_client` cookie and detected its HttpOnly attribute.

These findings provide an overview of the website's publicly detectable technology stack. However, automated technology fingerprints should be treated as identification results rather than independent confirmation of every installed component or version.

### 🛡️ Security Relevance

Web technology identification helps security professionals understand the technologies exposed by a website.

Information about CMS platforms, plugins, frameworks and server technologies can guide further security reviews and help organizations identify components that may require maintenance or security updates.

Technology identification alone does not establish the presence of a vulnerability.

Organizations should maintain their web applications, CMS platforms, plugins and dependencies through regular updates and security reviews.

### 📸 Evidence

The screenshot captures the WhatWeb command execution and its returned technology identification results.

- `PM1-03-WhatWeb-Scan.png`

### Conclusion

The WhatWeb scan identified several publicly detectable technologies associated with `networkwalks.com`, providing useful information about its web application environment.

---

## 🔍 4.4 Nslookup – DNS Information Gathering

### Objective

To query the Domain Name System (DNS) and identify the IPv4 address associated with `networkwalks.com`.

### 🛠️ Tool Used

- Nslookup

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
| Response Type | Non-authoritative answer |
| Resolved IPv4 Address | `192.232.216.135` |
| Additional Observation | DNS communication timeout reported after the answer |

### 🔎 Analysis and Observations

The Nslookup command successfully returned an IPv4 address for `networkwalks.com`.

The domain resolved to `192.232.216.135`, matching the IP address identified during the WhatWeb scan.

The DNS server used for the query was `10.171.146.84`, communicating over port 53.

The response was labelled non-authoritative, indicating that the answer was supplied by a DNS resolver rather than directly by the domain's authoritative nameserver.

Although a valid DNS answer was returned, the output also displayed a communication timeout involving the DNS server after the answer.

This timeout was recorded as an additional observation. It does not, by itself, establish a DNS configuration problem or vulnerability.

### 🛡️ Security Relevance

DNS reconnaissance helps security professionals understand how domain names are resolved into IP addresses and identify the DNS infrastructure involved in the resolution process.

The resolved IP address provides useful information about the domain's network presence.

DNS communication errors should also be documented because they may indicate intermittent communication or resolver-related issues that require further investigation.

### 📸 Evidence

- `PM1-04-Nslookup-Results.png`

### Conclusion

The Nslookup query successfully resolved `networkwalks.com` to `192.232.216.135`. The output also recorded a subsequent DNS communication timeout.

---

## 🔍 4.5 cURL – HTTP Response Header Analysis

### Objective

To inspect the HTTP response headers returned by `networkwalks.com` and identify information about the web server, response status, cookies and other HTTP configurations.

### 🛠️ Tool Used

- cURL

### Command Executed

```bash
curl -I https://networkwalks.com
```

### 📋 Key Findings

| Category | Observation |
|---|---|
| HTTP Protocol | HTTP/2 |
| Response Status | `200 OK` |
| Web Server Header | Apache |
| Content Type | `text/html; charset=UTF-8` |
| WordPress REST API Reference | `/wp-json/` detected |
| Cookie | `__wpdm_client` |
| Cookie Security Attributes | Secure, HttpOnly |
| Referrer Policy | `no-referrer-when-downgrade` |
| Cache Header | `x-nginx-cache: WordPress` |
| Permissions Policy | Present |
| Response Date | 8 November 2026 |

### 🔎 Analysis and Observations

The cURL command successfully retrieved the HTTP response headers from the HTTPS endpoint of `networkwalks.com`.

The server returned an `HTTP/2 200` response, indicating that the request was successfully processed.

The response identified Apache through the Server header and revealed WordPress REST API references through the `/wp-json/` endpoint.

The `__wpdm_client` cookie was also observed with both Secure and HttpOnly attributes.

The Secure attribute restricts the cookie to secure connections, while HttpOnly prevents direct access to the cookie through client-side scripts.

Additional response headers included a permissions policy, referrer policy and the WordPress-related cache header `x-nginx-cache`.

These headers provide useful information about the website's HTTP configuration and application environment.

### 🛡️ Security Relevance

HTTP response header analysis helps security professionals understand how a web server communicates with clients and identify security-related configuration information.

Reviewing response headers and cookie attributes can help assess the presence of security controls.

However, the presence of a security-related header does not independently establish that the website is secure. Further configuration review may be necessary.

### 📸 Evidence

- `PM1-05-cURL-Header-Analysis.png`

### Conclusion

The cURL request successfully retrieved the website's HTTP response headers, revealing information about its web server, WordPress configuration, cookie attributes and HTTP policies.

---

## 🔍 4.6 Wafw00f – Web Application Firewall Detection

### Objective

To identify whether a Web Application Firewall (WAF) was detected in front of `networkwalks.com`.

### 🛠️ Tool Used

- Wafw00f v2.4.2

### Command Executed

```bash
wafw00f networkwalks.com
```

### 📋 Key Findings

| Category | Observation |
|---|---|
| Target | `networkwalks.com` |
| WAF Detection Result | WAF detected |
| Identified WAF | ModSecurity |
| Provider/Signature | SpiderLabs |
| Number of Requests | 2 |
| HTTPS Endpoint | `https://networkwalks.com` |

### 🔎 Analysis and Observations

The Wafw00f scan identified ModSecurity (SpiderLabs) as the Web Application Firewall associated with the target website.

The tool completed its detection process using two HTTP requests.

This result indicates that the website has a detectable web application firewall layer that may help inspect, monitor and filter HTTP requests.

The identification represents the tool's fingerprinting result and does not independently establish the effectiveness or completeness of the WAF configuration.

### 🛡️ Security Relevance

A Web Application Firewall provides an additional layer of protection by inspecting web traffic and helping detect or filter potentially suspicious requests.

Identifying the WAF technology provides useful insight into the website's externally detectable defensive infrastructure.

Organizations should periodically review WAF rules, configurations and monitoring practices to ensure that the security controls remain effective.

### 📸 Evidence

- `PM1-06-Wafw00f-WAF-Detection.png`

### Conclusion

The Wafw00f scan identified ModSecurity (SpiderLabs) as the detected Web Application Firewall associated with `networkwalks.com`.

---

## 🔍 4.7 DNSRecon – DNS Enumeration

### Objective

To collect publicly available DNS information associated with `networkwalks.com`, including address records, text records and other DNS-related information.

### 🛠️ Tool Used

- DNSRecon

### Command Executed

```bash
dnsrecon -d networkwalks.com
```

### 📋 Key Findings

| DNS Category | Observation |
|---|---|
| Domain | `networkwalks.com` |
| A Record | `192.232.216.135` |
| TXT Record 1 | Google site verification record detected |
| TXT Record 2 | SPF record detected |
| SPF Mechanisms | `+a`, `+mx`, `+ip4:50.87.144.87`, `+include:websitewelcome.com`, `~all` |
| DNSSEC Query | No answer received |
| SOA Lookup | DNS operation timed out |
| Nameserver Used | `10.171.146.84` |
| SRV Records | No SRV records found |

### 🔎 Analysis and Observations

DNSRecon successfully identified the A record for `networkwalks.com`, resolving the domain to `192.232.216.135`.

The enumeration also discovered two TXT records. One contained a Google site verification value, while the other contained an SPF policy.

The SPF record included mechanisms for authorizing the domain's A and MX records, a specific IPv4 address (`50.87.144.87`) and an external SPF include (`websitewelcome.com`).

The `~all` mechanism indicates a softfail policy for senders that do not match the listed SPF mechanisms.

The tool also reported that no answer was received for its DNSSEC query and that the SOA lookup timed out while using `10.171.146.84` as the DNS server.

No SRV records were found during the enumeration.

These results provide an overview of the DNS records returned during the enumeration. The DNSSEC query failure and SOA timeout should be treated as lookup observations rather than confirmed security weaknesses.

### 🛡️ Security Relevance

DNS enumeration helps security professionals understand a domain's publicly available DNS configuration.

A records reveal address resolution, while TXT records can expose domain verification information and email authentication policies.

SPF information helps organizations identify which sources are authorized to send email on behalf of a domain.

DNSSEC, SOA and other DNS configuration observations can guide further review of the domain's DNS infrastructure.

Organizations should periodically review DNS records, email authentication policies and DNS infrastructure to ensure that configurations remain accurate and properly maintained.

### 📸 Evidence

- `PM1-07-DNSRecon-Enumeration.png`

### Conclusion

DNSRecon successfully identified the target domain's A and TXT records, including Google site verification and SPF information. The enumeration also reported DNSSEC and SOA lookup errors, alongside the absence of SRV records.
