<div align="center">

# LEVIATHAN OFFSEC

**High-Throughput Unix Security Tooling & Autonomous Recon Architecture**

[![Web](https://img.shields.io/badge/Platform-leviathan.ac-00ffcc?style=for-the-badge&logo=firefox&logoColor=black)](https://leviathan.ac)
[![License](https://img.shields.io/badge/License-MIT-111111?style=for-the-badge)](https://opensource.org/licenses/MIT)

</div>

---

### Core Arsenal

| Tool | Focus | Language | One-Line Install |
| :--- | :--- | :--- | :--- |
| **[`HostageLVX`](https://github.com/leviathan-offsec/HostageLVX)** | Subdomain & Dangling DNS Takeovers (30+ providers) | Go | `go install -v github.com/leviathan-offsec/HostageLVX@latest` |
| **[`surfacediff`](https://github.com/leviathan-offsec/surfacediff)** | Perimeter Snapshotting & Delta Diffing | Python (stdlib) | `pip install git+https://github.com/leviathan-offsec/surfacediff.git` |
| **[`FenrirLVX`](https://github.com/leviathan-offsec/FenrirLVX)** | WordPress Attack Surface & Offline CVE Triage | Go | `go install -v github.com/leviathan-offsec/FenrirLVX@latest` |
| **[`leviathan-core`](https://github.com/leviathan-offsec/leviathan-core)** | Contract-Enforced Risk Scoring (CVSS/EPSS/KEV) | Python | `git clone https://github.com/leviathan-offsec/leviathan-core.git` |
| **[`agy-mcp`](https://github.com/leviathan-offsec/agy-mcp)** | Hardened FastMCP Server for AI Coding Assistants | Python | `git clone https://github.com/leviathan-offsec/agy-mcp.git` |

---

### Architectural Principles

* **Unix Composability:** Tools read `stdin` and write deterministic `stdout` / structured JSONL so they chain naturally with `subfinder`, `httpx`, and standard Unix pipelines.
* **Zero Dependency Philosophy:** Standalone compiled Go binaries and standard-library Python utilities. No fragile dependency trees or bloated runtime containers.
* **Deterministic Verification:** Contract-enforced math against CVSS, FIRST EPSS, and CISA KEV feeds. Zero black-box scoring algorithms.

---

### Featured Research

* **[80 Days Reverse Engineering an IoT DVR](https://leviathan.ac/posts/80-days-reversing-iot-dvr.html)**: Technical teardown of stripped ARM32 surveillance firmware, recovering hardcoded AES-128 keys, and an honest post-mortem on hardware target selection.

---

<div align="center">
  <sub>Research Lab founded by <a href="https://github.com/cyeezy08">@cyeezy08</a> · <a href="https://leviathan.ac">leviathan.ac</a></sub>
</div>
