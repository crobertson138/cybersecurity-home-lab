# Cybersecurity Home Lab — Learning Portfolio

## Project Overview

This repository documents my hands-on cybersecurity education, focusing on Linux administration, networking fundamentals, packet analysis, network troubleshooting, and defensive security investigations.

My long-term goal is to develop the technical skills required for a Security Operations Center (SOC) Analyst position and eventually specialize in AI security and defense.

My approach emphasizes evidence-based investigation, understanding normal network behavior, and distinguishing suspicious activity from confirmed security threats.

## Lab Environment

**Host System**
- Apple Silicon M1 MacBook Pro
- 16 GB RAM
- macOS
- VMware Fusion

**Virtual Environment**
- Kali Linux ARM64
- Virtual network using VMware
- Kali IPv4 address observed: `192.168.226.128`
- VMware gateway/DNS address observed: `192.168.226.2`

**Tools Used**
- Linux terminal
- Wireshark
- Nmap
- curl
- nslookup
- ping
- ss
- Python

---

## Lab 01 — Linux Fundamentals

**Objective:** Become familiar with Linux command-line tools and basic system administration.

Commands practiced:

```bash
whoami
hostname
pwd
top
ss -tuln
sudo ss -tulpn
```

### Findings

- `whoami` identified the active user.
- `hostname` identified the computer as `kali`.
- `pwd` displayed the current working directory.
- `top` displayed active processes and resource utilization.
- `ss -tuln` identified listening TCP and UDP sockets.
- `sudo ss -tulpn` provided process information associated with sockets.

A listening TCP socket on port 1716 was associated with `kdeconnectd`.

**Lesson learned:** Open or listening ports are not automatically evidence of malicious activity. Their purpose, associated process, and exposure must be investigated.

---

## Lab 02 — Network Traffic Analysis with Wireshark

**Objective:** Capture and identify network protocols.

I installed and launched Wireshark in Kali Linux and captured traffic on the `eth0` interface.

Protocols observed included:

- DNS
- TCP
- UDP
- TLS
- ARP
- ICMP and ICMPv6
- mDNS

### Findings

I identified source and destination IP addresses, inspected packet details, and used display filters to isolate protocols.

Example filters:

```text
dns
tls
ip.addr == 3.233.158.25
```

I learned that Wireshark packet colors represent configurable display rules, not automatic security threat classifications.

**Lesson learned:** Packet interpretation requires examining protocol behavior and context rather than relying on colors or unfamiliar addresses.

---

## Lab 03 — DNS and TLS Investigation

**Objective:** Understand how web connections are established.

I examined DNS queries and responses, TLS handshakes, and encrypted HTTPS traffic.

Observed domain:

`location.services.mozilla.com`

I located the domain name within the TLS Client Hello Server Name Indication (SNI) extension.

I also investigated traffic associated with:

`browser-intake-datadoghq.com`

### Investigation Findings

Initially, I considered the Datadog domain suspicious because I was unfamiliar with it.

Further discussion established that unfamiliarity alone does not demonstrate malicious activity.

**Lesson learned:** Classify unfamiliar traffic as requiring further investigation rather than immediately declaring it malicious.

---

## Lab 04 — HTTP vs. HTTPS

**Objective:** Understand the security differences between encrypted and unencrypted web traffic.

I generated web requests using `curl` and examined the resulting traffic.

### Findings

- DNS resolves hostnames into IP addresses.
- TCP provides reliable transport for conventional HTTP/HTTPS connections.
- TLS establishes encryption for HTTPS.
- HTTP without TLS can expose transmitted information to parties capable of observing or modifying the connection.
- HTTPS protects application data in transit when TLS is properly established and validated.

**Lesson learned:** Encryption is an important security control, but HTTPS alone does not guarantee that a website is trustworthy.

---

## Lab 05 — TCP and Network Discovery

**Objective:** Understand network connections, port states, and TCP behavior.

I practiced identifying TCP connection behavior and interpreting Wireshark captures.

I also began learning Nmap for network discovery and service enumeration.

Example local test:

```bash
nmap -sV 127.0.0.1
```

