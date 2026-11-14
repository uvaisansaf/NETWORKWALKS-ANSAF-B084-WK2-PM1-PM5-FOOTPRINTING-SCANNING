<div align="center">

# 🛡️ Week 2 — Footprinting & Network Scanning
### Networkwalks Cybersecurity Internship 2026 · Batch B084

**Uvais Ansaf Ahameth** · Cybersecurity Intern · ID `NW-084-3AW`

![Week](https://img.shields.io/badge/Week-02-1F5FBF?style=for-the-badge)
![Modules](https://img.shields.io/badge/Modules-PM4%20%2B%20PM5%20%2B%20FINAL-0E8C7F?style=for-the-badge)
![Phase](https://img.shields.io/badge/Phases-Recon%20%E2%86%92%20Scanning-16365C?style=for-the-badge)
![Scope](https://img.shields.io/badge/Scope-Public%20info%20%2B%20permitted%20network-2E7D32?style=for-the-badge)

📄 **[Read the full report (PDF)](W2-PM-FINAL_Report_Uvais_Ansaf_Ahameth.pdf)**

</div>

---

## 📌 What this project covers

| Module | Task | Status |
|---|---|---|
| **W2-PM4** | Footprint **microsoft.com** with **theHarvester** (passive, public sources only) | ✅ Done |
| **W2-PM5** | **Zenmap** host discovery on a network used with the owner's permission: live hosts, IPs, MACs, topology PDF | ✅ Done |
| **W2-PM-FINAL** | Professional report covering both phases | ✅ Done |

> **Scope:** public information only for microsoft.com (as given in the lab guide) and a local network used with the owner's permission. Passive recon and ping-scan host discovery only — **no exploitation**.

---

## 🔎 Phase 1 — Footprinting with theHarvester (W2-PM4)

| Task | Command | Result |
|---|---|---|
| 1. Baidu, limit 1000 | `theHarvester -d microsoft.com -l 1000 -b baidu` | **No results** (no IPs, emails, people or hosts) |
| 2. Six free sources, limit 50 | `theHarvester -d microsoft.com -l 50 -b crtsh,rapiddns,otx,urlscan,hackertarget,robtex` | **603 hosts**, **713 IPs**, **4 URLs**, **2 ASNs**, **0 emails**, 0 people |

**Examples of hosts found:** `www.microsoft.com`, `workflow.ex.azure.microsoft.com`, `www.partners.extranet.microsoft.com`, `uddi.beta.microsoft.com`

👉 **Lesson:** one source is not enough. Baidu alone returned nothing, while six free sources together mapped hundreds of hosts, all without touching the target's systems.

Raw outputs: [`task1_baidu.txt`](task1_baidu.txt) · [`task2_all.txt`](task2_all.txt)

---

## 🌐 Phase 2 — Network Scanning with Zenmap (W2-PM5)

| Task | Answer |
|---|---|
| 1. Install Zenmap | Nmap / Zenmap **7.993** from the official nmap.org installer |
| 2. IP & subnet | IP **10.181.54.22**, mask **255.255.255.0 (/24)** → subnet **10.181.54.0/24**, gateway **10.181.54.50** (found with `nmap --iflist`) |
| 3. Live hosts | Zenmap **Ping scan** → `nmap -sn 10.181.54.0/24` |
| 4. How many live? | **3 hosts** (including the scanning PC), 256 addresses scanned in 15.79 s |
| 5 & 6. IPs + MACs | see table below |
| 7. Topology PDF | Saved from the Topology tab with the legend on → [`Zenmap_Topology_Ansaf_WK2.pdf`](Zenmap_Topology_Ansaf_WK2.pdf) |

| IP address | MAC address | Device |
|---|---|---|
| 10.181.54.7 | `FA:14:D9:E8:63:D5` | Another device on the hotspot (vendor unknown) |
| 10.181.54.50 | `92:EA:19:A6:D1:7E` | Mobile hotspot (default gateway) |
| 10.181.54.22 | *not shown by Nmap* | The scanning PC (Nmap does not show the MAC of its own interface) |

Both visible MACs show as "Unknown" vendor, which is normal for phones using random (private) MAC addresses.

📸 All screenshots are in [`screenshots/`](screenshots/).

---

## ⚠️ Risk summary

| Observation | Risk |
|---|---|
| Many sub-domains of the target listed from public sources | 🟠 Medium |
| Email addresses collectable from public sources | 🟢 Low |
| Hosts and IPs visible in public records | 🟢 Low |
| All devices on the local network answer a ping scan | 🟢 Low |

These are observations from information gathering, not confirmed vulnerabilities. Full analysis and recommendations are in the [report](W2-PM-FINAL_Report_Uvais_Ansaf_Ahameth.pdf).

---

## 🧰 Troubleshooting share

**Issue 1:** My laptop with the Week 1 Kali Linux VM was not available this week.
**Fix:** Ran theHarvester on a Debian Linux terminal (Google Cloud Shell) with the same commands as the lab guide, and Zenmap on a friend's Windows PC (hotspot network, with the owner's permission).

**Issue 2:** `theHarvester -b all` stayed stuck for a long time, and many sources were skipped with "missing credentials" because they need API keys.
**Fix:** Stopped it and re-ran with six free sources: `crtsh, rapiddns, otx, urlscan, hackertarget, robtex`.

**Zenmap tip:** No CMD needed for Task 2. Run `nmap --iflist` in Zenmap's Command box to get your IP, subnet and default gateway in one view.

---

## 📁 Repository structure

```
├── README.md
├── W2-PM-FINAL_Report_Uvais_Ansaf_Ahameth.pdf   → final report
├── task1_baidu.txt                              → raw output, Task 1
├── task2_all.txt                                → raw output, Task 2
├── Zenmap_Topology_Ansaf_WK2.pdf                → Zenmap topology (with legend)
└── screenshots/                                 → screenshots for every task
```

---

<div align="center">

⚖️ *For educational purposes only. Only public information and a network used with permission.*

**Uvais Ansaf Ahameth** · Networkwalks Cybersecurity Internship · Batch B084

Thanks to **Networkwalks** for the internship.

</div>
