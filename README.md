# SSH Brute Force Detection & Incident Response Investigation

## Project Overview

This project demonstrates the simulation and investigation of an SSH brute-force attack within an isolated Ubuntu lab environment using Multipass.

The objective was to replicate the activities of a Security Operations Center (SOC) analyst by detecting malicious authentication attempts, analysing Linux authentication logs, identifying indicators of compromise, mapping attacker behaviour to the MITRE ATT&CK framework, and producing remediation recommendations.

---

## Objectives

* Build an isolated attacker and target environment.
* Simulate an SSH brute-force attack using Hydra.
* Analyse authentication logs (`/var/log/auth.log`).
* Identify failed and successful login attempts.
* Determine whether account compromise occurred.
* Map findings to MITRE ATT&CK techniques.
* Create detection logic using Sigma rules.
* Produce an incident report and recommendations.

---

## Lab Architecture

```text
Attacker VM (Ubuntu)
192.168.252.3
        |
        | SSH Brute Force (Hydra)
        ▼
Target VM (Ubuntu)
192.168.252.2
```

---

## Technologies Used

* Ubuntu Linux
* Multipass
* OpenSSH
* Hydra
* Linux Authentication Logs
* Sigma Detection Rules
* MITRE ATT&CK Framework

---

## Attack Scenario

The attacker attempted multiple password guesses against the `analyst` account over SSH.

### Attack Timeline

| Time | Event                                           |
| ---- | ----------------------------------------------- |
| T0   | Multiple failed login attempts detected         |
| T1   | Repeated authentication failures from single IP |
| T2   | Successful login observed                       |
| T3   | Account compromise confirmed                    |

---

## Investigation Findings

### Indicators of Compromise (IOCs)

| IOC               | Value           |
| ----------------- | --------------- |
| Source IP         | 192.168.252.3   |
| Target Host       | target          |
| Username          | analyst         |
| Attack Type       | SSH Brute Force |
| Compromise Status | Successful      |

---

## Evidence

### Failed Logins

```bash
sudo grep 'Failed password' /var/log/auth.log
```

### Successful Login

```bash
sudo grep 'Accepted password' /var/log/auth.log
```

### Count Attacks by Source IP

```bash
sudo grep 'Failed password' /var/log/auth.log \
| grep -oE 'from [0-9.]+' \
| sort | uniq -c | sort -rn
```

---

## MITRE ATT&CK Mapping

| Technique      | ID    |
| -------------- | ----- |
| Brute Force    | T1110 |
| Valid Accounts | T1078 |

---

## Sigma Detection Rule

See:

`detection/sigma-rule.yml`

---

## Recommendations

1. Enforce strong password policies.
2. Disable password-based SSH authentication.
3. Implement SSH key authentication.
4. Deploy Fail2Ban.
5. Configure SIEM alerting for repeated login failures.
6. Enable Multi-Factor Authentication (MFA).

---

## Skills Demonstrated

* Security Monitoring
* Threat Hunting
* Log Analysis
* Incident Response
* IOC Identification
* Linux Security
* Detection Engineering
* MITRE ATT&CK Mapping
* SOC Investigation Methodology

---

## Author

**Testimony Igbagiri**

MSc Cyber Security | SOC Analyst | Threat Detection | Blue Team Operations
