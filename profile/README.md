<div align="center">

```
╦  ╔═╗╦  ╦╦╔═╗╔╦╗╦ ╦╔═╗╔╗╔  ╔═╗╔═╗╔═╗╔═╗╔═╗
║  ║╣ ╚╗╔╝║╠═╣ ║ ╠═╣╠═╣║║║  ║ ║╠╣ ╠╣ ╚═╗║╣ 
╩═╝╚═╝ ╚╝ ╩╩ ╩ ╩ ╩ ╩╩ ╩╝╚╝  ╚═╝╚  ╚  ╚═╝╚═╝
```

### Deterministic Attack Surface Intelligence & Firmware Vulnerability Research

[![Platform](https://img.shields.io/badge/Platform-leviathan.ac-00ffcc?style=for-the-badge&logo=googlechrome&logoColor=black)](https://leviathan.ac)
[![Research](https://img.shields.io/badge/Research-Dossiers-00f0ff?style=for-the-badge&logo=gitbook&logoColor=black)](https://leviathan.ac/research/)
[![License](https://img.shields.io/badge/License-MIT-111827?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Author](https://img.shields.io/badge/Lead-@cyeezy08-161b22?style=for-the-badge&logo=github)](https://github.com/cyeezy08)

<p align="center">
  <b>High-throughput Go engines, stateless perimeter diffing, and auditable risk scoring.</b><br>
  Built for red teams, bug bounty hunters, and security engineers who value precision over vendor noise.
</p>

</div>

---

### The Anti-Noise Philosophy

Most enterprise Attack Surface Management (ASM) platforms sell heavy background daemons, closed-source dashboards, and generic CVSS scores that drown security teams in false positives. 

**Leviathan OffSec builds the counter-weight:**

* **Stateless & Composable:** Standard UNIX philosophy. Tools accept input on `stdin`, stream clean data on `stdout`, and exit `1` on a delta. No databases, no mandatory daemons, and zero cloud vendor lock-in.
* **Verified Takeover Signatures:** 81 fingerprints verified across 21 cloud providers. `HostageLVX` checks claimability—not just dangling CNAME presence—preventing alerts on active cloud buckets.
* **Radical Coverage Transparency:** If a target plugin or component is not in the advisory database, `FenrirLVX` prints the exact coverage ratio (`3/7 matched, 4 with no data`). We never silently report unanalyzed attack surfaces as "clean".
* **Auditable Math, Not Black Boxes:** `leviathan-core` ranks risk mathematically by combining raw CVSS vectors with EPSS probability and CISA Known Exploited Vulnerabilities (KEV) data.
* **Instruction-Level Research:** We publish our firmware and protocol research in full—including reverse engineering dead-ends, binary disassemblies, and Unicorn CPU emulation transcripts.

---

### Chained Pipeline Architecture

Tools are modular and chain seamlessly inside standard cron jobs, GitHub Actions, and recon scripts:

```
┌────────────────────────────────┐
│ Recon Feeds (httpx, subfinder) │
└───────────────┬────────────────┘
                │ stdin
                ▼
┌────────────────────────────────┐
│          surfacediff           │ ───[ Delta Exit 1 ]───► Instant Alert / Webhook
└───────────────┬────────────────┘
                │ changed perimeters
                ▼
┌────────────────────────────────┐      ┌────────────────────────────────┐
│           HostageLVX           │      │           FenrirLVX            │
│ (81 Takeover Fingerprints, Go) │      │  (CMS Fingerprinting, Go)      │
└───────────────┬────────────────┘      └───────────────┬────────────────┘
                │ verified findings                     │ coverage verdicts
                └───────────────┬───────────────────────┘
                                ▼
                ┌────────────────────────────────┐
                │         leviathan-core         │
                │ (Auditable EPSS/KEV Risk Math) │
                └────────────────────────────────┘
```

---

### Tooling Suite

| Tool | Core Function | Stack | Install Command |
| :--- | :--- | :--- | :--- |
| **[`surfacediff`](https://github.com/leviathan-offsec/surfacediff)** | Content-addressed perimeter snapshots & deterministic field diffing. Exits `1` on deltas. | Python (Stdlib) | `pip install git+https://github.com/leviathan-offsec/surfacediff.git` |
| **[`HostageLVX`](https://github.com/leviathan-offsec/HostageLVX)** | High-concurrency dangling DNS and subdomain takeover engine with 81 cloud signatures. | Go | `go install github.com/leviathan-offsec/HostageLVX@latest` |
| **[`FenrirLVX`](https://github.com/leviathan-offsec/FenrirLVX)** | WordPress & CMS attack surface auditor with offline CVE correlation and coverage reporting. | Go | `go install github.com/leviathan-offsec/FenrirLVX@latest` |
| **[`leviathan-core`](https://github.com/leviathan-offsec/leviathan-core)** | Deterministic risk scoring kernel computing from CVSS vectors, EPSS, and CISA KEV. | Python | `pip install git+https://github.com/leviathan-offsec/leviathan-core.git` |
| **[`[a private repo]`](https://github.com/leviathan-offsec/[a private repo])** | Passive threat intelligence correlation scoped strictly to authorized perimeters. | Python | `git clone https://github.com/leviathan-offsec/[a private repo].git` |

---

### Published Research Dossiers

Deep-dive offensive security writeups published directly from the lab:

* 🔬 **[Offline WordPress Scanners: What They Find and What They Don't](https://leviathan.ac/posts/offline-wordpress-scanner-comparison/)**
  * *Four offline scanners (CMSmap, Nuclei, Wapiti, FenrirLVX) tested against advisory data gaps and silent failures.*
* 🔬 **[80 Days on an IoT DVR: Three Real Bugs, No Bounty](https://leviathan.ac/posts/80-days-reversing-iot-dvr/)**
  * *HiSilicon ARM32 surveillance firmware across 28,006 units: hardcoded AES-256 keys, unsigned root bootloader chains, and blocklist bypasses proven with Unicorn Engine emulation.*
* 📚 **[Browse All Research & Published Advisories →](https://leviathan.ac/research/)**

---

<div align="center">
  <sub>Operated exclusively against authorized infrastructure. Research conducted by <a href="https://github.com/cyeezy08">@cyeezy08</a>.</sub><br>
  <sub>Official Site: <a href="https://leviathan.ac">leviathan.ac</a> · Verified Domain: <code>leviathan.ac</code></sub>
</div>