An initial localhost scan reported that the 1,000 commonly scanned TCP ports were closed.

### Findings

- TCP uses a three-way handshake: SYN, SYN-ACK, ACK.
- TCP RST packets indicate connection resets or rejections.
- A TCP reset is not automatically malicious.
- An open port indicates that a service may be reachable, not necessarily that it is vulnerable.
- Network scanning must be limited to authorized targets.

**Lesson learned:** Port states and TCP flags must be interpreted in the context of the connection.

---

## Lab 06 — ICMP and Connectivity Troubleshooting

**Objective:** Understand basic network diagnostics.

I generated ICMP echo requests and examined the corresponding responses.

### Findings

- Echo requests originated from `192.168.226.128`.
- Echo replies were observed from `8.8.8.8`.
- 20 replies were recorded.
- Average round-trip time: 13.891 milliseconds.
- No unusually slow responses were observed during the test.

**Lesson learned:** ICMP can help evaluate network reachability, packet loss, and latency, but successful ping responses do not prove that every application or service is functioning.

---

## Lab 07 — DNS Resolver Performance

**Objective:** Compare DNS resolution performance using different DNS servers.

DNS resolvers tested:

| DNS Resolver | Initial Result |
|---|---|
| VMware — 192.168.226.2 | 0.06 seconds |
| Google — 8.8.8.8 | 0.05 seconds |
| Cloudflare — 1.1.1.1 | 4.26 seconds |

### Investigation

The unusually slow Cloudflare result prompted further testing.

I repeated DNS queries and captured the resulting traffic using Wireshark.

In a subsequent capture, I observed:

- A DNS A query for `openai.com`
- A corresponding A response
- A DNS AAAA query
- A corresponding AAAA response

The A record response contained an IPv4 address.

The AAAA response contained an SOA record rather than an IPv6 address.

### Measured Packet Response Times

- A query/response: approximately 18.1 milliseconds
- AAAA query/response: approximately 18.6 milliseconds

### Conclusion

Cloudflare responded promptly in the subsequent packet capture. The earlier 4.26-second result was not reproduced in that test.

The available evidence does not establish the cause of the original delay.

**Lesson learned:** A single slow measurement is insufficient to diagnose a persistent network problem. Repeated measurements and packet-level evidence help distinguish transient issues from recurring faults.

---

## Lab 08 — ARP and Local Network Communication

**Objective:** Understand how devices identify each other on a local IPv4 network.

Observed ARP exchange:

```text
Who has 192.168.226.2?
Tell 192.168.226.128
```

Response:

```text
192.168.226.2 is at 00:50:56:ec:b4:84
```

### Findings

ARP resolves IPv4 addresses to link-layer MAC addresses on the local network.

The observed exchange was consistent with normal VMware virtual network communication.

**Lesson learned:** ARP is necessary for ordinary local network communication, although attackers can abuse it through techniques such as ARP spoofing.

---

## Security Investigation Principles

The most important lessons from these exercises are:

1. **Evidence before conclusions:** Unfamiliar domains and IP addresses are not automatically malicious.
2. **Understand normal behavior:** Learning DNS, ARP, ICMP, TCP, and TLS makes unusual activity easier to identify.
3. **Investigate anomalies:** Delays, resets, failed queries, and unexpected connections deserve contextual analysis.
4. **Avoid false positives:** Wireshark colors and individual packet characteristics are not proof of compromise.
5. **Document findings:** Record observations, evidence, uncertainty, and conclusions separately.
6. **Respect authorization:** Perform scanning and security testing only on systems where permission has been granted.

## Next Learning Objectives

- DNS anomaly detection
- TCP connection troubleshooting
- Recognizing suspicious traffic patterns
- Introductory security alert triage
- Log analysis
- Incident documentation
- SIEM fundamentals
- Continued defensive security and AI security exercises

## Professional Development

This portfolio represents independent, hands-on cybersecurity training. It documents my technical learning and investigation methods as I work toward an entry-level SOC Analyst or cybersecurity position.

All experiments are conducted for educational purposes using authorized systems and environments.
