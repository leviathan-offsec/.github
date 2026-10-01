<div align="center">

  <img src="https://raw.githubusercontent.com/leviathan-offsec/.github/main/profile/banner.svg" alt="Leviathan OffSec Banner" width="100%" />

  <br><br>

  [![Platform](https://img.shields.io/badge/Platform-leviathan.ac-00ffcc?style=for-the-badge&logo=googlechrome&logoColor=07090e)](https://leviathan.ac)
  [![Research](https://img.shields.io/badge/Research-Dossiers-38bdf8?style=for-the-badge&logo=gitbook&logoColor=07090e)](https://leviathan.ac/research/)
  [![License](https://img.shields.io/badge/License-MIT-0d111a?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](https://opensource.org/licenses/MIT)
  [![Lead](https://img.shields.io/badge/Lead-@cyeezy08-1e293b?style=for-the-badge&logo=github&logoColor=white)](https://github.com/cyeezy08)

  <br>

  <p align="center">
    <b>Stateless perimeter diffing, high-concurrency takeover detection, and transparent CMS auditing.</b><br>
    Built for red teams, bug bounty hunters, and defensive engineers who value deterministic signals over vendor noise.
  </p>

</div>

---

### The Anti-Noise Philosophy

Most modern Attack Surface Management (ASM) platforms push proprietary cloud dashboards, heavy background daemons, and inflated CVSS scores that drown teams in false positives. 

**Leviathan OffSec builds the deterministic alternative:**

| Capability | Traditional ASM / Scanners | Leviathan OffSec Suite |
| :--- | :--- | :--- |
| **Runtime Model** | Heavy background agents, persistent daemons | **Stateless CLI tools** (`stdin` &rarr; `stdout`) |
| **Pipeline Integration** | Proprietary webhooks & dashboards | **Exit Code `1` on deltas** (native UNIX cron) |
| **Subdomain Takeovers** | Simple CNAME matching (high false alarms) | **81 verified claimability signatures** across 21 clouds |
| **Advisory Coverage** | Silent failure when plugin has no templates | **Explicit match-to-unknown coverage ratios** printed |
| **Risk Prioritization** | Proprietary vendor score black-boxes | **Auditable math:** CVSS vectors + EPSS + CISA KEV |
| **Licensing** | Enterprise SaaS paywalls | **100% Free & Open Source (MIT)** |

---

### Chained Pipeline Architecture

Leviathan tools follow the standard UNIX philosophy: each tool does one job deterministically and composes cleanly inside standard bash scripts, cron jobs, or GitHub Actions:

```
┌──────────────────────────────────────────────┐
│  Target Perimeters (httpx, subfinder, naabu) │
└──────────────────────┬───────────────────────┘
                       │ stdin (JSONL / hosts)
                       ▼
┌──────────────────────────────────────────────┐
│                 surfacediff                  │ ───[ Delta Exit 1 ]───► Instant Slack/Webhook
│    (Content-Addressed Perimeter Snapshots)   │
└──────────────────────┬───────────────────────┘
                       │ changed / new assets
                       ▼
         ┌─────────────────────────────┐
         │                             │
         ▼                             ▼
┌─────────────────────────────┐ ┌─────────────────────────────┐
│         HostageLVX          │ │          FenrirLVX          │
│   (Subdomain Takeovers)     │ │   (CMS Surface Auditor)     │
│ 81 Multi-Cloud Fingerprints │ │ Transparent Advisory Ratio  │
└──────────────┬──────────────┘ └──────────────┬──────────────┘
               │ verified findings             │ coverage data
               └──────────────┬────────────────┘
                              ▼
┌──────────────────────────────────────────────┐
│                leviathan-core                │
│    (Auditable CVSS + EPSS + KEV Risk Math)   │
└──────────────────────────────────────────────┘
```

---

### Core Tooling Suite

<table>
  <thead>
    <tr>
      <th>Tool</th>
      <th>Focus</th>
      <th>Stack</th>
      <th>Quick Install</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://github.com/leviathan-offsec/surfacediff"><b>surfacediff</b></a></td>
      <td>Immutable, content-addressed perimeter snapshots and field-by-field diffing. Exits <code>1</code> on any detected delta.</td>
      <td><code>Python</code> (stdlib)</td>
      <td><code>pip install git+https://github.com/leviathan-offsec/surfacediff.git</code></td>
    </tr>
    <tr>
      <td><a href="https://github.com/leviathan-offsec/HostageLVX"><b>HostageLVX</b></a></td>
      <td>High-speed dangling DNS and subdomain takeover engine with 81 CNAME fingerprints across 21 cloud providers.</td>
      <td><code>Go</code> (CLI)</td>
      <td><code>go install github.com/leviathan-offsec/HostageLVX@latest</code></td>
    </tr>
    <tr>
      <td><a href="https://github.com/leviathan-offsec/FenrirLVX"><b>FenrirLVX</b></a></td>
      <td>WordPress and CMS vulnerability scanner with offline CVE correlation and transparent coverage-gap reporting.</td>
      <td><code>Go</code> (CLI)</td>
      <td><code>go install github.com/leviathan-offsec/FenrirLVX@latest</code></td>
    </tr>
    <tr>
      <td><a href="https://github.com/leviathan-offsec/leviathan-core"><b>leviathan-core</b></a></td>
      <td>Contract-enforced risk ranking kernel computing from raw CVSS vectors, EPSS probabilities, and CISA KEV status.</td>
      <td><code>Python</code> (Kernel)</td>
      <td><code>pip install git+https://github.com/leviathan-offsec/leviathan-core.git</code></td>
    </tr>
    <tr>
      <td><a href="https://github.com/leviathan-offsec/leviathan-intel"><b>leviathan-intel</b></a></td>
      <td>Passive threat intelligence correlation and asset telemetry scoped strictly to authorized environments.</td>
      <td><code>Python</code></td>
      <td><code>git clone https://github.com/leviathan-offsec/leviathan-intel.git</code></td>
    </tr>
  </tbody>
</table>

---

### Quickstart: 60-Second Attack Surface Pipeline

```bash
# 1. Probe your target perimeter and snapshot state
subfinder -d example.com -silent | httpx -json -silent | surfacediff snap -l prod

# 2. On the next cron run, diff for changes (exits 1 if new hosts or changed titles appear)
surfacediff diff -l prod || echo "[!] Perimeter modified since last snapshot"

# 3. Audit all discovered subdomains for verified takeovers
HostageLVX -l subs.txt -threads 50

# 4. Fingerprint web applications and evaluate transparent database coverage
fenrir -t https://target.example.com
```

---

### Published Research Dossiers

We publish complete offensive engineering research—including hardware disassemblies, failed hypotheses, and binary reversing post-mortems:

<table>
  <tr>
    <td width="50%">
      <div style="font-family: monospace; font-size: 0.72rem; color: #38bdf8; margin-bottom: 0.4rem;">// RESEARCH DOSSIER 0x02</div>
      <h4><a href="https://leviathan.ac/posts/offline-wordpress-scanner-comparison/">Offline WordPress Scanners Compared</a></h4>
      <p>CMSmap, Nuclei, Wapiti, and FenrirLVX benchmarked against advisory feeds and silent failure modes when plugins are missing from local databases.</p>
      <sub>October 2026 &middot; 9 min read &middot; <a href="https://leviathan.ac/posts/offline-wordpress-scanner-comparison/">Read Dossier &rarr;</a></sub>
    </td>
    <td width="50%">
      <div style="font-family: monospace; font-size: 0.72rem; color: #38bdf8; margin-bottom: 0.4rem;">// RESEARCH DOSSIER 0x01</div>
      <h4><a href="https://leviathan.ac/posts/80-days-reversing-iot-dvr/">80 Days on an IoT DVR: Three Real Bugs, No Bounty</a></h4>
      <p>HiSilicon ARM32 surveillance firmware across 28,006 units: static AES keys, unsigned root bootloaders, and command injections emulated with Unicorn Engine.</p>
      <sub>September 2026 &middot; 16 min read &middot; <a href="https://leviathan.ac/posts/80-days-reversing-iot-dvr/">Read Dossier &rarr;</a></sub>
    </td>
  </tr>
</table>

<div align="center">
  <p><b><a href="https://leviathan.ac/research/">Browse All Research &amp; Published Vulnerability Advisories &rarr;</a></b></p>
</div>

---

### Ethics & Operational Boundaries

* **Passive by Default:** Our intelligence tools prioritize index queries, DNS enumeration, and public vulnerability metadata. No invasive payloads are dispatched to unconfirmed targets.
* **Authorized Testing Only:** Active penetration tests require explicit written scope and authorization.
* **Intellectual Honesty:** If an exploit cannot reach the network or a vendor patched the gate, we state it plainly. Evidence over speculation.

---

<div align="center">
  <sub>Research lab directed by <a href="https://github.com/cyeezy08">@cyeezy08</a>.</sub><br>
  <sub>Official Laboratory Portal: <a href="https://leviathan.ac"><b>leviathan.ac</b></a> &middot; Verified Organization Domain: <code>leviathan.ac</code></sub>
</div>
