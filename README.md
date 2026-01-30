
<div align="center">
  <img
    src="https://github.com/user-attachments/assets/ec419623-4575-4fe9-aa19-a7363201155b"
    alt="banner"
    width="128"
  />
  <h1>yuki-antiddos</h1>
  <p><b>Minimalist L3–L4 Anti-DDoS powered by nftables</b></p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Backend-nftables-0f172a?style=for-the-badge&labelColor=020617" />
  <img src="https://img.shields.io/badge/Protection-L3--L4-0f172a?style=for-the-badge&labelColor=020617" />
  <img src="https://img.shields.io/badge/Filtering-STATEFUL-0f172a?style=for-the-badge&labelColor=020617" />
  <img src="https://img.shields.io/badge/License-AGPL--3.0-0f172a?style=for-the-badge&labelColor=020617" />
</p>

---

## ❓ What is this?

**yuki-antiddos** is a lightweight L3–L4 anti-DDoS ruleset built on top of **nftables** and Linux kernel tuning.

It is designed to mitigate **CPU-exhausting network attacks** with:
- minimal overhead
- kernel-level filtering
- no userspace packet processing

This project targets environments where:
- bandwidth is not the main bottleneck
- CPU exhaustion is the real problem
- provider-side DDoS protection is insufficient

Works on:
- servers
- desktops & laptops (including hostile public networks)
- routers (with minor manual adjustments)

---

## 🧠 Why this exists

This project was born out of necessity.

A production server was targeted with **advanced L3–L4 attacks**.  
The hosting provider claimed to have DDoS protection — and technically, they did.

However:
- it only covered attacks that saturated bandwidth
- it did not protect against attacks designed to **overload CPU**

No hosting provider used at the time offered protection against the specific attack patterns being used.

Existing public rulesets:
- were inefficient
- caused unnecessary CPU load
- or failed under real attack conditions

So the decision was made to write a custom ruleset focused specifically on **CPU-bound attack mitigation**.

The result provided full coverage for the observed attack vectors.  
Since there were no solid ready-made solutions at the time, this project was later shared publicly.

---

## 🧨 Threat model

### What this protects against
- UDP floods
- SYN floods
- Reflection & amplification attacks
- Spoofed traffic
- High PPS junk traffic at L3–L4

### What this does NOT protect against
- L7 / application-layer attacks
- Slowloris-style attacks
- Abuse of valid application logic
- Attacks hidden behind TLS
- Payload-level inspection attacks

---

## ⚡️ Performance philosophy

This ruleset is optimized primarily for **minimal CPU usage** under high packet rates.

Core principles:
- early packet drops
- short rule traversal paths
- avoiding expensive matches in hot chains
- no logging at all

The goal is not to analyze traffic, but to **reject garbage as early and cheaply as possible**.

As a result, the ruleset remains effective under large PPS floods while keeping CPU usage stable.

---

## ⚙️ Features

- 🧬 Split-Chain Architecture
- 🛑 Drop Policy
- 📶 Stateful 2-Stage UDP rate limiting
- 🛡️ Sysctl Hardening
- 🔄 Easy Updates

---

## 📦 Installation

> ⚠️ This will remove `ufw`, `firewalld`, and their configs.

```bash
sudo apt update \
  && sudo apt purge ufw firewalld -y \
  && sudo apt install nftables git bc iproute2 -y \
  && git clone https://github.com/mintyYuki/antiddos \
  && cd antiddos \
  && sudo bash antiddos-yuki
````

---

## 🧪 Compatibility

| Distribution       | Status                          |
| ------------------ | ------------------------------- |
| **Ubuntu 24.04+**  | ✅ Fully supported, recommended |
| **Ubuntu < 24.04** | ⚠️ Not recommended              |
| **Debian 12+**     | 🟡 Partially supported          |
| **Other distros**  | ❌ Not supported                |

---

## 📋 Dependencies

* **nftables** — packet filtering backend
* **git** — repository cloning
* **bc**, **iproute2** — script utilities

---

## 🔄 Updates & maintenance

Updating is straightforward:

* pull the latest changes from Git
* re-run the installation script

The ruleset is designed to be easily re-applied without restarting the network or the system.

Rollback mechanisms are currently limited.
Always test updates on non-critical systems first.

---

## ⚠️ Known issues & limitations

### Rules persistence

On some systems, nftables rules may not survive reboot due to service behavior.
This is not critical but may require a custom workaround.

### Stability

There are no automated tests.
Most testing happens on real servers under real workloads.

### Rollback safety

Automatic rollback is incomplete.
In rare edge cases, SSH access may break without proper rollback.

### Oracle Cloud

Oracle Cloud heavily relies on preconfigured iptables rules.
This script wipes existing rules and may break networking.
Not supported.

### iptables-nft

Not supported.

---

## 📚 FAQ

👉 [https://github.com/mintyYuki/antiddos/wiki/FAQ](https://github.com/mintyYuki/antiddos/wiki/FAQ)
