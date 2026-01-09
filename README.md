<div align="center">
  <img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/ec419623-4575-4fe9-aa19-a7363201155b"
       alt="banner"
       style="width: 8%; height: auto;" />
    <h1>yuki-antiddos</h1>
</div>

<p align="center">
<img src="https://img.shields.io/badge/Backend-nftables-0f172a?style=for-the-badge&labelColor=020617" />
<img src="https://img.shields.io/badge/Protection-L3--L4-0f172a?style=for-the-badge&labelColor=020617" />
<img src="https://img.shields.io/badge/Filtering-STATEFUL-0f172a?style=for-the-badge&labelColor=020617" />
<img src="https://img.shields.io/badge/Layer-KERNEL--LEVEL-0f172a?style=for-the-badge&labelColor=020617" />
<img src="https://img.shields.io/badge/License-AGPL--3.0-0f172a?style=for-the-badge&labelColor=020617" />
</p>

## ❔ What this is?
yuki-antiddos is a simple project aimed at mitigating most of the L3-L4 attacks by using just nftables and kernel tweaks. It's made for servers, desktops, laptops (what if you need more security in public networks for your lappy?), and routers (additional configuration is needed in this case, although it should be simple and all you'd need is to add the required rules inside the 20-user.nft file). It's capable of filtering even the most sophisticated attacks at the same time leaving your legitimate traffic untouched and not impacting the overall performance and CPU load. To know how is this possible, continue reading.

## ⏩ **Optimization**
Most of the ruleset makers forget about optimization; We don't.
Our custom techniques allow for filtering out attacks with massive PPS rates without causing unnecessary strain on your server's CPU.

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

## ⚠️ Known issues & limitations

- Rules don't persist after reboot on some systems
  Caused by an nftables service issue.
  Most likely this will require either a custom service or a workaround around the existing nftables service.
  The issue is non-trivial, so it won`t be fixed quickly — fortunately, it’s also not critical.

- Overall stability
  I didn't write any tests or anything for this project. It isn't profitable either and I got $0 of donations, as of moment of writing this. Sometimes, when I make minor changes and don't test anything to save time, stuff breaks. Thus, there might be some weird issues, although I use it on some of my servers myself with real-world workloads and review people's feedback.

- Safety / rollback reliability
  Automatic rollback is currently incomplete. In some edge cases, if SSH access breaks, the rules might not rollback correctly. I didn't get enough information about such issues, so if you're able to provide some debug information, you can do this and open an issue - I'll review it and attempt to fix.

- Compatibility with Oracle Cloud instances
  The script will likely make your network stop working if you'll try to run it on a Oracle Cloud instance. This is caused by the script wiping all the rules before applying its own ones. This cloud provider uses lots of nftables/iptables rules, that's why it happens. It's not clear yet what should be done to work this around.

  Planned improvements:
  - rollback with a timer
  - removing or redesigning automatic ruleset saving
  - generally making rollback behavior more reliable

  Important:
  Always make backups.
  If SSH is your only way to access the server, the server is important, and you don't have backups — do not install this script yet.

- iptables-nft compatibility
  It's basically non-existent.


## ⁉️ <a href="https://github.com/mintyYuki/antiddos/wiki/FAQ">FAQ</a>
