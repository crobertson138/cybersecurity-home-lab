# Cybersecurity Home Lab

**Hands-On Cybersecurity Training | Network Analysis | Linux | SOC Fundamentals**

Welcome to my cybersecurity home lab portfolio.

I'm an aspiring cybersecurity professional developing practical skills in network security, threat detection, incident investigation, and defensive security operations.

My immediate career objective is to become an entry-level **Security Operations Center (SOC) Analyst**, with a long-term goal of specializing in **AI security and defense**.

This repository documents my hands-on learning, technical experiments, observations, and troubleshooting exercises.

---

## Lab Environment

| Component | Technology |
|---|---|
| Host computer | Apple Silicon M1 Mac |
| Virtualization | VMware Fusion |
| Operating system | Kali Linux ARM64 |
| Network analysis | Wireshark |
| Network discovery | Nmap |
| DNS troubleshooting | nslookup |
| HTTP testing | curl |
| Command line | Linux shell |

## Completed Lab Exercises

| Lab | Topic | Skills Practiced |
|---|---|---|
| 01 | Linux Fundamentals | System identification, process monitoring, command-line navigation |
| 02 | Network Connections | TCP/UDP sockets, listening ports, process identification |
| 03 | Wireshark Analysis | Packet capture, protocol filtering, traffic inspection |
| 04 | DNS Investigation | DNS queries, responses, domain identification |
| 05 | HTTP vs. HTTPS | TLS handshakes, encrypted traffic, security implications |
| 06 | TCP Analysis | Connection establishment, resets, port states |
| 07 | ICMP Analysis | Echo requests, replies, latency measurement |
| 08 | DNS Performance | Resolver comparison, packet-level troubleshooting |
| 09 | ARP Analysis | Local network address resolution |

**[Read My Cybersecurity Lab Documentation](cybersecurity-home-lab.md)**

---

## Technical Skills in Development

**Network Analysis**
- Identifying common network protocols
- Capturing and filtering traffic using Wireshark
- Examining source and destination IP addresses
- Understanding TCP handshakes and connection resets
- Investigating DNS resolution and latency

**Linux Administration**
- Navigating the Linux terminal
- Monitoring processes and system resources
- Inspecting network sockets
- Using command-line diagnostic tools

**Security Investigation**
- Distinguishing unusual behavior from confirmed threats
- Recognizing the importance of investigation before escalation
- Understanding the security differences between HTTP and HTTPS
- Documenting findings and maintaining evidence-based conclusions

## Investigation Philosophy

One of the most important lessons I've learned is that **unfamiliar activity is not necessarily malicious activity**.

For example, during a Wireshark investigation, I encountered traffic involving a Datadog domain that I initially considered suspicious because I didn't recognize it.

Rather than treating unfamiliarity as proof of compromise, I learned to investigate the domain, understand the traffic, and evaluate the available evidence before drawing conclusions.

This experience reinforced a principle I intend to carry into professional cybersecurity work:

**Investigate first. Verify the evidence. Document the findings. Escalate when justified.**

---

## Current Learning Objectives

- [x] Establish a Kali Linux virtual machine
- [x] Learn essential Linux terminal commands
- [x] Capture network traffic with Wireshark
- [x] Identify DNS, TCP, TLS, ARP, and ICMP traffic
- [x] Investigate DNS performance
- [x] Understand TCP resets and basic connection behavior
- [ ] Perform structured security alert triage exercises
- [ ] Learn SIEM fundamentals
- [ ] Practice security log analysis
- [ ] Build a simulated SOC investigation
- [ ] Develop introductory incident response reports
- [ ] Explore AI-assisted threat detection and defensive security

## Professional Development

I am currently pursuing IT training through Calbright College, working toward CompTIA A+ foundational knowledge while independently studying cybersecurity.

My professional background includes security operations, monitoring, dispatching, incident documentation, and working in environments requiring careful observation and accurate reporting.

I am building on that experience to transition into IT and cybersecurity.

## Future Projects

Planned additions to this repository include:

- Simulated SOC alert investigations
- Network traffic anomaly analysis
- Security event log investigations
- Incident response documentation
- SIEM exercises
- Defensive security automation experiments

---

*This repository documents independent educational work performed in authorized lab environments. Findings and conclusions are based on observed evidence and are updated as my technical knowledge develops.*
