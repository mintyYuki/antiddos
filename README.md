<div align="center">
  <img src="https://github.com/user-attachments/assets/96b9d177-fe29-41f4-8a6e-7731d5696409"
       alt="banner"
       style="width: 7%; height: auto;" />
    <h1> yuki-antiddos</h1>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Backend-nftables-red?style=for-the-badge" alt="Backend: nftables"/>
  <img src="https://img.shields.io/badge/License-MIT-blueviolet?style=for-the-badge" alt="License: MIT"/>
  <img src="https://img.shields.io/badge/Protection-L3--L4-critical?style=for-the-badge&logo=linux" alt="Protection Level: L3-L4"/>
  <img src="https://img.shields.io/badge/Ubuntu-24.04%2B-orange?style=for-the-badge&logo=ubuntu" alt="OS: Ubuntu 24.04+"/>
</p>

## ❔ What this is?
yuki-antiddos is a simple project aimed at mitigating most of the L3-L4 attacks by using just nftables and kernel tweaks. It's made for servers, desktops (what if you need more security in public networks for your Linux laptop?), and routers (additional configuration needed in this case). It's capable of filtering even the most sophisticated attacks at the same time leaving your legitimate traffic untouched and not impacting the overall performance and CPU load. To know how is this possible, continue reading.

## ⏩ **Optimization**
Most of the ruleset makers forget about optimization; We don't.
Our custom techniques allow for filtering out attacks with massive PPS rates without causing unnecessary strain on your server’s CPU.

## ⚙️ **Features**
- 🛡️ Split-chain system
- ⛔ Default drop policy
- 📶 Two-stage UDP stateful rate limiting
- 🧩 Sysctl-level kernel tuning

## 📦 **Installation**
```
sudo apt update && sudo apt purge ufw firewalld -y && sudo apt install nftables git bc iproute2 -y && git clone https://github.com/mintyYuki/antiddos && cd antiddos && sudo bash antiddos-yuki && cd ..
```

## 🧪 **Compatibility**

| Distribution       | Status                 |
|--------------------|------------------------|
| **Ubuntu 24.04+**   | Fully supported and recommended  |
| **Ubuntu < 24.04**  | Not recommended                  |
| **Debian 12+**      | Partially supported              |
| **Other distros**   | Not supported                    |

## 📋 **Dependencies**
- Nftables, for packet filtering
- Git, to clone the repository

## ⚠️ **Currently known problems/bugs**
- Rules don't persist across reboots (Caused by an nftables service error).
#### (I'm working on this problem; Would either need to make a custom service and use it or just make a workaround for the nftables service. This issue is complicated so I cannot solve it quickly + it's not that critical)
- Overall stability (There were many changes in the past and at the same time the script didn't get tested very well, so there may be weird bugs)
- Safety (Also, automatic rollback is a bit incomplete and won't roll the rules back if your SSH stops working, which sometimes happens due to unknown reasons. I will implement automatic roll-back with a timer soon, remove ruleset auto-saving probably or make it smarter, and make the automatic rollback better overall)
#### (Please don't forget to make backups, it's always a good practice. If SSH is your only method to access your server and it's important for you + you don't have backups -> don't even think about installing the script yet, please.)
- iptables-nft compatibility

## ⁉️ <a href="https://github.com/mintyYuki/antiddos/wiki/FAQ">FAQ</a>
