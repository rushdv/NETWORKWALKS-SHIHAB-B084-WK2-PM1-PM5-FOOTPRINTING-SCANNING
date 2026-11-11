# Footprinting and Local Network Scanning

Week 2 project modules PM1 and PM5 for Batch B084. This repository documents a practical exercise in collecting publicly observable domain and web-service information, followed by a basic host-discovery scan of a private lab network using Zenmap.

The repository is an evidence archive and learning reference. It contains command output, screenshots, and an eight-page written report; it does not contain a runnable application.

## Contents

- [Project scope](#project-scope)
- [Modules and observations](#modules-and-observations)
- [Repository structure](#repository-structure)
- [Tools and environment](#tools-and-environment)
- [Methodology](#methodology)
- [Limitations](#limitations)
- [Responsible use](#responsible-use)

## Project Scope

The work is split into two separate modules:

| Module | Activity | Target represented in the evidence |
| --- | --- | --- |
| W2-PM1 | External footprinting and web-technology identification | `networkwalks.com` |
| W2-PM5 | Local host discovery and topology visualization in Zenmap | Private lab subnet `10.0.0.0/24` |

The saved output timestamps indicate that the exercises were run on November 11, 2026. Results describe only what the tools observed at that time and should not be treated as current configuration or security assurance.

## Modules and Observations

### W2-PM1: Footprinting

The PM1 evidence contains output and a screenshot for each of the following checks:

| Check | Evidence | What it records |
| --- | --- | --- |
| Domain registration lookup | [`whois.txt`](W2-PM1/whois.txt), [`whois.png`](W2-PM1/whois.png) | Registrar, registration dates, domain status, and name-server data returned by WHOIS |
| DNS lookup | [`nslookup.txt`](W2-PM1/nslookup.txt), [`nslookup.png`](W2-PM1/nslookup.png) | A DNS answer for the domain using the resolver shown in the capture |
| DNS enumeration | [`dnsrecon.txt`](W2-PM1/dnsrecon.txt), [`dnsrecon.png`](W2-PM1/dnsrecon.png) | SOA, NS, MX, A, TXT, and SRV records returned by DNSRecon |
| HTTP response headers | [`curl-i.txt`](W2-PM1/curl-i.txt), [`curl-i.png`](W2-PM1/curl-i.png) | Response status and selected headers from the HTTPS endpoint |
| Web-technology fingerprint | [`whatweb.txt`](W2-PM1/whatweb.txt), [`whatweb.png`](W2-PM1/whatweb.png) | Server response and technologies fingerprinted by WhatWeb, including WordPress-related components |
| WAF fingerprint | [`wafw00f.txt`](W2-PM1/wafw00f.txt), [`wafw00f.png`](W2-PM1/wafw00f.png) | WAFW00F's reported web-application firewall identification |

The captured outputs report an HTTPS `200` response, identify WordPress and related components, and report a ModSecurity (SpiderLabs) WAF. DNSRecon also records a DNSSEC-query error alongside its returned records. These are tool observations, not independently verified vulnerabilities or guarantees about the live service. Fingerprint results can be incomplete or inaccurate.

### W2-PM5: Zenmap

The Zenmap screenshots document a ping-scan exercise against the private `10.0.0.0/24` lab subnet. The captured output reports 256 addresses scanned and three hosts up. The topology view visualizes the discovered hosts.

- [`network.png`](W2-PM5%20-%20Zenmap/network.png): Zenmap scan output and discovered hosts.
- [`topology.png`](W2-PM5%20-%20Zenmap/topology.png): Zenmap topology visualization.

These screenshots demonstrate host discovery only. They do not establish that ports or services were assessed.

## Repository Structure

```text
.
├── README.md
├── Penetration Testing Report.pdf
├── W2-PM1/
│   ├── curl-i.txt / curl-i.png
│   ├── dnsrecon.txt / dnsrecon.png
│   ├── nslookup.txt / nslookup.png
│   ├── wafw00f.txt / wafw00f.png
│   ├── whatweb.txt / whatweb.png
│   └── whois.txt / whois.png
└── W2-PM5 - Zenmap/
	├── network.png
	└── topology.png
```

The text files preserve terminal output for review and search. PNG files provide visual evidence of the corresponding tool sessions. The [Penetration Testing Report](Penetration%20Testing%20Report.pdf) provides the accompanying written report.

## Tools and Environment

The evidence shows the following tools and environment:

- Kali Linux terminal for the PM1 checks.
- `whois`, `nslookup`, `DNSRecon`, `curl`, `WhatWeb`, and `WAFW00F` for domain and web-service footprinting.
- Zenmap with Nmap for local-network host discovery and topology visualization.

Tool versions and target configurations may differ from those shown in the captures. The archive does not include a dependency lockfile or an automated test suite because it contains evidence files rather than software.

## Methodology

The exercise follows a basic discovery workflow:

1. Collect domain-registration and DNS information.
2. Observe the web endpoint's HTTP response and identify technologies using fingerprinting tools.
3. Record the WAF fingerprint result as an indicator for later validation, not as a definitive security conclusion.
4. Separately, use Zenmap for host discovery on the authorized private lab subnet and save the output and topology view.
5. Preserve raw output and screenshots, then summarize the observations in the written report.

To reproduce or extend any assessment, use a controlled lab or obtain explicit written authorization for every target and activity first. Keep external-domain checks separate from local-network scans, and set scan scope and intensity to the approved engagement boundaries.

## Limitations

- The results are point-in-time observations from November 11, 2026; services, DNS records, and software versions can change.
- Tool fingerprints can produce false positives, miss components, or report only what is visible to an unauthenticated observer.
- The Zenmap evidence shows a ping scan, not a port or vulnerability assessment.
- The artifacts do not demonstrate exploitation, authenticated testing, remediation validation, or a comprehensive security review.
- Screenshots are supporting evidence; the saved text outputs should be preferred when exact output details matter.

## Responsible Use

Only assess systems you own or for which you have explicit authorization. A public website being reachable does not imply permission to scan it. Do not use this repository as authorization to assess the domain or network shown in the captures. Follow applicable laws, the target owner's rules of engagement, and the relevant tool-provider terms. Store and share assessment data responsibly, since DNS, infrastructure, and registration details may be sensitive in context.
