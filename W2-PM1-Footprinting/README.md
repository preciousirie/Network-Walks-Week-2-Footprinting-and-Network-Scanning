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
| Web
