# Incident Report – SSH Brute Force Compromise

## Executive Summary

On 09 July 2026, an SSH brute-force attack was detected against the `analyst` account on the Ubuntu target host.

Multiple failed authentication attempts originating from IP address `192.168.252.3` were identified, followed by a successful login using valid credentials.

The investigation confirmed account compromise.

---

## Incident Details

### Incident Type

Credential Access – SSH Brute Force Attack

### Affected Asset

Target Ubuntu Virtual Machine

### User Account

analyst

### Attacker Source

192.168.252.3

---

## Investigation Timeline

1. Multiple failed SSH login attempts detected.
2. Authentication failures occurred within a short timeframe.
3. Successful login observed from same source IP.
4. Compromise confirmed.
5. Incident escalated.

---

## Evidence

### Failed Authentication Attempts

```bash
Failed password for analyst from 192.168.252.3
```

### Successful Authentication

```bash
Accepted password for analyst from 192.168.252.3
```

---

## Root Cause

Weak password configuration (`Password1`) allowed successful brute-force guessing.

---

## Impact Assessment

* Unauthorized account access achieved.
* Potential for privilege escalation and persistence.
* Confidentiality and integrity risks identified.

---

## MITRE ATT&CK Mapping

* T1110 – Brute Force
* T1078 – Valid Accounts

---

## Recommendations

* Reset compromised account password.
* Disable password authentication.
* Enable SSH key authentication.
* Deploy Fail2Ban.
* Implement SIEM detection rules.
* Introduce MFA controls.

---

## Conclusion

The investigation successfully identified, analysed, and confirmed an SSH brute-force compromise through Linux authentication log analysis.
