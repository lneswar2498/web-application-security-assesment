# Web Application Security Assessment — OWASP Juice Shop

> A hands-on web security assessment of an intentionally vulnerable e-commerce application in a TryHackMe lab.

[![Platform](https://img.shields.io/badge/Lab-TryHackMe-212C42)](https://tryhackme.com/)
[![Target](https://img.shields.io/badge/Target-OWASP%20Juice%20Shop-orange)](https://owasp.org/www-project-juice-shop/)
[![Focus](https://img.shields.io/badge/Focus-Web%20Application%20Security-blue)](#assessment-scope)

## Project overview

This project documents a practical assessment of OWASP Juice Shop through a TryHackMe environment. The objective was to understand how common web application weaknesses can be discovered, validated, and communicated with practical remediation advice.

The work combined initial network discovery with manual application exploration and HTTP request inspection. Burp Suite Community Edition was used to inspect and modify requests in the lab; Nmap was used for initial service discovery.

## Assessment scope

The activities documented in this lab covered:

- SQL injection testing against the login workflow, including an authentication-bypass outcome in the intentionally vulnerable target.
- Cross-site scripting (XSS) testing through an application input field.
- Information disclosure through a document request.
- Client-side versus server-side validation, using a modified feedback rating request.
- Inspection and manipulation of product-related HTTP requests and responses.

All testing was performed against the designated training target in TryHackMe. These techniques must only be used in systems for which testing is explicitly authorized.

## Environment and tools

| Component | Purpose |
|---|---|
| TryHackMe | Hosted, authorized training environment |
| OWASP Juice Shop | Intentionally vulnerable web application |
| Kali Linux | Assessment workstation |
| OpenVPN | Connection to the TryHackMe lab network |
| Nmap | Initial port and service discovery |
| Burp Suite Community Edition | HTTP proxy, interception, and Repeater |
| Web browser | Manual application exploration |

## Methodology

### 1. Lab connectivity

Joined the relevant TryHackMe room, started the target instance, downloaded the room-provided OpenVPN configuration, and connected from Kali Linux. The target address was session-specific and could change when the lab instance was restarted.

### 2. Initial service discovery

Used Nmap against the assigned lab target to identify exposed ports and services before beginning application-level testing. The README notes HTTP and SSH services during the recorded scan; exact scan output is not included here.

### 3. Application reconnaissance

Opened Juice Shop in a browser and reviewed its public pages, navigation, product area, feedback feature, and information pages. This established the application workflow and likely input points for further testing.

### 4. HTTP traffic inspection

Started Burp Suite Community Edition and configured the browser to use the local proxy at `127.0.0.1:8080`. Intercepted application traffic and used Burp Repeater to review and modify selected requests.

### 5. Vulnerability validation

| Area tested | Lab observation | Defensive recommendation |
|---|---|---|
| Login input | SQL injection test resulted in an administrative session in the lab | Use parameterized queries; avoid dynamically concatenated SQL; enforce authentication controls |
| User input | XSS-related behavior was observed during the test | Apply context-aware output encoding, safe templating, input validation, and an appropriate Content Security Policy |
| Document access | Changing a requested document path exposed additional content | Enforce server-side authorization for every resource; do not rely on obscurity of file names |
| Feedback rating | A modified HTTP request accepted a value outside the normal UI range | Validate allowed values on the server side |
| Product requests | Request/response behavior and returned product information were inspected | Validate client-controlled parameters and enforce object-level authorization |

The table summarizes observations recorded in the project notes. It does not imply that every possible variant of these vulnerability classes was tested.

## Key learning outcomes

- Established a VPN-connected security testing environment for a hosted lab.
- Used Nmap for initial network and service discovery.
- Configured Burp Suite as an intercepting proxy and used Repeater for request analysis.
- Practised identifying input-handling, authorization, and information-disclosure weaknesses.
- Connected technical observations to practical remediation recommendations.

## Evidence and reproducibility

The original project notes describe the testing sequence, but this repository currently contains no screenshots, raw scan output, sanitized HTTP captures, or exported evidence files. Add those artifacts only after checking that they contain no credentials, session cookies, personal data, or live target details.

For a stronger technical portfolio, future evidence can include:
- A sanitized Nmap output excerpt.
- A redacted request/response pair for each confirmed finding.
- Screenshots showing the relevant Burp Repeater test and observed response.
- A concise finding report containing severity rationale, impact, reproduction summary, and remediation.

## Limitations

- The work was performed on an intentionally vulnerable training application, not a production e-commerce site.
- Exact tool versions, full command history, and raw evidence were not included in the source notes.
- Findings are limited to the workflows described above; this is not a claim of comprehensive application coverage.

## Responsible use

This repository is for education and authorized security testing. Do not test websites, accounts, or infrastructure without explicit permission.

## Author

**Naga Venkata Eswara Sastry L**  
Cybersecurity learner | Aspiring SOC Analyst

